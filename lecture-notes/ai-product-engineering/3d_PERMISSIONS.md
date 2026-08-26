# Roles & Permissions

## REEBOK (Progressive Role-Based Access Control)

```ts
const users = [
  { id: 1, name: "Alice", role_id: 1 },
  { id: 2, name: "Bob", role_id: 2 },
];

const userRoles = [
  { id: 1, name: "Alice", role_id: 1 },
  { id: 2, name: "Bob", role_id: 2 },
];

const roles = [
  { id: 1, name: "Admin" },
  { id: 2, name: "Editor" },
];

const permissions = [
  { id: 1, name: "create_post" },
  { id: 2, name: "delete_post" },
  { id: 3, name: "edit_post" },
];

const rolePermissions = [
  { role_id: 1, permission_id: 1 },
  { role_id: 1, permission_id: 2 },
  { role_id: 1, permission_id: 3 },
  { role_id: 2, permission_id: 1 },
  { role_id: 2, permission_id: 3 },
];
```

## RBAC (Role-Based Access Control)

- Access rights are assigned to roles, not directly to users.
- Users are assigned roles, and roles are assigned permissions.
- A user's effective permissions come from the role(s) they hold.

```ts
const users = [
  { id: 1, name: "Alice", role_id: 1 },
  { id: 2, name: "Bob", role_id: 2 },
];

const roles = [
  { id: 1, name: "Admin" },
  { id: 2, name: "Editor" },
];

const permissions = [
  { id: 1, name: "create_post" },
  { id: 2, name: "delete_post" },
  { id: 3, name: "edit_post" },
];

const rolePermissions = [
  { role_id: 1, permission_id: 1 },
  { role_id: 1, permission_id: 2 },
  { role_id: 1, permission_id: 3 },
  { role_id: 2, permission_id: 1 },
  { role_id: 2, permission_id: 3 },
];
```

## ABAC (Attribute-Based Access Control)

Access decisions are based on attributes of the user, resource, action, and environment, evaluated against rules at request time.

```ts
const users = [
  { id: 1, name: "Alice", department: "Finance", clearance: "high" },
  { id: 2, name: "Bob", department: "Sales", clearance: "low" },
];

const resources = [
  { id: 1, name: "Budget Report", department: "Finance", sensitivity: "high" },
  { id: 2, name: "Sales Deck", department: "Sales", sensitivity: "low" },
];

const rules = [
  {
    id: 1,
    description:
      "User can access resource if same department and clearance >= sensitivity",
  },
];
```

## ACL (Access Control List)

Permissions are attached directly to each resource, listing which users (or groups) can perform which actions on it.

```ts
const resources = [
  {
    id: 1,
    name: "Budget Report",
    acl: [
      { user_id: 1, permissions: ["read", "write"] },
      { user_id: 2, permissions: ["read"] },
    ],
  },
];
```

## PBAC (Policy-Based Access Control)

Access is governed by centrally defined policies (often rule/condition based) that are evaluated to allow or deny an action.

```ts
const policies = [
  {
    id: 1,
    name: "AllowFinanceReadDuringBusinessHours",
    effect: "allow",
    action: "read",
    resource: "Budget Report",
    condition: "user.department === 'Finance' && time.isBusinessHours",
  },
];

const users = [{ id: 1, name: "Alice", department: "Finance" }];
```

## ReBAC (Relationship-Based Access Control)

Access is determined by the relationship between the user and the resource (e.g. owner, member, friend), rather than roles or static attributes.

```ts
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
];

const documents = [{ id: 1, name: "Design Doc", owner_id: 1 }];

const relationships = [{ user_id: 2, resource_id: 1, relation: "editor" }];
```

## DAC (Discretionary Access Control)

The resource owner decides who else can access it and what they can do, permissions can be granted or revoked at the owner's discretion.

```ts
const documents = [{ id: 1, name: "Design Doc", owner_id: 1 }];

const grants = [
  { document_id: 1, granted_by: 1, granted_to: 2, permission: "read" },
];
```

## MAC (Mandatory Access Control)

Access is enforced by a central authority using fixed security labels (e.g. classification levels), users cannot change permissions themselves.

```ts
const users = [
  { id: 1, name: "Alice", clearance: "Secret" },
  { id: 2, name: "Bob", clearance: "Confidential" },
];

const documents = [
  { id: 1, name: "Top Secret Plan", classification: "Secret" },
  { id: 2, name: "Internal Memo", classification: "Confidential" },
];

// Rule: user.clearance level must be >= document.classification level
```

## Claims-based Access Control

A trusted identity provider issues claims (key-value assertions about the user) inside a token, and the app authorizes based on those claims.

```ts
const token = {
  sub: "user-1",
  claims: [
    { type: "role", value: "Admin" },
    { type: "department", value: "Finance" },
    { type: "email_verified", value: "true" },
  ],
};

// Authorization check example:
// allow if token.claims.some(c => c.type === "role" && c.value === "Admin")
```

## Scope-based Access Control (OAuth scopes)

Access tokens carry scopes representing the specific actions/resources a client is allowed to use on behalf of the user.

```ts
const accessToken = {
  user_id: 1,
  client_id: "mobile-app",
  scopes: ["posts:read", "posts:write", "profile:read"],
};

// Authorization check example:
// allow if accessToken.scopes.includes("posts:write")
```

## Permission Bitmasking

Each permission is a bit flag; a user's permissions are combined into a single integer using bitwise OR, and checked using bitwise AND.

```ts
const PERMISSIONS = {
  READ: 1 << 0, // 0001 = 1
  WRITE: 1 << 1, // 0010 = 2
  DELETE: 1 << 2, // 0100 = 4
  ADMIN: 1 << 3, // 1000 = 8
};

const users = [
  { id: 1, name: "Alice", permissions: PERMISSIONS.READ | PERMISSIONS.WRITE }, // 3
  { id: 2, name: "Bob", permissions: PERMISSIONS.READ }, // 1
];

// Check: (user.permissions & PERMISSIONS.WRITE) !== 0
```
