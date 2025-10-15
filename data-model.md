# Data Model: HIS Subsystem

## Entity: Employee
- **employee_id** (String[10], Primary Key): Employee identifier
- **name** (String[50], Required): Employee's full name
- **department_id** (String[10], Foreign Key): Department association
- **position** (String[50]): Job title or position
- **email** (String[100]): Email address
- **phone** (String[20]): Phone number
- **hire_date** (Date): Employment start date
- **status** (String[1], Default '1'): Employment status ('1'=Active, '0'=Inactive)

**Relationships**:
- One-to-Many: Department has many Employees
- One-to-One: Employee has one User (authentication)

## Entity: Department
- **department_id** (String[10], Primary Key): Unique department identifier
- **name** (String[100], Required): Department name
- **parent_id** (String[10], Foreign Key): Parent department for hierarchy
- **level** (Integer): Hierarchy level
- **manager_id** (String[10], Foreign Key): Department manager (Employee ID)

**Relationships**:
- Self-referencing: Department may have parent Department
- One-to-Many: Department has many Employees
- Many-to-One: Department belongs to one parent Department

## Entity: User
- **user_id** (String[10], Primary Key): User identifier (same as employee_id)
- **employee_id** (String[10], Foreign Key, Unique): Associated employee
- **username** (String[50], Required, Unique): Login username
- **password_hash** (String[255], Required): Bcrypt hashed password
- **role** (String[20]): User role (e.g., admin, hr, user)
- **last_login** (DateTime): Timestamp of last login
- **is_active** (Boolean, Default True): Account status

**Relationships**:
- Many-to-One: User belongs to one Employee
- One-to-Many: User performs many Sessions

## Entity: Session
- **session_id** (String[255], Primary Key): Session identifier (JWT token)
- **user_id** (String[10], Foreign Key): Associated user
- **created_at** (DateTime, Required): Session creation time
- **expires_at** (DateTime, Required): Session expiration time
- **is_active** (Boolean, Default True): Active session status

**Relationships**:
- Many-to-One: Session belongs to one User

## Validation Rules

**Employee**:
- employee_id: Must be unique, format: E followed by numbers
- name: Required, minimum 2 characters
- email: Valid email format if provided
- phone: Valid phone format if provided
- status: Must be '0' or '1'

**Department**:
- department_id: Must be unique, format: D followed by numbers
- name: Required, minimum 3 characters
- level: Non-negative integer
- parent_id: Must reference existing department or be null

**User**:
- username: Required, unique, 3-50 characters
- password: Minimum 8 characters with complexity requirements
- role: Must be one of allowed values (admin, hr, user)
- employee_id: Must reference existing employee

## State Transitions

**Employee Status**:
- Active ('1') → Inactive ('0'): When employee leaves
- Inactive ('0') → Active ('1'): When employee returns (rare)

**User Account**:
- Active (True) → Inactive (False): Admin deactivation
- Inactive (False) → Active (True): Admin reactivation
- Account locked after N failed login attempts

## Indexing Strategy

**Primary Indexes**:
- employee_id (unique)
- department_id (unique)
- user_id (unique)
- session_id (unique)

**Secondary Indexes**:
- employee.department_id (for department queries)
- employee.status (for status filtering)
- user.username (for login)
- session.expires_at (for cleanup)
- employee.name (for search)