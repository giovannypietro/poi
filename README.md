# 🔐 From Permissions to Proof-of-Intent: The Missing Layer in Agentic IAM

> **The future of AI agent security isn't just about who can do what—it's about proving why they're doing it.**

## 🚨 The Problem: Traditional IAM Falls Short for AI Agents

In traditional IAM, access is binary: who can do what. But when AI agents act on our behalf, that's no longer enough.

Agents don't just execute—they:

- **Chain workflows** across multiple systems
- **Spawn sub-agents** dynamically  
- **Act at machine speed**, often without direct human oversight

That means we can't just ask:
✅ "Does this agent have permission?"

We must also ask:
❓ "Why is it doing this, right now, on whose behalf, and with what justification?"

## 💡 The Solution: Proof-of-Intent (PoI)

That's where Proof-of-Intent (PoI) comes in.

With PoI, every privileged agent action carries a cryptographic intent receipt:

- **🔗 Initiator lineage**: who or what spawned the action (human, parent agent)
- **🎯 Declared objective**: task hash or explicit purpose  
- **⏳ Just-in-time capability**: scoped and time-boxed permissions
- **⚖️ Risk context**: sensitivity of data, anomaly scores, policy checks

## 🎯 Why This Matters

- **Auditors** get cryptographic receipts, not vague logs
- **CISOs** get provable accountability at agent speed
- **Developers** get a safer way to let agents act autonomously without fear of "black box" abuse

Without Proof-of-Intent, AI agents are essentially ghost users.  
With it, we move from **blind trust → provable trust**.

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Basic understanding of cryptographic signatures and IAM concepts

### Quick Start
```bash
# Clone the repository
git clone <your-repo-url>
cd poi

# Install dependencies
npm install

# Run the example
npm run example
```

### Explore the Concepts
- Check out `poi_receipt_example.json` to see what a PoI receipt looks like
- Review the core concepts in our documentation
- Try building your first intent receipt

## 🏗️ Architecture Overview

PoI operates at three key layers:

1. **Intent Declaration**: Agents declare their purpose before taking action
2. **Receipt Generation**: Cryptographic proof of intent is created and signed
3. **Verification & Audit**: Receipts can be verified and audited in real-time

## 🤝 How to Contribute

We're building the foundation for trustworthy AI agent interactions. Here's how you can help:

### 🐛 Report Issues
Found a bug or have a feature request? [Open an issue](../../issues) with:
- Clear description of the problem
- Steps to reproduce
- Expected vs actual behavior

### 💡 Propose Enhancements
Have ideas for improving PoI? We'd love to hear them:
- [Start a discussion](../../discussions) 
- [Submit a feature request](../../issues/new?template=feature_request.md)

### 🔧 Submit Code
Ready to contribute code? Here's our process:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### 📚 Improve Documentation
Help others understand PoI better:
- Fix typos or clarify explanations
- Add examples for common use cases
- Translate documentation to other languages

## 🧪 Development

### Running Tests
```bash
npm test
```

### Building
```bash
npm run build
```

### Code Style
We use Prettier and ESLint. Run before committing:
```bash
npm run lint
npm run format
```

## 📖 Documentation

- [Core Concepts](./docs/concepts.md)
- [API Reference](./docs/api.md)
- [Integration Guide](./docs/integration.md)
- [Security Model](./docs/security.md)

## 🔒 Security

This project addresses critical security challenges in AI agent interactions. If you discover a security vulnerability, please:

1. **Do not** open a public issue
2. **Email** security@yourdomain.com with details
3. **Wait** for our security team to respond

## 📄 License

[License details to be added]

## 🙏 Acknowledgments

Thanks to all contributors who are helping build a more trustworthy AI future.

---

**Ready to move from blind trust to provable trust?** [Get started](#getting-started) or [join the discussion](../../discussions)!
