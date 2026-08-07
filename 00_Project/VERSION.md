# VERSION

> DetectorAssistant Version Management Specification

Current Version: **v1.0.0**  
Release Status: **Release Candidate (RC)**  
Last Updated: 2026-08-07

---

# 1. Purpose

This document defines the version management strategy for DetectorAssistant.

Version management ensures:

- Controlled project evolution
- Traceable document changes
- Backward compatibility
- Consistent release process
- Clear maintenance history

---

# 2. Version Format

DetectorAssistant follows Semantic Versioning.

```
Major.Minor.Patch
```

Example:

```
v1.2.3
```

Meaning:

| Component | Description |
|----------|-------------|
| Major | Architecture or incompatible changes |
| Minor | New modules or significant feature additions |
| Patch | Documentation fixes, corrections, small improvements |

---

# 3. Major Version

Major versions indicate significant architectural evolution.

Examples:

- Directory restructuring
- Knowledge model redesign
- Major document reorganization
- Breaking compatibility

Examples:

```
v1.0.0
v2.0.0
v3.0.0
```

---

# 4. Minor Version

Minor versions indicate functional expansion while maintaining compatibility.

Examples:

- New detector products
- Additional SOPs
- New FailureKnowledge
- New Case documents
- New SDK documentation

Examples:

```
v1.1.0
v1.2.0
v1.3.0
```

---

# 5. Patch Version

Patch versions indicate maintenance updates.

Examples:

- Typographical corrections
- Image replacement
- Cross-reference updates
- ErrorCode corrections
- Improved explanations

Examples:

```
v1.0.1
v1.0.2
v1.0.3
```

---

# 6. Release Levels

## Draft

Early development.

Characteristics:

- Content incomplete
- Internal use only
- Frequent changes

Example:

```
v0.5.0
```

---

## Beta

Feature-complete but under validation.

Characteristics:

- Internal testing
- Engineering review
- Structure stable

Example:

```
v0.9.0
```

---

## Release Candidate (RC)

Documentation substantially complete.

Characteristics:

- Ready for production validation
- Minor corrections only
- Architecture frozen

Example:

```
v1.0.0-rc1
```

---

## Release

Official published version.

Characteristics:

- Stable
- Production ready
- Controlled updates

Example:

```
v1.0.0
```

---

# 7. Current Version Status

| Item | Status |
|------|--------|
| Architecture | Complete |
| Knowledge Structure | Complete |
| SDK | Complete |
| Hardware | Nearly Complete |
| Software | In Progress |
| Calibration | Complete |
| Workflow | Complete |
| FailureKnowledge | Nearly Complete |
| DecisionTree | Complete |
| SOP | Complete |
| Case | Complete |
| ErrorCode | Complete |
| Template | Complete |
| Glossary | Complete |
| Reference | Partial |

---

# 8. Compatibility Policy

Minor and Patch updates should maintain compatibility with existing document links and directory structure.

Major versions may introduce structural changes.

Top-level directory names should remain stable unless a Major version is released.

---

# 9. Planned Versions

| Version | Planned Content | Status |
|----------|-----------------|--------|
| v1.0.0 | Core knowledge base | Current |
| v1.1.0 | Complete 04_Software and remaining Hardware/FailureKnowledge content | Planned |
| v1.2.0 | Expand supported detector product families | Planned |
| v1.3.0 | Enhance 15_Reference and engineering reference center | Planned |
| v2.0.0 | Next-generation knowledge architecture (if required) | Future |

---

# 10. Version Update Rules

Increase the version when:

### Major

- Architecture changes
- Breaking compatibility
- Directory restructuring

### Minor

- New functional modules
- New document collections
- Significant feature expansion

### Patch

- Bug fixes
- Documentation improvements
- Reference updates
- Formatting corrections

---

# 11. Version History

| Version | Date | Description |
|----------|------|-------------|
| v1.0.0 | 2026-08-07 | Initial complete knowledge base architecture established |

---

# Related Documents

- README.md
- ROADMAP.md
- CHANGELOG.md
- ProjectScope.md