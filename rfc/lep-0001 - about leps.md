# LEP-0001 : About LEPs

| Field          | Value            |
| -------------- | ---------------- |
| LEP            | 0001: About LEPs |
| Author         | Alex Oleshkevich |
| Type           | Informational    |
| Created        | 2025-11-01       |
| Depends on     |                  |
| Target Version | 0.1.0            |


## Summary

### LEP = Lunette Enhancement Proposal”
A formal design document that introduces, explains, or changes anything in the framework ecosystem.




## Motivation

LEP-0001 defines how LEPs are written, linked, approved, and evolved.
It is the root document that establishes the LEP lifecycle and dependency graph, ensuring every future LEP is consistent, traceable, and non-ambiguous. **LEPs are not blog posts.**
They are part of the project’s long-term architecture record.

## Specification or Vision

### LEP Types

| Type          | Description                                                        |
| ------------- | ------------------------------------------------------------------ |
| Informational | Records vision, philosophy, rationale (no implementation required) |
| Standards     | Track Defines something that must be implemented in code           |
| Process       | Defines rules for contributors, releases, governance               |
| Meta          | Changes or expands the LEP process itself                          |


### LEP structure
Every LEP must include header:

| Field          | Value            |
| -------------- | ---------------- |
| LEP            | 0001: About LEPs |
| Author         | Alex Oleshkevich |
| Type           | Informational    |
| Created        | 2025-11-01       |
| Depends on     |                  |
| Target Version | 0.1.0            |

Followed by sections:

1. Summary
2. Motivation
3. Specification or Vision
4. Rationale / Alternatives
5. Backwards Compatibility
6. Security Considerations (if applicable)
7. Open Questions
8. Appendix / Diagrams (optional)

Empty sections can be omitted.


### LEP lifecycle

LEPs created as a regular PRs. Once merged, it is a subject for implementation.
