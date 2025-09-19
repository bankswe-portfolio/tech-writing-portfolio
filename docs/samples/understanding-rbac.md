# Understanding RBAC

Role-Based Access Control (RBAC) assigns permissions to **roles**, not individuals. Users inherit permissions by the roles they hold.

## Why it matters
- Reduces permission sprawl
- Centralizes policy changes
- Auditable and easier to reason about

## Core concepts
- **User**: an identity
- **Role**: a named set of permissions
- **Permission**: an allowed action on a resource
- **Assignment**: user ↔ role mapping

## Common pitfalls
- Too many bespoke roles
- Granting roles directly to service accounts without review
