---
id: edd
version: 1.0.0
name: Engineering Design Document Rules
description: Design decisions, implementation guides, and architectural patterns using docs/DESIGN.md
domain: requirements
author: dixson3
tags: [design, architecture, implementation, patterns, nfr]
relationship:
  complements:
    - beads-workflow
    - prd-workflow
activation:
  triggers:
    - "docs/DESIGN.md exists"
    - "user mentions design decisions, architecture, or implementation patterns"
  contexts:
    - implementation-planning
    - architecture-decisions
---

# Engineering Design Document Rules

This project tracks design decisions and implementation guides in `docs/DESIGN.md`. Use it for architectural decisions, non-functional requirements, and implementation patterns.

## Scope & Relationship with PRD

**EDD focuses on HOW:**
- Architectural decisions and rationale (DD-xxx IDs)
- Non-functional requirements: performance, security, scalability (NFR-xxx IDs)
- Implementation patterns and conventions
- Technology choices and trade-offs

**PRD focuses on WHAT and WHY (see `docs/PRD.md`):**
- Product goals and business objectives
- User-facing functional requirements (REQ-xxx IDs)
- Technical constraints and boundaries

When both documents exist, PRD defines *what* to build, while EDD guides *how* to build it.

## Activation Context

- `docs/DESIGN.md` file exists
- User mentions: "design", "architecture", "implementation", "patterns", "NFR"
- Implementation approach needs to be decided
- Design decisions need documentation

## Core Responsibilities

### 0. Design Documentation

- Document architectural decisions in `docs/DESIGN.md` before implementation
- Record non-functional requirements and how they'll be achieved
- Capture implementation patterns and conventions

### 1. Design Loading

- **Always read docs/DESIGN.md first** when starting implementation
- Parse and understand all design sections:
  - Non-Functional Requirements (performance, security, scalability)
  - Design Decisions (architectural choices and rationale)
  - Implementation Guides (patterns, conventions, examples)

### 2. Design Validation

Before implementing any change, validate against docs/DESIGN.md:

```markdown
## Pre-Implementation Checklist

- [ ] Does this follow established Design Decisions?
- [ ] Does this satisfy relevant Non-Functional Requirements?
- [ ] Is this consistent with implementation patterns?
- [ ] Are there conflicting design decisions?
- [ ] Does the PRD requirement (REQ-xxx) align with this approach?
```

### 3. Design Traceability

- Link design decisions to PRD requirements they support
- Track which NFRs are addressed by which patterns
- Identify implementation gaps
- Flag deviations from established patterns

### 4. Design Evolution

When design needs change or new insights emerge:

- Propose updates to docs/DESIGN.md
- Document new design decisions with rationale
- Update implementation guides as patterns evolve
- Flag breaking changes that affect existing code

## DESIGN.md Structure Enforcement

Ensure docs/DESIGN.md maintains this structure:

```markdown
# Engineering Design Document

## Overview

[Brief architectural overview and design philosophy]

- Key architectural patterns used
- Technology stack decisions
- Integration points

## Non-Functional Requirements

[How the system must perform - with measurable criteria]

- NFR-001: [Requirement with acceptance criteria]
- NFR-002: [Requirement with acceptance criteria]
  [Performance, scalability, security, maintainability]

## Design Decisions

[Key architectural and implementation choices with rationale]

- DD-001: [Decision]
  - **Context:** Why this decision was needed
  - **Decision:** What was decided
  - **Rationale:** Why this approach over alternatives
  - **Consequences:** Trade-offs and implications

## Implementation Guides

[Patterns, conventions, and examples for common tasks]

### [Pattern Name]
- **When to use:** [Conditions]
- **Example:** [Code or pseudocode]
- **Related:** [DD-xxx, NFR-xxx]
```

## Design Analysis Commands

### Analyze Design Coverage

When asked to analyze design implementation:

1. Read docs/DESIGN.md
2. Scan implementation files
3. Generate coverage report:
   - Design decisions implemented
   - NFRs addressed
   - Patterns followed
   - Deviations from established patterns

### Validate Implementation Against Design

When reviewing code or planning implementation:

1. Identify which design decisions apply
2. Check alignment with NFRs
3. Verify implementation follows patterns
4. Ensure consistency with architectural choices
5. Report any conflicts or gaps

### Propose Design Updates

When suggesting docs/DESIGN.md updates:

