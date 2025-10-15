- [ ] T015 Setup frontend API request wrapper in frontend/utils/api.js

### SQL Query Modules (Core Infrastructure)

- [ ] T016a [P] Create SQL query module base class in backend/app/core/sql_queries/__init__.py
- [ ] T016b [P] Create employee SQL queries in backend/app/core/sql_queries/employee.py
- [ ] T016c [P] Create department SQL queries in backend/app/core/sql_queries/department.py
- [ ] T016d [P] Create authentication SQL queries in backend/app/core/sql_queries/auth.py
- [ ] T016e [P] Create role SQL queries in backend/app/core/sql_queries/role.py

### Audit Logging Framework (Security Infrastructure)

- [ ] T016f [P] Create AuditLog model in backend/app/models/audit_log.py
- [ ] T016g [P] Create AuditLog schema in backend/app/schemas/audit_log.py
- [ ] T016h Implement audit logging service in backend/app/services/audit_service.py
- [ ] T016i Create audit logging middleware in backend/app/api/deps.py (audit_dependency)
- [ ] T016j [P] Create audit SQL queries in backend/app/core/sql_queries/audit.py

---

## Phase 3.5: Role-Based Access Control (RBAC) - Critical Security Feature

**Goal**: Implement role-based access control system to satisfy FR-005 security requirement

**Independent Test**: Can be fully tested by creating roles, assigning permissions, and verifying access control enforcement

### Tests for RBAC (OPTIONAL - only if tests requested) ⚠️

- [ ] T031a [P] [RBAC] Contract test for GET /api/v1/roles in backend/tests/test_roles.py
- [ ] T031b [P] [RBAC] Contract test for POST /api/v1/roles in backend/tests/test_roles.py

### Implementation for RBAC

- [ ] T031c [P] [RBAC] Create Role model in backend/app/models/role.py
- [ ] T031d [P] [RBAC] Create Permission model in backend/app/models/role.py
- [ ] T031e [P] [RBAC] Create Role schema in backend/app/schemas/role.py
- [ ] T031f [RBAC] Implement role service in backend/app/services/role_service.py
- [ ] T031g [RBAC] Implement GET roles endpoint in backend/app/api/v1/roles.py
- [ ] T031h [RBAC] Implement POST/PUT/DELETE role endpoints in backend/app/api/v1/roles.py
- [ ] T031i [RBAC] Add role-based authorization middleware in backend/app/api/deps.py
- [ ] T031j [P] [RBAC] Create role management UI in frontend/pages/roles/

**Checkpoint**: RBAC system should be fully functional and enforce access control

### Dashboard Backend APIs

- [ ] T071a Implement GET dashboard statistics endpoint in backend/app/api/v1/dashboard.py
- [ ] T071b Implement GET recent activities endpoint in backend/app/api/v1/dashboard.py
- [ ] T071c Implement GET quick actions endpoint in backend/app/api/v1/dashboard.py

### Audit Logging Integration

- [ ] T078a Integrate audit logging into authentication endpoints
- [ ] T078b Integrate audit logging into user management endpoints
- [ ] T078c Integrate audit logging into department management endpoints
- [ ] T078d Create audit log viewer endpoint in backend/app/api/v1/audit.py
- [ ] T078e Create audit log viewer UI in frontend/pages/audit/

### Edge Case Handling (from spec.md)

- [ ] T080 Handle deactivated employee account login attempts in backend/app/services/auth_service.py
- [ ] T081 Implement concurrent login session management in backend/app/services/auth_service.py
- [ ] T082 Add database connection failure handling in backend/app/core/database.py
- [ ] T083 Implement comprehensive input validation for employee creation in backend/app/services/user_service.py
- [ ] T084 Handle session expiration during form submission in frontend/utils/auth.js

In the "Dependencies & Execution Order" section, update "User Story Dependencies" to include RBAC:

- **RBAC (Phase 3.5)**: Must complete after Foundational (Phase 2) and before User Stories that require authorization
- **User Story 1 (P1)**: Can start after Foundational (Phase 2) - No dependencies on other stories
- **User Story 2 (P1)**: Should start after RBAC (Phase 3.5) for proper access control
- **User Story 3 (P2)**: Should start after RBAC (Phase 3.5) for proper access control

