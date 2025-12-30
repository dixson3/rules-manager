# Rules Management Plugin

A Claude Code plugin for managing project rules. Browse, install, validate, and remove rules from a curated collection.

## Installation

### From GitHub

```bash
# Add the marketplace
claude plugin marketplace add dixson3/rules-management

# Install the plugin
claude plugin install rules-management@dixson3/rules-management
```

### Local Development

```bash
claude --plugin-dir /path/to/rules-management
```

## Usage

```bash
# Interactive mode - guided rule management
/rules-management:rules

# List all available rules
/rules-management:rules list

# Add a rule to your project
/rules-management:rules add beads-workflow

# Remove a rule from your project
/rules-management:rules remove design-spec

# Validate installed rules for conflicts
/rules-management:rules validate

# Show current installation status
/rules-management:rules status
```

## Available Rules

| Rule ID | Domain | Description |
|---------|--------|-------------|
| `beads-workflow` | task-management | Multi-session task tracking with dependency graphs |
| `design-spec` | requirements | Requirements tracking using DESIGN.md |
| `prd-workflow` | requirements | Spec-driven development using docs/PRD.md |

### Rule Compatibility

- **beads-workflow** works with either `design-spec` or `prd-workflow`
- **design-spec** and **prd-workflow** are alternatives - choose one

### Recommended Combinations

1. **Beads + Design Spec** - Task management with design specification tracking
2. **Beads + PRD** - Task management with PRD-driven development

## How It Works

When you run `/rules-management:rules add <rule-id>`, the plugin:

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
3. Test with `/rules-management:rules list`

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
