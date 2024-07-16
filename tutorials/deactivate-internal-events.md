# Deactivate internal events

As a tenant maintainer you can decide to temporarily disable the execution of internal events. This makes sense when restoring a CED backup. These rules should exist for the shortest time possible.

## Create internal events deactivation rules

You can create deactivation rules by manually pushing documents to `/internal-events-deactivation-rules` path in Firestore.

## Types of deactivation rules

### Organization

Deactivates internal events within an organization.

```typescript
{
  type: "organization",
  organization: string | "*"
}
```

### Project

Deactivates internal events within a project.

```typescript
{
  type: "project",
  organization: string | "*",
  projectId: string | "*"
}
```

### Agents maintenance

Deactivates agents maintenance events. This applies to the whole tenant.

```typescript
{
  type: 'agents';
}
```

### AgentsManager maintenance

Deactivates agents managers maintenance events. This applies to the whole tenant.

```typescript
{
  type: 'agents-manager';
}
```