1. Identify the type (NFR/DD/Implementation Guide)
2. Provide clear, measurable criteria
3. Include rationale and context
4. Note dependencies or conflicts with existing decisions
5. Suggest ID numbering (NFR-XXX, DD-XXX)

## Design Best Practices

### Writing Good NFRs

- **Specific**: Avoid vague terms like "fast" or "scalable"
- **Measurable**: Include concrete criteria (e.g., "< 100ms response time at p95")
- **Testable**: Define how to verify compliance
- **Traceable**: Link to design decisions that achieve them

### Non-Functional Requirements (NFR)

Focus on _how_ the system performs:

- Performance: "API responses < 200ms at 95th percentile"
- Scalability: "Support 10,000 concurrent users"
- Security: "All data encrypted at rest using AES-256"
- Maintainability: "Code coverage > 80%"
- Compatibility: "Support Python 3.9+"

### Design Decisions (DD)

Document _why_ choices were made using ADR format:

- **Context**: What prompted this decision?
- **Decision**: What was decided?
- **Rationale**: Why this over alternatives?
- **Consequences**: Trade-offs and implications

Example:
```
DD-001: Use PostgreSQL for primary data store
- Context: Need ACID compliance for financial transactions
- Decision: PostgreSQL over MongoDB
- Rationale: Strong consistency required, team expertise
- Consequences: Less flexible schema, requires migrations
```

## Conflict Detection

Watch for design conflicts:

- **Contradictory decisions**: DD-001 vs DD-005
- **NFR trade-offs**: Performance vs cost, security vs usability
- **Pattern violations**: Code that doesn't follow established patterns
- **Technical impossibility**: Decisions that can't coexist

When conflicts detected:

1. Flag the specific decisions in conflict
2. Explain the conflict clearly
3. Propose resolution options
4. Recommend updating docs/DESIGN.md

## Design Workflow Integration

### When Planning Work

1. Read docs/DESIGN.md to understand architectural context
2. Read docs/PRD.md to understand product requirements
3. Identify which design decisions and NFRs apply
4. Verify approach is consistent with established patterns

### During Implementation

1. Follow established design patterns
2. Ensure code satisfies NFR criteria
3. Add comments linking code to DD-xxx or NFR-xxx IDs
4. Write tests that validate NFR compliance

### After Implementation

1. Verify NFRs are satisfied
2. Update docs/DESIGN.md if new patterns emerged
3. Document any new design decisions made

## Documentation Quality Checks

Regularly verify docs/DESIGN.md quality:

- [ ] All design decisions have rationale
- [ ] NFRs have measurable criteria
- [ ] Implementation guides are current
- [ ] Patterns are consistently applied
- [ ] No contradictory decisions
- [ ] IDs are sequential and unique

## Example Statements

**Good Non-Functional Requirement:**

```
NFR-001: All API endpoints must respond within 200ms at the 95th
percentile under load of 1000 concurrent requests.
```

**Good Design Decision:**

```
DD-001: Using Redis for session storage
- Context: NFR-001 requires <200ms response times
- Decision: Redis over database-backed sessions
- Rationale: Benchmarks showed database sessions added 150ms
  overhead while Redis added only 5ms
- Consequences: Additional infrastructure dependency, requires
  Redis cluster for HA
```

**Good Implementation Guide:**

```
## Error Handling Pattern
- When to use: All API endpoints
- Pattern: Return structured error responses with codes
- Example: { "error": { "code": "AUTH_FAILED", "message": "..." } }
- Related: DD-003 (API design), NFR-002 (observability)
```

## Integration with Other Rules

This rule works alongside:

- **prd-workflow**: PRD defines WHAT to build, EDD defines HOW
- **beads-workflow**: Track design decisions as tasks when needed
- **Testing frameworks**: Ensure tests validate NFR compliance

## Quick Reference

```bash
# When starting work
1. Read docs/PRD.md (what to build)
2. Read docs/DESIGN.md (how to build)
3. Identify applicable patterns

# During implementation
1. Follow established patterns
2. Satisfy NFR criteria
3. Update docs/DESIGN.md if needed

# After implementation
1. Verify NFR compliance
2. Document new patterns
3. Link code to design decisions
```

## Error Prevention

Prevent common mistakes:

- ❌ Ignoring established design patterns
- ❌ Missing NFR compliance
- ❌ Making design decisions without documentation
- ❌ Leaving docs/DESIGN.md outdated
- ✅ Always validate against docs/DESIGN.md first
- ✅ Document decisions as you make them
- ✅ Keep requirements and implementation synchronized
