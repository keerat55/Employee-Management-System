# Employee Management System

A comprehensive employee management system designed to streamline HR operations and employee data management. This Final Year Project (FYP) aims to simplify employee records, attendance tracking, payroll management, and performance evaluation.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Database Schema](#database-schema)
- [API Endpoints](#api-endpoints)
- [Project Structure](#project-structure)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Overview

The Employee Management System is a full-stack web application that provides organizations with a centralized platform to manage employee information, track attendance, manage payroll, handle leave requests, and evaluate employee performance. The system is designed to reduce paperwork, improve efficiency, and provide data-driven insights into workforce management.

### Key Objectives

- Centralize employee information and records
- Automate attendance tracking
- Streamline leave management process
- Simplify payroll calculations
- Facilitate performance evaluations
- Generate insightful reports and analytics

## Features

### Core Functionality

- **Employee Management**
  - Add, edit, and delete employee records
  - Manage employee personal and professional information
  - Track employee status (active, inactive, on leave)
  - Department and role-based organization

- **Attendance Tracking**
  - Daily attendance marking
  - Attendance reports and analytics
  - Late arrival tracking
  - Automatic absent notifications

- **Leave Management**
  - Submit leave requests
  - Approve/reject leave applications
  - Track leave balance
  - Multiple leave types (sick, casual, earned, etc.)

- **Payroll System**
  - Automated salary calculations
  - Deductions and allowances management
  - Payslip generation
  - Tax calculations
  - Salary history and records

- **Performance Management**
  - Performance review scheduling
  - Rating and feedback system
  - Goal tracking
  - Performance reports

- **Dashboard & Analytics**
  - Executive dashboard with KPIs
  - Employee statistics
  - Department-wise reports
  - Graphical data visualization
  - Export to PDF/Excel

- **User Management**
  - Role-based access control (Admin, Manager, HR, Employee)
  - User authentication and authorization
  - Activity logging
  - Password management

## Technologies Used

### Frontend
- **Framework**: [React.js / Angular / Vue.js] - *Specify your framework*
- **UI Library**: [Material-UI / Bootstrap / Tailwind CSS] - *Specify your choice*
- **State Management**: [Redux / Context API / Vuex]
- **HTTP Client**: Axios

### Backend
- **Language**: [Node.js / Python / Java] - *Specify your backend*
- **Framework**: [Express.js / Django / Spring Boot]
- **Authentication**: JWT (JSON Web Tokens)
- **API**: RESTful Architecture

### Database
- **Database**: [MySQL / PostgreSQL / MongoDB] - *Specify your database*
- **ORM**: [Sequelize / SQLAlchemy / Mongoose]

### Additional Tools
- **Version Control**: Git & GitHub
- **Development Environment**: [Visual Studio Code / IntelliJ IDEA]
- **API Testing**: Postman
- **Deployment**: [Heroku / AWS / Docker]

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     CLIENT LAYER                             │
│                  (Frontend - React.js)                       │
└──────────────────────────┬──────────────────────────────────┘
                           │
                    HTTP/HTTPS
                           │
┌──────────────────────────┴──────────────────────────────────┐
│                     API LAYER                                │
│              (Backend - Express.js/Node.js)                 │
│                  RESTful API Endpoints                      │
└──────────────────────────┬──────────────────────────────────┘
                           │
                    Database Queries
                           │
┌──────────────────────────┴──────────────────────────────────┐
│                   DATABASE LAYER                             │
│                  (MySQL/PostgreSQL)                         │
└─────────────────────────────────────────────────────────────┘
```

## Installation

### Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v14.x or higher)
- npm or yarn package manager
- MySQL/PostgreSQL Database
- Git

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/keerat55/Employee-Management-System.git
   cd Employee-Management-System
   ```

2. **Navigate to backend directory**
   ```bash
   cd backend
   ```

3. **Install dependencies**
   ```bash
   npm install
   ```

4. **Create `.env` file**
   ```bash
   cp .env.example .env
   ```

5. **Configure environment variables**
   ```
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=employee_management_db
   DB_USER=your_db_user
   DB_PASSWORD=your_db_password
   JWT_SECRET=your_secret_key
   PORT=5000
   ```

6. **Initialize database**
   ```bash
   npm run migrate
   npm run seed
   ```

7. **Start backend server**
   ```bash
   npm run dev
   ```

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd ../frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create `.env` file**
   ```bash
   REACT_APP_API_URL=http://localhost:5000/api
   ```

4. **Start development server**
   ```bash
   npm start
   ```

The application will be available at `http://localhost:3000`

## Configuration

### Database Configuration

Edit `backend/config/database.js` or `.env` file:

```javascript
{
  host: process.env.DB_HOST,
  port: process.env.DB_PORT,
  database: process.env.DB_NAME,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  dialect: 'mysql' // or 'postgres'
}
```

### JWT Configuration

Update the JWT secret in `.env`:
```
JWT_SECRET=your_very_secure_secret_key_here
JWT_EXPIRE=7d
```

## Usage

### Default Credentials

After seeding the database, you can log in with:

```
Admin Account:
Email: admin@ems.com
Password: admin123

Manager Account:
Email: manager@ems.com
Password: manager123

Employee Account:
Email: employee@ems.com
Password: employee123
```

### Key Operations

#### Adding an Employee
1. Navigate to Employee Management
2. Click "Add New Employee"
3. Fill in employee details
4. Click "Save"

#### Marking Attendance
1. Go to Attendance
2. Select date and department
3. Mark attendance for each employee
4. Submit

#### Applying for Leave
1. Click "My Leave Requests"
2. Click "New Leave Request"
3. Select leave type and dates
4. Submit request

#### Viewing Payslip
1. Navigate to Payroll
2. Select employee and month
3. View or download payslip

## Database Schema

### Main Tables

```sql
-- Employees
CREATE TABLE employees (
  id INT PRIMARY KEY AUTO_INCREMENT,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  phone VARCHAR(20),
  department_id INT,
  position VARCHAR(100),
  joining_date DATE,
  salary DECIMAL(10, 2),
  status ENUM('active', 'inactive', 'on_leave'),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (department_id) REFERENCES departments(id)
);

-- Attendance
CREATE TABLE attendance (
  id INT PRIMARY KEY AUTO_INCREMENT,
  employee_id INT NOT NULL,
  attendance_date DATE NOT NULL,
  status ENUM('present', 'absent', 'late', 'half_day'),
  check_in_time TIME,
  check_out_time TIME,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (employee_id) REFERENCES employees(id)
);

-- Leave Requests
CREATE TABLE leave_requests (
  id INT PRIMARY KEY AUTO_INCREMENT,
  employee_id INT NOT NULL,
  leave_type VARCHAR(50) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NOT NULL,
  reason TEXT,
  status ENUM('pending', 'approved', 'rejected'),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (employee_id) REFERENCES employees(id)
);

-- Payroll
CREATE TABLE payroll (
  id INT PRIMARY KEY AUTO_INCREMENT,
  employee_id INT NOT NULL,
  month_year VARCHAR(7) NOT NULL,
  basic_salary DECIMAL(10, 2),
  allowances DECIMAL(10, 2),
  deductions DECIMAL(10, 2),
  net_salary DECIMAL(10, 2),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (employee_id) REFERENCES employees(id)
);
```

## API Endpoints

### Authentication
```
POST   /api/auth/login          - User login
POST   /api/auth/logout         - User logout
POST   /api/auth/refresh        - Refresh token
```

### Employees
```
GET    /api/employees           - Get all employees
POST   /api/employees           - Create new employee
GET    /api/employees/:id       - Get employee by ID
PUT    /api/employees/:id       - Update employee
DELETE /api/employees/:id       - Delete employee
```

### Attendance
```
GET    /api/attendance          - Get attendance records
POST   /api/attendance          - Mark attendance
GET    /api/attendance/report   - Get attendance report
```

### Leave Management
```
GET    /api/leaves              - Get leave requests
POST   /api/leaves              - Submit leave request
PUT    /api/leaves/:id          - Approve/Reject leave
GET    /api/leaves/balance/:id  - Get leave balance
```

### Payroll
```
GET    /api/payroll             - Get payroll records
POST   /api/payroll             - Generate payroll
GET    /api/payroll/:id/slip    - Get payslip
```

## Project Structure

```
Employee-Management-System/
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── redux/
│   │   ├── utils/
│   │   └── App.js
│   └── package.json
├── backend/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middleware/
│   ├── database/
│   │   ├── migrations/
│   │   └── seeds/
│   ├── .env.example
│   └── package.json
├── docs/
│   ├── API_DOCUMENTATION.md
│   └── DATABASE_SCHEMA.md
├── README.md
└── .gitignore
```

## Screenshots

[Add screenshots of your application here]

- Dashboard Overview
- Employee Management Interface
- Attendance Tracking
- Leave Request Form
- Payroll Report

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Guidelines

- Follow the existing code style
- Write meaningful commit messages
- Update documentation as needed
- Test your changes before submitting

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

**Project Author**: Keerat   
**Email**: keerat55@email.com  
**GitHub**: [@keerat55](https://github.com/keerat55)

---

**Last Updated**: [Current Date]  
**Version**: 1.0.0
