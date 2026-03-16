# ARCHITECTURE.md — [Project Name]

> Claude reads this before writing any DB query, auth logic, middleware, or
> access control. Keep it accurate — stale info here causes real bugs.

---

## Data Models

<!-- FILL IN: one section per model -->
<!-- Include: key fields, types, relationships, any virtual fields or hooks -->

### [ModelName]
```
field       type        notes
-------     --------    ------
<!-- e.g. _id        ObjectId    auto -->
<!-- e.g. email      String      unique, indexed -->
<!-- e.g. role       enum        admin | manager | employee -->
```
Relationships:
<!-- FILL IN: e.g. "belongs to Tenant via tenantId", "has many Tasks" -->

---

## Auth Strategy

<!-- FILL IN: how auth works end to end -->

**Method:** <!-- e.g. JWT / sessions / OAuth -->

**Flow:**
1. <!-- e.g. User submits email + password to POST /auth/login -->
2. <!-- e.g. Server verifies hash, signs JWT with userId + role -->
3. <!-- e.g. Client stores token in localStorage / httpOnly cookie -->
4. <!-- e.g. Every request sends token in Authorization: Bearer header -->
5. <!-- e.g. Auth middleware verifies token, attaches user to req.user -->

**Token:**
- Expiry: <!-- FILL IN: e.g. 7d -->
- Payload: <!-- FILL IN: e.g. userId, role, tenantId -->
- Secret: <!-- stored in: process.env.JWT_SECRET -->

**Middleware chain:**
<!-- FILL IN: e.g. verifyToken → attachUser → checkRole → handler -->

---

## Access Control

<!-- FILL IN: who can do what -->
<!-- Add or remove roles to match your app -->

| Action                  | Admin | Manager | Employee |
|-------------------------|-------|---------|----------|
| <!-- FILL IN action --> | ✅    | ❌      | ❌       |
| <!-- FILL IN action --> | ✅    | ✅      | ❌       |
| <!-- FILL IN action --> | ✅    | ✅      | ✅       |

**Rules:**
<!-- FILL IN: any non-obvious access control logic -->
<!-- e.g. "Managers can only access instances within their tenantId" -->
<!-- e.g. "Employees can only update their own task completions" -->

---

## Service Boundaries

<!-- FILL IN: what each service owns and must not cross -->

### [ServiceName]
- **Owns:** <!-- e.g. email composition, delivery, retry logic -->
- **Does not:** <!-- e.g. never reads from DB directly — receives data as args -->
- **Called by:** <!-- e.g. schedulerService, reminderController -->

<!-- Repeat per service -->

---

## API Structure

**Base URL:** `<!-- FILL IN: e.g. /api/v1 -->`

| Method | Route                        | Auth | Description              |
|--------|------------------------------|------|--------------------------|
| POST   | <!-- FILL IN: e.g. /auth/login --> | ❌ | <!-- description --> |
| GET    | <!-- FILL IN -->             | ✅   | <!-- description -->     |

<!-- Add all routes. Claude uses this to avoid creating duplicate endpoints -->

---

## Database Conventions

**DB:** <!-- FILL IN: e.g. MongoDB Atlas via Mongoose / PostgreSQL via Prisma -->

- **Naming:** <!-- e.g. camelCase fields, PascalCase model names -->
- **Timestamps:** <!-- e.g. all models include createdAt / updatedAt via { timestamps: true } -->
- **Soft deletes:** <!-- e.g. use isDeleted: Boolean flag — never hard delete -->
- **Indexes:** <!-- e.g. index on email, tenantId on all tenant-scoped models -->
- **Multi-tenancy:** <!-- e.g. every query must scope by tenantId — never query globally -->

---

## Multi-Tenancy (if applicable)

<!-- DELETE this section if not applicable -->

- **Isolation strategy:** <!-- e.g. shared DB, tenant scoped by tenantId field -->
- **Rule:** every DB query must include a `tenantId` filter — no exceptions
- **Enforced at:** <!-- e.g. service layer, never assumed at controller -->

---

## Error Handling

<!-- FILL IN: how errors are structured and returned -->

**Format:**
```json
{
  "success": false,
  "message": "Human readable message",
  "code": "ERROR_CODE"
}
```

**HTTP codes used:**
- `400` — <!-- e.g. validation errors -->
- `401` — <!-- e.g. missing or invalid token -->
- `403` — <!-- e.g. insufficient role -->
- `404` — <!-- e.g. resource not found -->
- `500` — <!-- e.g. unhandled server error -->

---

## Environment Variables

<!-- FILL IN: all vars Claude needs to know exist — no values, just names and purpose -->

| Variable              | Purpose                          |
|-----------------------|----------------------------------|
| `JWT_SECRET`          | <!-- e.g. signs and verifies tokens --> |
| `MONGODB_URI`         | <!-- e.g. Atlas connection string -->   |
| <!-- FILL IN -->      | <!-- purpose -->                        |

> Never hardcode these. Always reference via `process.env.VAR_NAME`.
```

---