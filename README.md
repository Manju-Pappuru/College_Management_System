# College Management System

A comprehensive college management system with **Firebase Authentication**, built using React.js frontend and Node.js/Express.js backend with **MySQL database**.

## Features

- **Firebase Authentication** - Secure login with Google, email/password
- **Role-Based Access Control** - Separate dashboards for Students, Faculty, and Admin
- **Student Module** - View personal details, subjects, attendance, marks, and timetable
- **Faculty Module** - Manage assigned subjects, mark attendance, add/update student marks
- **Admin Module** - Full CRUD operations for students, faculty, subjects, departments
- **Dashboard** - Statistics overview with key metrics

## Technology Stack

- **Frontend**: React.js, Bootstrap 5, React Router
- **Backend**: Node.js, Express.js
- **Database**: MySQL with mysql2 driver
- **Authentication**: Firebase Auth (Google + Email/Password)
- **Styling**: CSS with Bootstrap components

## Setup Instructions

### Prerequisites

- Node.js (v16+)
- MySQL (v5.7+ or v8.0+)
- Firebase Project with Authentication enabled (Google and Email/Password providers)

### 1. MySQL Setup

Create a MySQL database:
```sql
CREATE DATABASE college_management;
CREATE USER 'college_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON college_management.* TO 'college_user'@'localhost';
```

### 2. Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the backend directory:
   ```
   PORT=5000
   MYSQL_HOST=localhost
   MYSQL_USER=college_user
   MYSQL_PASSWORD=your_password
   MYSQL_DATABASE=college_management
   MYSQL_PORT=3306
   FIREBASE_PROJECT_ID=your-firebase-project-id
   FIREBASE_CLIENT_EMAIL=your-client-email@your-firebase-project-id.iam.gserviceaccount.com
   FIREBASE_PRIVATE_KEY=-----BEGIN PRIVATE KEY-----\nyour-private-key-here\n-----END PRIVATE KEY-----
   FRONTEND_URL=http://localhost:3000
   ```

4. Start the backend server:
   ```bash
   npm run dev
   ```
   The server will run on http://localhost:5000

### 3. Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the frontend directory:
   ```
   REACT_APP_API_URL=http://localhost:5000/api
   REACT_APP_FIREBASE_API_KEY=your-firebase-api-key
   REACT_APP_FIREBASE_AUTH_DOMAIN=your-project-id.firebaseapp.com
   REACT_APP_FIREBASE_PROJECT_ID=your-project-id
   REACT_APP_FIREBASE_STORAGE_BUCKET=your-project-id.appspot.com
   REACT_APP_FIREBASE_MESSAGING_SENDER_ID=123456789012
   REACT_APP_FIREBASE_APP_ID=your-app-id
   ```

4. Start the frontend development server:
   ```bash
   npm start
   ```
   The application will run on http://localhost:3000

### 4. Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project or select an existing one
3. Enable Google Authentication in the Authentication section
4. Enable Email/Password Authentication
5. Download the service account key (JSON file) and copy:
   - `project_id` → `FIREBASE_PROJECT_ID`
   - `client_email` → `FIREBASE_CLIENT_EMAIL`
   - `private_key` → `FIREBASE_PRIVATE_KEY`
6. In Project Settings > General > Your apps, copy the Firebase SDK config values

## Database Schema

The application creates the following tables automatically:

- `users` - User accounts (students, faculty, admin)
- `departments` - Department information
- `students` - Student profiles linked to users
- `faculty` - Faculty profiles linked to users
- `subjects` - Subject/course information
- `student_subjects` - Many-to-many relationship between students and subjects
- `faculty_subjects` - Many-to-many relationship between faculty and subjects
- `attendance` - Student attendance records
- `marks` - Student assessment marks

## API Endpoints

### Authentication
- `POST /api/auth/login` - Login with Firebase ID token
- `GET /api/auth/profile` - Get current user profile
- `POST /api/auth/update-role` - Update user role (Admin)
- `GET /api/auth/logout` - Logout user

### Students
- `GET /api/students` - Get all students (faculty/admin)
- `GET /api/students/:id` - Get student by ID
- `POST /api/students` - Create new student (admin)
- `PUT /api/students/:id` - Update student (admin/student)
- `DELETE /api/students/:id` - Delete student (admin)

### Faculty
- `GET /api/faculty` - Get all faculty (faculty/admin)
- `GET /api/faculty/:id` - Get faculty by ID
- `POST /api/faculty` - Create new faculty (admin)
- `PUT /api/faculty/:id` - Update faculty (admin/faculty)
- `DELETE /api/faculty/:id` - Delete faculty (admin)

### Subjects
- `GET /api/subjects` - Get all subjects (faculty/admin)
- `GET /api/subjects/:id` - Get subject by ID
- `POST /api/subjects` - Create new subject (admin)
- `PUT /api/subjects/:id` - Update subject (admin)
- `DELETE /api/subjects/:id` - Delete subject (admin)

### Departments
- `GET /api/departments` - Get all departments (faculty/admin)
- `GET /api/departments/:id` - Get department by ID
- `POST /api/departments` - Create new department (admin)
- `PUT /api/departments/:id` - Update department (admin)
- `DELETE /api/departments/:id` - Delete department (admin)
- `GET /api/departments/dashboard/stats` - Get dashboard statistics (admin)

### Attendance
- `GET /api/attendance` - Get attendance records (faculty/admin)
- `GET /api/attendance/student/:studentId/subject/:subjectId` - Get student attendance
- `POST /api/attendance/mark` - Mark attendance (faculty)
- `GET /api/attendance/summary/:studentId` - Get attendance summary

### Marks
- `GET /api/marks` - Get marks records (faculty/admin)
- `GET /api/marks/student/:studentId` - Get marks for student
- `POST /api/marks` - Add marks (faculty)
- `PUT /api/marks/:id` - Update marks (faculty)
- `DELETE /api/marks/:id` - Delete marks (admin)

## Project Structure

```
college_management/
├── backend/
│   ├── config/           # db.js, schema.js, auth.js
│   ├── controllers/      # Request handlers (MySQL queries)
│   ├── middlewares/      # Auth middleware
│   ├── routes/           # API route definitions
│   ├── server.js         # Express server entry point
│   ├── .env              # Environment variables
│   └── package.json
└── frontend/
    ├── public/
    └── src/
        ├── components/     # React components
        ├── context/        # React context (Auth with Firebase)
        ├── services/       # API service functions
        ├── App.js          # Main App component
        └── index.js        # Entry point
```

## Usage

1. Ensure MySQL is running on localhost:3306
2. Run `npm run dev` in the backend directory
3. Run `npm start` in the frontend directory
4. Visit http://localhost:3000 in your browser
5. Click "Sign in with Google" or use email/password to authenticate
6. After successful login, you'll be redirected to your role-based dashboard
7. Use the sidebar menu to navigate to different features

## Default Departments

The system seeds the following departments by default:
- Computer Science (CSE)
- Electronics & Communication (ECE)
- Mechanical Engineering (MECH)
- Civil Engineering (CIVIL)
- Electrical Engineering (EE)

## Security Notes

- In production, ensure you:
  - Use HTTPS in production
  - Configure proper CORS origins
  - Use strong secrets and keys
  - Use environment variables for all sensitive data
  - Enable rate limiting for auth endpoints

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License.