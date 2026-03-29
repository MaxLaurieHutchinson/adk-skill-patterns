# ADK Skill Patterns 🧩

[![ClawHub](https://img.shields.io/badge/ClawHub-adk--skill--patterns-blue)](https://clawhub.ai/skills/adk-skill-patterns)
[![Version](https://img.shields.io/badge/version-1.0.0-green)](https://github.com/MaxLaurieHutchinson/adk-skill-patterns/releases)
[![License](https://img.shields.io/badge/license-MIT-yellow)](LICENSE)

> 5 proven agent skill design patterns from Google's Agent Development Kit (ADK), adapted for the OpenClaw ecosystem.

The ADK specification explains how to **package** a skill, but offers zero guidance on how to **structure the logic inside it**. These 5 patterns solve that problem.

---

## 🎯 The 5 Patterns

| Pattern | Question It Answers | Use When |
|---------|---------------------|----------|
| **🔧 Tool Wrapper** | "How do I make my agent an expert on a specific library?" | Agent needs deep, contextual knowledge about a technology |
| **📄 Generator** | "How do I enforce consistent output structure?" | Output format must be predictable every time |
| **✅ Reviewer** | "How do I separate what to check from how to check it?" | Code review, quality gates, compliance checking |
| **🎤 Inversion** | "How do I stop the agent from guessing and gather requirements first?" | Complex tasks requiring full context before execution |
| **🔄 Pipeline** | "How do I enforce a strict multi-step workflow?" | Multi-phase tasks with checkpoints and approvals |

---

## 🚀 Quick Start

### Install via ClawHub
```bash
clawhub install adk-skill-patterns
```

### Use in OpenClaw
```
"Use the Tool Wrapper pattern to create a FastAPI expert skill"
"Apply the Pipeline pattern to my documentation workflow"
"Which pattern should I use for code review?"
```

---

## 📖 Pattern Details

### 1. Tool Wrapper
**Purpose:** Give your agent on-demand context for a specific library/framework.

**Mechanism:**
- Listens for library keywords in prompts
- Dynamically loads documentation from `references/`
- Applies conventions as absolute truth only when needed

**Example:** FastAPI conventions that load only when FastAPI is mentioned

```yaml
# SKILL.md
metadata:
  pattern: tool-wrapper
  domain: fastapi
```

---

### 2. Generator
**Purpose:** Enforce consistent output via fill-in-the-blank orchestration.

**Mechanism:**
- `assets/` holds output template
- `references/` holds style guide
- Instructions act as project manager
- Asks for missing variables before generating

**Example:** Standardized technical reports that follow exact structure every time

```yaml
# SKILL.md
metadata:
  pattern: generator
  output-format: markdown
```

---

### 3. Reviewer
**Purpose:** Separate review criteria from review execution.

**Mechanism:**
- Stores modular rubric in `references/review-checklist.md`
- Methodically scores submissions
- Groups findings by severity
- Swap checklist = completely different audit

**Example:** PR reviews, security scans, compliance audits

```yaml
# SKILL.md
metadata:
  pattern: reviewer
  severity-levels: error, warning, info
```

---

### 4. Inversion
**Purpose:** Stop agents from guessing — make them interview first.

**Mechanism:**
- Agent acts as interviewer, not executor
- Structured questions in phases
- Hard gates prevent premature synthesis
- User drives through answers, not prompts

**Example:** Project planning, requirements gathering, system design

```yaml
# SKILL.md
metadata:
  pattern: inversion
  interaction: multi-turn
```

---

### 5. Pipeline
**Purpose:** Enforce strict sequential workflow with hard checkpoints.

**Mechanism:**
- Instructions = workflow definition
- Diamond gate conditions (user approval required)
- Cannot bypass steps or present unvalidated results
- Progressive disclosure keeps context clean

**Example:** Documentation generation, multi-step code workflows

```yaml
# SKILL.md
metadata:
  pattern: pipeline
  steps: "4"
```

---

## 🧬 Pattern Composition

These patterns are **not mutually exclusive** — they compose:

| Combination | Effect |
|-------------|--------|
| **Pipeline + Reviewer** | Multi-step workflow with quality gate at the end |
| **Generator + Inversion** | Gather variables via interview, then fill template |
| **Pipeline + Tool Wrapper** | Each step loads specific expertise as needed |
| **Reviewer + Generator** | Review output before generating final document |

**Principle:** Your agent only spends context tokens on the exact patterns it needs at runtime.

---

## 🗺️ Decision Tree

```
START: What does your skill need to do?
│
├─→ Provide deep knowledge about a specific library/framework?
│   └─→ Use: TOOL WRAPPER
│
├─→ Produce consistent, templated output?
│   └─→ Use: GENERATOR
│
├─→ Check/audit something against criteria?
│   └─→ Use: REVIEWER
│
├─→ Gather requirements before acting?
│   └─→ Use: INVERSION
│
├─→ Execute strict multi-step workflow?
│   └─→ Use: PIPELINE
│
└─→ Multiple of the above?
    └─→ Patterns COMPOSE
```

---

## 📁 Repository Structure

```
adk-skill-patterns/
├── SKILL.md                              # Main skill documentation
├── README.md                             # This file
├── LICENSE                               # MIT License
├── CONTRIBUTING.md                       # Contribution guidelines
├── templates/                            # Ready-to-use SKILL.md templates
│   ├── tool-wrapper-SKILL.md
│   ├── generator-SKILL.md
│   ├── reviewer-SKILL.md
│   ├── inversion-SKILL.md
│   └── pipeline-SKILL.md
└── references/                           # Quick reference guides
    └── pattern-selection-checklist.md
```

---

## 🛠️ Creating a New Skill

1. **Choose a pattern** using the decision tree above
2. **Copy the template** from `templates/`
3. **Customize** the metadata and instructions
4. **Add references/assets** as needed
5. **Test** with real use cases
6. **Publish** to ClawHub

---

## 🎓 Best Practices

### Do ✅
- Use **Tool Wrapper** for domain-specific expertise
- Use **Generator** for any templated output
- Use **Reviewer** for quality gates
- Use **Inversion** for complex planning tasks
- Use **Pipeline** for multi-phase workflows
- **Compose patterns** for complex needs
- Keep `references/` modular and swappable

### Don't ❌
- Cram everything into system prompts (use Tool Wrapper)
- Accept inconsistent output (use Generator)
- Hardcode review criteria (use Reviewer)
- Let agents assume context (use Inversion)
- Allow skipped steps (use Pipeline)

---

## 📚 Resources

- **Source Article:** [Google Cloud Tech on X](https://x.com/GoogleCloudTech/status/2033953579824758855)
- **ADK Documentation:** [Google Agent Development Kit](https://google.github.io/adk-docs/)
- **ClawHub Page:** [adk-skill-patterns](https://clawhub.ai/skills/adk-skill-patterns)

---

## 🤝 Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Ideas for contributions
- Additional pattern examples
- Real-world case studies
- Pattern compositions for common workflows
- Templates for other frameworks

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- Original patterns from [Google Cloud Tech](https://x.com/GoogleCloudTech)
- Adapted for [OpenClaw](https://openclaw.ai) by [Max Laurie Hutchinson](https://github.com/MaxLaurieHutchinson)

---

**Build smarter agents. Use patterns, not prompts.** 🧩
