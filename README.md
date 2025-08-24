# From Permissions to Proof-of-Intent: One of the Missing Layers in Agentic IAM

> **The future of AI agent security isn't just about who can do what—it's about proving why they're doing it.**

## The Problem: Traditional IAM Falls Short for AI Agents

In traditional IAM, access is binary: who can do what. But when AI agents act on our behalf, that's no longer enough.

Agents don't just execute—they:

- **Chain workflows** across multiple systems
- **Spawn sub-agents** dynamically  
- **Act at machine speed**, often without direct human oversight

That means we can't just ask:
"Does this agent have permission?"

We must also ask:
"Why is it doing this, right now, on whose behalf, and with what justification?"

## A Possible Solution: Proof-of-Intent (PoI)

That's where Proof-of-Intent (PoI) comes in.

With PoI, every privileged agent action carries a cryptographic intent receipt:

- **Initiator lineage**: who or what spawned the action (human, parent agent)
- **Declared objective**: task hash or explicit purpose  
- **Just-in-time capability**: scoped and time-boxed permissions with ICP signatures
- **Risk context**: sensitivity of data, anomaly scores, policy checks
- **Cryptographic attestations**: tamper-evident proof of authorization and agent lineage

## Why This Matters

- **Auditors** get cryptographic receipts, not vague logs
- **CISOs** get provable accountability at agent speed
- **Developers** get a safer way to let agents act autonomously without fear of "black box" abuse

Without Proof-of-Intent, AI agents are essentially ghost users.  
With it, we move from **blind trust to provable trust**.

## Current Status of the project: Starting Point

This repository represents the beginning of the Proof-of-Intent journey. We're starting with a concrete example (see JSON) to demonstrate the concept and gather feedback from the community.

### What We Have So Far

- **`poi_receipt_example.json`** - A sample Proof-of-Intent receipt showing the structure and fields we envision
- **`SCHEMA.md`** - Comprehensive schema documentation with field definitions and validation rules
- **Basic concept documentation** - This README explaining the vision and problem space

### What's Next

We're actively seeking input on:
- **Receipt structure** - Does the JSON format capture all necessary intent information?
- **Cryptographic approach** - What signing and verification methods make sense?
- **ICP signature coverage** - Does our agent lineage binding approach provide sufficient security?
- **Integration patterns** - How should PoI integrate with existing IAM systems?
- **Use case priorities** - Which agent scenarios should we tackle first?

## Explore the Concept

Start by examining the sample receipt:

```bash
# View the current example
cat poi_receipt_example.json
```

For detailed field explanations and validation rules, see [SCHEMA.md](SCHEMA.md).

This file demonstrates our initial thinking on what a Proof-of-Intent receipt should contain. We want your feedback on:

- **Missing fields** - What intent information are we not capturing?
- **Field definitions** - Are our field names and descriptions clear?
- **Data types** - Do the proposed data structures make sense?
- **Security model** - Does our ICP signature and agent lineage binding provide adequate protection?
- **Extensibility** - How can we make this format future-proof?

## We Need Your Feedback

This is an open exploration, and we want to hear from:

- **Security professionals** - Does this approach address real IAM gaps?
- **AI/ML engineers** - How would you integrate this with your agent systems?
- **DevOps teams** - What operational challenges do you foresee?
- **Compliance experts** - Does this provide the audit trail you need?

## How to Contribute Feedback

### GitHub Discussions
The best way to share your thoughts is through [GitHub Discussions](../../discussions):

- **General feedback** - Start a new discussion about the overall concept
- **Receipt structure** - Comment on specific fields or propose new ones
- **Use cases** - Share scenarios where PoI would be valuable
- **Technical questions** - Ask about implementation details or alternatives

### Contributing Guide
For detailed contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md). This includes:
- Code contribution workflow
- Documentation standards
- Testing requirements
- Community guidelines

### Community Standards
We're committed to a welcoming and inclusive community. Please review our [Code of Conduct](CODE_OF_CONDUCT.md) before participating.

### Issues
Found a specific problem or have a concrete suggestion? [Open an issue](../../issues):

- **Bug reports** - If something in our examples doesn't work
- **Feature requests** - For new capabilities or improvements
- **Documentation** - If something isn't clear or is missing

### Pull Requests
Ready to contribute code or examples? We welcome:

- **Improved examples** - Better receipt structures or use cases
- **Documentation** - Clarifications, tutorials, or integration guides
- **Prototype implementations** - Working code that demonstrates the concept

## Getting Started

### Prerequisites
- Basic understanding of IAM and cryptographic concepts
- Familiarity with JSON and API design
- Interest in AI agent security

### Quick Start
```bash
# Clone the repository
git clone <your-repo-url>
cd poi

# Examine the example
cat poi_receipt_example.json

# Start a discussion with your feedback
# Visit: https://github.com/yourusername/poi/discussions
```

## Architecture Vision

PoI operates at three key layers:

1. **Intent Declaration**: Agents declare their purpose before taking action
2. **Receipt Generation**: Cryptographic proof of intent is created and signed
3. **Verification & Audit**: Receipts can be verified and audited in real-time

## Security Features

### Cryptographic Binding
- **ICP Signatures**: Identity Control Plane cryptographically signs capability grants
- **Agent Lineage Binding**: Signatures bind capabilities to specific agent chains
- **Tamper Detection**: Any modification invalidates cryptographic signatures
- **Temporal Security**: Expiration times prevent replay attacks

### Audit & Compliance
- **Immutable Receipts**: Cryptographic proof of what was authorized
- **Agent Accountability**: Clear chain of responsibility for actions
- **Policy Enforcement**: Risk context and compliance signals
- **Verifiable Authorization**: Cryptographic proof of capability grants

## Development Status

- **Phase 1**: Concept exploration and community feedback ✅
- **Phase 2**: Specification development and validation (Planned)
- **Phase 3**: Reference implementation and testing (planned)
- **Phase 4**: Integration examples and production readiness (planned)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

Thanks to all contributors who are helping build a more trustworthy AI future. See the [AUTHORS](AUTHORS) file for a complete list of contributors and how to add your name.

---

**Ready to help shape the future of AI agent security?** 

1. **Examine** the sample receipt
2. **Share** your feedback via [GitHub Discussions](../../discussions)
3. **Join** the conversation about building provable trust

This is just the beginning—your input will shape where we go next!
