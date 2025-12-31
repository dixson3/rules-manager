# Rules Manager Plugin

A Claude Code plugin for managing project rules. Browse, install, validate, and remove rules from a curated collection.

## Installation

### From GitHub

```bash
# Add the marketplace
claude plugin marketplace add dixson3/rules-manager

# Install the plugin
claude plugin install rules-manager@dixson3/rules-manager
```

### Local Development

```bash
claude --plugin-dir /path/to/rules-manager
```

## Usage

```bash
# Interactive mode - guided rule management
/rules-manager:rules

# List all available rules
/rules-manager:rules list

# Add a rule to your project
/rules-manager:rules add beads-workflow

# Remove a rule from your project
/rules-manager:rules remove edd

# Validate installed rules for conflicts
/rules-manager:rules validate

# Show current installation status
/rules-manager:rules status
```

## Available Rules

| Rule ID | Domain | Description |
|---------|--------|-------------|
| `beads-workflow` | task-management | Multi-session task tracking with dependency graphs |
| `edd` | requirements | Design decisions and implementation guides (HOW to build) |
| `prd-workflow` | requirements | High-level product requirements (WHAT to build) |

### Rule Compatibility

- **prd-workflow** and **edd** are complementary - use both together:
  - PRD defines WHAT to build (product requirements, constraints)
  - EDD defines HOW to build (design decisions, patterns, NFRs)
- **beads-workflow** complements both for task tracking

### Recommended Combinations

1. **Complete Workflow** - Beads + PRD + EDD (full requirements and design)
2. **Product Development** - Beads + PRD (task management with product requirements)
3. **Engineering Focus** - Beads + EDD (task management with design decisions)

## How It Works

When you run `/rules-manager:rules add <rule-id>`, the plugin:

1. Looks up the rule in the bundled collection
2. Copies it to your project's `.claude/rules/` directory
3. Shows complementary rules you might want to add
4. Warns if you're installing conflicting rules

Rules installed to `.claude/rules/` are automatically loaded by Claude Code.

## Contributing

### Adding a New Rule

1. Create `collection/<domain>/<RuleName>.md` with frontmatter:

```yaml
---
id: my-rule-id
version: 1.0.0
name: Human Readable Name
description: Brief description (< 160 chars)
domain: task-management
author: your-github-username
tags: [relevant, tags]
relationship:
  complements: []
  replaces: []
---

# Rule Title

Your rule content here...
```

2. Add an entry to `catalog.yaml`
3. Test with `/rules-manager:rules list`

### Domain Taxonomy

| Domain | Description |
|--------|-------------|
| `task-management` | Work tracking, issues, sprints |
| `requirements` | PRDs, design docs, specifications |
| `code-quality` | Style, patterns, architecture |
| `version-control` | Git workflows, branching |
| `testing` | Test strategy, coverage |
| `documentation` | READMEs, API docs |
| `security` | Auth, secrets, OWASP |
| `deployment` | CI/CD, releases |

## License

MIT License - see [LICENSE](LICENSE) for details.
