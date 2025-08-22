# Proof-of-Intent (PoI) Receipt Schema

This document defines the schema for Proof-of-Intent receipts - cryptographic artifacts that prove why an AI agent is taking a specific action.

## Overview

A PoI receipt is a JSON document that cryptographically proves an agent's intent before executing privileged operations. It serves as a tamper-evident record of:
- Who initiated the action and why
- What capabilities were granted
- Risk context and policy compliance
- Cryptographic attestations for verification

## Table of Contents

- [Schema Version](#schema-version)
- [Root Object Structure](#root-object-structure)
- [Field Definitions](#field-definitions)
  - [Core Metadata](#core-metadata)
  - [Initiator Information](#initiator-information)
  - [Objective Declaration](#objective-declaration)
  - [Capability Grant](#capability-grant)
  - [Risk Context](#risk-context)
  - [Cryptographic Attestations](#cryptographic-attestations)
  - [Audit Trail](#audit-trail)
- [Validation Rules](#validation-rules)
- [Security Considerations](#security-considerations)
- [Cryptographic Binding](#cryptographic-binding)
- [Extensibility](#extensibility)
- [Example Usage](#example-usage)
- [Schema Evolution](#schema-evolution)

## Schema Version

**Current Version**: `agentic.poi.receipt.v1`

## Root Object Structure

```json
{
  "type": "string",
  "receipt_id": "string",
  "issued_at": "string",
  "expires_at": "string",
  "initiator": "object",
  "objective": "object",
  "capability": "object",
  "risk_context": "object",
  "attestations": "object",
  "audit": "object"
}
```

## Field Definitions

### Core Metadata

#### `type` (required)
- **Type**: `string`
- **Format**: URI-like identifier
- **Example**: `"agentic.poi.receipt.v1"`
- **Description**: Schema version identifier for the receipt format
- **Constraints**: Must match expected format for validation

#### `receipt_id` (required)
- **Type**: `string`
- **Format**:  string
- **Example**: `"4449f17eca4ac359"`
- **Description**: Unique identifier for this receipt instance
- **Constraints**: 16+ characters, globally unique

#### `issued_at` (required)
- **Type**: `string`
- **Format**: ISO 8601 UTC timestamp
- **Example**: `"2025-08-22T20:39:52Z"`
- **Description**: When the receipt was issued
- **Constraints**: Must be in the past, UTC timezone

#### `expires_at` (required)
- **Type**: `string`
- **Format**: ISO 8601 UTC timestamp
- **Example**: `"2025-08-22T20:44:52Z"`
- **Description**: When the receipt expires and becomes invalid
- **Constraints**: Must be after `issued_at`, typically short-lived (minutes to hours)

### Initiator Information

#### `initiator` (required)
Contains information about who or what initiated the action.

```json
{
  "human": "object",
  "agent_lineage": "array"
}
```

##### `initiator.human` (optional)
- **Type**: `object`
- **Description**: Human user who originally requested the action
- **Fields**:
  - `sub`: Subject identifier (e.g., `"user:4345654345654345654"`)
  - `session_id`: Active session identifier (e.g., `"sess-4f92a7"`)

##### `initiator.agent_lineage` (required)
- **Type**: `array`
- **Description**: Chain of agents that led to this action
- **Array Elements**: Each element contains:
  - `agent_id`: Agent identifier (e.g., `"agent://sales-reporter@v1.3.2"`)
  - `spawn_reason`: Why this agent was created (e.g., `"scheduled_report"`)

### Objective Declaration

#### `objective` (required)
Describes what the agent intends to accomplish.

```json
{
  "description": "string",
  "task_hash": "string"
}
```

##### `objective.description` (required)
- **Type**: `string`
- **Example**: `"Export Q2 revenue by product to S3"`
- **Description**: Human-readable description of the task
- **Constraints**: Clear, specific, actionable description

##### `objective.task_hash` (required)
- **Type**: `string`
- **Format**: SHA-256 hash (64 characters)
- **Example**: `"0ceab96dcb0711521e4776cd7e32c73073154027154955e14c4944069c6c5933"`
- **Description**: Cryptographic hash of the task definition
- **Constraints**: Must match the actual task being executed

### Capability Grant

#### `capability` (required)
Defines what the agent is allowed to do.

```json
{
  "mode": "string",
  "scope": "object",
  "ttl": "string",
  "audience": "string",
  "issued_by": "string",
  "icp_signature": "string"
}
```

##### `capability.mode` (required)
- **Type**: `string`
- **Values**: `"just-in-time"`, `"delegated"`, `"emergency"`
- **Description**: How the capability was granted
- **Constraints**: Must be one of the predefined values

##### `capability.scope` (required)
- **Type**: `object`
- **Description**: What actions and resources are permitted
- **Fields**:
  - `actions`: Array of permitted actions (e.g., `["s3:PutObject"]`)
  - `resources`: Array of target resources (e.g., `["arn:aws:s3:::finance-reports/q2-*.csv"]`)

##### `capability.ttl` (required)
- **Type**: `string`
- **Format**: Duration string (e.g., `"5m"`, `"1h"`)
- **Description**: Time-to-live for the capability
- **Constraints**: Must be reasonable for the action (typically minutes to hours)

##### `capability.audience` (required)
- **Type**: `string`
- **Format**: Resource identifier
- **Example**: `"arn:aws:s3:::finance-reports"`
- **Description**: Target system or service for the action

##### `capability.issued_by` (required)
- **Type**: `string`
- **Format**: URI-like identifier
- **Example**: `"icp://agentic/identity-control-plane"`
- **Description**: Authority that granted the capability

##### `capability.icp_signature` (required)
- **Type**: `string`
- **Format**: Base64-encoded signature
- **Example**: `"MEUCIQCs6m9...=="`
- **Description**: Digital signature from the Identity Control Plane authorizing the specific capabilities for this agent lineage
- **Constraints**: Must be verifiable against ICP's public key, signature covers capability scope and agent lineage

**Signature Coverage**: The ICP signature covers the concatenated hash of:
- Capability scope (actions + resources)
- Agent lineage chain
- Capability TTL and audience
- Receipt expiration time

### Risk Context

#### `risk_context` (required)
Provides context about the risk level and compliance status.

```json
{
  "data_sensitivity": "string",
  "env": "string",
  "anomaly_score": "number",
  "policy_version": "string",
  "signals": "array"
}
```

##### `risk_context.data_sensitivity` (required)
- **Type**: `string`
- **Values**: `"public"`, `"internal"`, `"confidential"`, `"restricted"`
- **Description**: Sensitivity level of data being accessed
- **Constraints**: Must match data classification policies

##### `risk_context.env` (required)
- **Type**: `string`
- **Values**: `"dev"`, `"staging"`, `"prod"`
- **Description**: Environment where the action occurs
- **Constraints**: Must be valid environment identifier

##### `risk_context.anomaly_score` (required)
- **Type**: `number`
- **Range**: 0.0 to 1.0
- **Example**: `0.12`
- **Description**: Risk score based on behavioral analysis
- **Constraints**: 0.0 = low risk, 1.0 = high risk

##### `risk_context.policy_version` (required)
- **Type**: `string`
- **Format**: Policy identifier
- **Example**: `"pol-2025-08-01"`
- **Description**: Version of security policies in effect
- **Constraints**: Must reference valid policy version

##### `risk_context.signals` (required)
- **Type**: `array`
- **Description**: Security signals that influenced the risk assessment
- **Examples**: `["mfa_present", "device_trusted", "ip_reputation:good"]`
- **Constraints**: Must be valid signal identifiers

### Cryptographic Attestations

#### `attestations` (required)
Provides cryptographic proof of the receipt's authenticity.

```json
{
  "agent_pubkey_fingerprint": "string",
  "icp_signature": "string",
  "witness_log_anchor": "string"
}
```

##### `attestations.agent_pubkey_fingerprint` (required)
- **Type**: `string`
- **Format**: `algorithm:hash` (e.g., `"ed25519:2f1c...ab7e"`)
- **Description**: Public key fingerprint of the executing agent
- **Constraints**: Must match agent's actual public key

##### `attestations.icp_signature` (required)
- **Type**: `string`
- **Format**: Base64-encoded signature
- **Example**: `"MEUCIQCs6m9...=="`
- **Description**: Digital signature from the Identity Control Plane
- **Constraints**: Must be verifiable against ICP's public key

##### `attestations.witness_log_anchor` (required)
- **Type**: `string`
- **Format**: Blockchain or log reference
- **Example**: `"chain://attestnet/blk-9823445#tx-17"`
- **Description**: Reference to immutable log entry
- **Constraints**: Must point to valid, immutable record

### Audit Trail

#### `audit` (required)
Provides information for audit and compliance purposes.

```json
{
  "nonce": "string",
  "merkle_root": "string",
  "log_stream": "string"
}
```

##### `audit.nonce` (required)
- **Type**: `string`
- **Format**: Hexadecimal string
- **Example**: `"b7e5c930"`
- **Description**: Unique value to prevent replay attacks
- **Constraints**: Must be unique per receipt

##### `audit.merkle_root` (required)
- **Type**: `string`
- **Format**: Hexadecimal hash
- **Example**: `"a9d4b80f..."`
- **Description**: Root of Merkle tree for receipt integrity
- **Constraints**: Must be valid cryptographic hash

##### `audit.log_stream` (required)
- **Type**: `string`
- **Format**: AWS CloudWatch log stream ARN
- **Example**: `"arn:aws:logs:us-east-1:123456789012:log-group:agent-actions"`
- **Description**: Where detailed audit logs are stored
- **Constraints**: Must be valid log stream identifier

## Validation Rules

### Required Fields
All fields marked as `(required)` must be present and non-null.

### Data Type Constraints
- String fields must not be empty
- Numeric fields must be within specified ranges
- Array fields must contain at least one element
- Timestamps must be valid ISO 8601 format

### Business Logic Constraints
- `expires_at` must be after `issued_at`
- `capability.ttl` must align with `expires_at` - `issued_at`
- `risk_context.anomaly_score` must be between 0.0 and 1.0
- All resource ARNs must be valid format
- All agent IDs must follow the specified URI format

## Security Considerations

### Immutability
- Receipts should be signed and timestamped
- Changes to receipts invalidate cryptographic signatures
- Audit logs should be immutable and tamper-evident

### Signature Verification
- **ICP Signature**: Must verify the Identity Control Plane's signature covers the exact capability scope and agent lineage
- **Agent Lineage Binding**: The signature binds capabilities to the specific chain of agents, preventing capability transfer to unauthorized agents
- **Scope Integrity**: Any modification to actions, resources, or agent lineage invalidates the ICP signature
- **Temporal Binding**: Signature includes expiration time to prevent replay attacks

### Privacy
- Sensitive information should be encrypted or redacted
- Personal identifiers should be pseudonymized when possible
- Access to receipts should be controlled and logged

### Verification
- All cryptographic signatures must be verified
- Receipt expiration must be checked before use
- Risk scores should be validated against current policies

## Extensibility

The schema is designed to be extensible:
- New fields can be added to existing objects
- New object types can be introduced
- Version numbers allow for schema evolution
- Unknown fields should be preserved during processing

## Cryptographic Binding

### Agent Lineage Binding
The ICP signature creates a cryptographic binding between:
1. **Capability Scope**: What actions and resources are permitted
2. **Agent Chain**: The specific sequence of agents authorized to use these capabilities
3. **Temporal Constraints**: When the capabilities are valid
4. **Context**: Risk assessment and policy compliance

This binding ensures that:
- Capabilities cannot be transferred to unauthorized agents
- Agent lineage changes invalidate the receipt
- Scope modifications break the signature
- Temporal constraints are cryptographically enforced

## Example Usage

See `poi_receipt_example.json` for a complete example of a valid receipt.

## Quick Reference

### Common Receipt Types

| Use Case | Capability Mode | Typical TTL | Risk Level |
|----------|----------------|-------------|------------|
| Data Export | `just-in-time` | 5-15 minutes | Low-Medium |
| Emergency Access | `emergency` | 1-2 hours | High |
| Scheduled Tasks | `delegated` | 1-24 hours | Medium |
| Interactive Sessions | `just-in-time` | 30-60 minutes | Low |

### Required Fields Checklist

- [ ] `type` - Schema version
- [ ] `receipt_id` - Unique identifier
- [ ] `issued_at` - Issue timestamp
- [ ] `expires_at` - Expiration timestamp
- [ ] `initiator.agent_lineage` - Agent chain
- [ ] `objective.description` - Task description
- [ ] `objective.task_hash` - Task hash
- [ ] `capability.scope` - Actions and resources
- [ ] `capability.icp_signature` - ICP authorization
- [ ] `risk_context` - Risk assessment
- [ ] `attestations` - Cryptographic proof
- [ ] `audit` - Audit trail

## Schema Evolution

When making changes to the schema:
1. Increment the version number in the `type` field
2. Maintain backward compatibility where possible
3. Document breaking changes clearly
4. Provide migration tools for existing receipts

## Implementation Considerations

### Cryptographic Requirements
- **Key Management**: Secure storage and rotation of ICP signing keys
- **Signature Algorithms**: Support for Ed25519, RSA-PSS, or ECDSA
- **Hash Functions**: SHA-256 for task hashing and Merkle trees
- **Key Distribution**: Secure distribution of ICP public keys to verifiers

### Performance Considerations
- **Signature Verification**: Optimize for high-throughput verification
- **Receipt Size**: Balance between completeness and network overhead
- **Caching**: Cache verified receipts to reduce repeated verification
- **Batch Processing**: Support for bulk receipt validation

### Integration Points
- **IAM Systems**: Integrate with existing identity providers
- **Monitoring**: Real-time receipt validation and alerting
- **Compliance**: Automated policy checking and reporting
- **Incident Response**: Quick receipt invalidation and investigation
