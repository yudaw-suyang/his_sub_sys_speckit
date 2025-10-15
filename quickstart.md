# Quickstart Guide: HIS Subsystem

## Prerequisites

- Python 3.8 or higher
- Oracle SQL Server (with cx_Oracle client)
- Node.js (for development only, not required in production)
- Git

## Environment Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd his_subsystem
```

### 2. Backend Setup
```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Linux/Mac:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Database Setup
```bash
# Ensure Oracle SQL Server is running
# Update .env file with your database connection details:

DB_HOST=localhost
DB_PORT=1521
DB_SERVICE=ORCL
DB_USER=his_user
DB_PASSWORD=your_password
```

### 4. Environment Variables
Create a `.env` file in the backend directory with the following:
```ini
APP_NAME=HIS Sub System
APP_VERSION=1.0.0
DEBUG=False
ENVIRONMENT=production

HOST=0.0.0.0
PORT=8000
WORKERS=4

DB_HOST=localhost
DB_PORT=1521
DB_SERVICE=ORCL
DB_USER=his_user
DB_PASSWORD=secure_password

SECRET_KEY=your-secret-key-min-32-characters-long
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
REFRESH_TOKEN_EXPIRE_DAYS=7

CORS_ORIGINS=["http://localhost", "http://192.168.1.100"]

LOG_LEVEL=INFO
LOG_FILE=logs/app.log
```

## Running the Application

### 1. Backend Server
```bash
cd backend
# Activate virtual environment if not already active
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate     # Windows

# Run the application
python run.py
# Or with uvicorn directly:
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

### 2. Frontend (No build step needed)
The frontend is served as static files by Nginx. Simply place the `frontend/` directory content in your web server's static files directory.

## API Endpoints

### Authentication
- `POST /api/v1/auth/login` - User login
- `POST /api/v1/auth/refresh` - Token refresh
- `POST /api/v1/auth/logout` - User logout

### Users
- `GET /api/v1/users` - List users (with pagination/filtering)
- `GET /api/v1/users/{employee_id}` - Get user details
- `POST /api/v1/users` - Create user
- `PUT /api/v1/users/{employee_id}` - Update user
- `DELETE /api/v1/users/{employee_id}` - Delete user

### Departments
- `GET /api/v1/departments` - List departments
- `GET /api/v1/departments/{dept_id}` - Get department details
- `POST /api/v1/departments` - Create department
- `PUT /api/v1/departments/{dept_id}` - Update department
- `DELETE /api/v1/departments/{dept_id}` - Delete department

### Configuration
- `GET /api/v1/config/frontend` - Get frontend configuration

## Frontend Usage

1. Access the system at `http://your-server-address/`
2. Login with your employee ID and password
3. Use the navigation menu to access different features

## Development

### Backend Development
1. Run the backend with auto-reload: `uvicorn app.main:app --reload`
2. Access the automatic API documentation at `http://localhost:8000/docs`

### Frontend Development
1. The frontend uses a component-based architecture
2. Components are located in `frontend/components/`
3. Pages are located in `frontend/pages/`
4. Utilities are in `frontend/utils/`

## Configuration for Production

1. Set `DEBUG=False` in your environment
2. Use a reverse proxy like Nginx to serve static files
3. Set up proper SSL certificates
4. Configure proper logging and monitoring

## Troubleshooting

### Common Issues
- Database connection errors: Check your `.env` database configuration
- Frontend not loading: Ensure static files are properly configured in your web server
- Authentication errors: Verify SECRET_KEY is properly set in environment

### API Documentation
- Auto-generated documentation at `/docs` endpoint
- OpenAPI schema at `/openapi.json` endpoint