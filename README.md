# 🏛️ Municipality Reporting System (MRS)

A simple Municipality Reporting System (MRS) for submitting and managing city complaints using PHP, MySQL, HTML, CSS, JavaScript, and Bootstrap.

![PHP](https://img.shields.io/badge/PHP-7.4+-777BB4?style=flat&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-5.7+-4479A1?style=flat&logo=mysql&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=flat&logo=bootstrap&logoColor=white)

---

## 📑 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Screenshots](#-screenshots)
- [Technology Stack](#-technology-stack)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [Database Setup](#-database-setup)
- [Configuration](#-configuration)
- [Project Structure](#-project-structure)
- [Usage](#-usage)
- [Security Features](#-security-features)
- [File Structure Details](#-file-structure-details)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)
- [Acknowledgments](#-acknowledgments)

---

## 📖 About

The **Municipality Reporting System (MRS)** is a full-stack web application designed to facilitate communication between citizens and municipal administrators. The system enables citizens to report various municipal issues such as:

- 🚧 Potholes and road damage
- 💡 Broken streetlights
- 🗑️ Waste management issues
- 🏗️ Infrastructure problems
- 📍 Location-specific complaints

Municipality administrators can efficiently manage, track, and respond to these complaints through a dedicated admin panel.

### Target Audience

- **Citizens**: Submit and track their municipal complaints
- **Municipality Administrators**: Manage complaints, update statuses, and oversee user accounts

---

## ✨ Features

### 👤 User Features

- **User Registration**: Create an account with username, email, password, and optional profile photo
- **Secure Login**: Session-based authentication with role-based access
- **Submit Complaints**: Report municipal issues with title, description, and optional photo attachment
- **View Own Complaints**: Track all submitted complaints with status updates
- **Complaint Status Tracking**: See real-time status of complaints (Pending, Seen, Fixed)

### 🔐 Admin Features

- **View All Complaints**: Access complete list of all submitted complaints
- **Update Complaint Status**: Change complaint status (Pending → Seen → Fixed)
- **User Management**:
  - View all registered users
  - Add new users
  - Edit existing users
  - Delete users
- **Complaint Details**: View detailed information about each complaint including user details

### 🛡️ Security Features

- **Password Hashing**: Uses PHP's `password_hash()` and `password_verify()` for secure password storage
- **Prepared Statements**: PDO prepared statements prevent SQL injection attacks
- **Input Sanitization**: All user input is sanitized using `htmlspecialchars()` to prevent XSS attacks
- **Session Management**: Secure session-based authentication
- **Role-Based Access Control**: Separate access levels for users and administrators
- **File Upload Validation**: Secure file upload handling with validation

### 🎨 Technical Features

- **RTL/Arabic Support**: Full right-to-left layout support for Arabic language interface
- **Responsive Design**: Bootstrap-based responsive design for mobile and desktop
- **File Uploads**: Support for image attachments with complaints
- **Modern UI**: Clean and intuitive user interface

---

## 📸 Screenshots

### Login Page

_Add screenshot of login page here_

### Registration Page

_Add screenshot of registration page here_

### User Dashboard

_Add screenshot of user dashboard here_

### Complaint Submission Form

_Add screenshot of complaint submission form here_

### Admin Dashboard

_Add screenshot of admin dashboard here_

### Complaint Management Interface

_Add screenshot of complaint management interface here_

---

## 🛠️ Technology Stack

### Backend

- **PHP 7.4+**: Server-side scripting language
- **PDO (PHP Data Objects)**: Database abstraction layer for secure database interactions
- **MySQL**: Relational database management system
- **Session Management**: PHP sessions for user authentication

### Frontend

- **HTML5**: Semantic markup with RTL support (`dir="rtl" lang="ar"`)
- **CSS3**: Custom styling with responsive design
- **JavaScript**: Client-side interactivity and form validation
- **Bootstrap**: UI framework for responsive components and grid system

### Development Environment

- **XAMPP/WAMP**: Local server environment (Apache + MySQL + PHP)
- **phpMyAdmin**: Database management tool

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **PHP 7.4 or higher**
- **MySQL 5.7 or higher** (or MariaDB equivalent)
- **XAMPP** or **WAMP** (or similar local server environment)
- **Web Browser** (Chrome, Firefox, Edge, etc.)
- **Git** (for cloning the repository)

---

## 🚀 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/your-username/Municipality-Reporting-System.git
cd Municipality-Reporting-System
```

### Step 2: Set Up Local Server

1. **Install XAMPP** (or WAMP):

   - Download from [XAMPP Official Website](https://www.apachefriends.org/)
   - Install and start Apache and MySQL services

2. **Copy Project Files**:
   - Copy the `rms/` folder to your XAMPP `htdocs/` directory
   - Path should be: `C:\xampp\htdocs\rms\` (Windows) or `/opt/lampp/htdocs/rms/` (Linux)

### Step 3: Create Database

1. Open **phpMyAdmin** in your browser: `http://localhost/phpmyadmin`
2. Click on **"New"** to create a new database
3. Name it: `rms_db`
4. Set collation to: `utf8mb4_general_ci` or `utf8mb4_unicode_ci`
5. Click **"Create"**

### Step 4: Create Database Tables

Run the following SQL commands in phpMyAdmin SQL tab:

```sql
-- Create users table
CREATE TABLE IF NOT EXISTS `users` (
  `user_id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(50) NOT NULL UNIQUE,
  `email` varchar(100) NOT NULL UNIQUE,
  `password` varchar(255) NOT NULL,
  `role` enum('admin','user') NOT NULL DEFAULT 'user',
  `photo` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`user_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Create complaints table
CREATE TABLE IF NOT EXISTS `complaints` (
  `complaint_id` int(11) NOT NULL AUTO_INCREMENT,
  `user_id` int(11) NOT NULL,
  `title` varchar(255) NOT NULL,
  `description` text NOT NULL,
  `photo` varchar(255) DEFAULT NULL,
  `status` enum('Pending','Seen','Fixed') NOT NULL DEFAULT 'Pending',
  `date_added` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (`complaint_id`),
  KEY `user_id` (`user_id`),
  CONSTRAINT `complaints_ibfk_1` FOREIGN KEY (`user_id`) REFERENCES `users` (`user_id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

### Step 5: Configure Database Connection

1. Open `rms/db.php` in a text editor
2. Verify the database connection settings:

```php
$host    = '127.0.0.1';   // or 'localhost'
$dbname  = 'rms_db';      // Database name
$user    = 'root';        // Default XAMPP user
$password = '';           // Default XAMPP password (empty)
```

3. Adjust if your MySQL credentials are different

### Step 6: Set Up Uploads Directory

1. Ensure the `rms/uploads/` directory exists
2. Set proper permissions (write access for web server):
   - **Windows**: Right-click folder → Properties → Security → Allow write permissions
   - **Linux/Mac**: `chmod 755 rms/uploads/`

### Step 7: Create Admin User (Optional)

You can create an admin user directly in the database:

```sql
INSERT INTO `users` (`username`, `email`, `password`, `role`)
VALUES ('admin', 'admin@municipality.com', '$2y$10$YourHashedPasswordHere', 'admin');
```

**Note**: Use `rms/make_hash.php` to generate a password hash, or register through the web interface and manually update the role in the database.

### Step 8: Access the Application

1. Open your web browser
2. Navigate to: `http://localhost/rms/`
3. You should see the login page

---

## 🗄️ Database Setup

### Database Schema

#### `users` Table

| Field      | Type                 | Constraints                 | Description               |
| ---------- | -------------------- | --------------------------- | ------------------------- |
| `user_id`  | INT(11)              | PRIMARY KEY, AUTO_INCREMENT | Unique user identifier    |
| `username` | VARCHAR(50)          | UNIQUE, NOT NULL            | User's username           |
| `email`    | VARCHAR(100)         | UNIQUE, NOT NULL            | User's email address      |
| `password` | VARCHAR(255)         | NOT NULL                    | Hashed password           |
| `role`     | ENUM('admin','user') | NOT NULL, DEFAULT 'user'    | User role (admin or user) |
| `photo`    | VARCHAR(255)         | NULL                        | Profile photo filename    |

#### `complaints` Table

| Field          | Type                           | Constraints                         | Description                    |
| -------------- | ------------------------------ | ----------------------------------- | ------------------------------ |
| `complaint_id` | INT(11)                        | PRIMARY KEY, AUTO_INCREMENT         | Unique complaint identifier    |
| `user_id`      | INT(11)                        | FOREIGN KEY, NOT NULL               | Reference to users table       |
| `title`        | VARCHAR(255)                   | NOT NULL                            | Complaint title                |
| `description`  | TEXT                           | NOT NULL                            | Detailed complaint description |
| `photo`        | VARCHAR(255)                   | NULL                                | Complaint photo filename       |
| `status`       | ENUM('Pending','Seen','Fixed') | NOT NULL, DEFAULT 'Pending'         | Complaint status               |
| `date_added`   | TIMESTAMP                      | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Complaint submission date      |

### Relationships

- **One-to-Many**: One user can have many complaints (`users.user_id` → `complaints.user_id`)

---

## ⚙️ Configuration

### Database Configuration (`rms/db.php`)

The database connection is configured in `rms/db.php`. Default settings for XAMPP:

```php
$host    = '127.0.0.1';   // Database host
$dbname  = 'rms_db';      // Database name
$user    = 'root';        // Database username
$password = '';           // Database password (empty for XAMPP default)
$charset = 'utf8mb4';     // Character set for Arabic support
```

### Upload Directory

- **Location**: `rms/uploads/`
- **Permissions**: Must be writable by web server
- **Supported Formats**: Images (JPEG, PNG, GIF, etc.)

### Session Configuration

Sessions are automatically started in `db.php` for all pages that require authentication.

---

## 📁 Project Structure

```
Municipality-Reporting-System/
│
├── rms/                          # Main application directory
│   ├── admin/                    # Admin panel files
│   │   ├── admin_dashboard.php   # Main admin dashboard
│   │   ├── add_users.php         # Add new users
│   │   ├── edit_users.php        # Edit existing users
│   │   ├── delete_users.php      # Delete users
│   │   ├── view_users.php        # View all users
│   │   └── view_complaint.php    # View and manage complaints
│   │
│   ├── user/                     # User-facing files
│   │   ├── user_home.php         # User dashboard/home
│   │   ├── add_complaint.php     # Submit new complaint
│   │   └── my_complaints.php     # View user's complaints
│   │
│   ├── css/                      # Stylesheets
│   │   └── styles.css            # Main stylesheet
│   │
│   ├── js/                       # JavaScript files
│   │   └── main.js               # Main JavaScript file
│   │
│   ├── uploads/                  # Uploaded files directory
│   │   └── [uploaded files]      # User-uploaded images/documents
│   │
│   ├── db.php                    # Database connection (PDO)
│   ├── login.php                 # Login page
│   ├── register.php              # User registration
│   ├── logout.php                # Logout functionality
│   ├── test.php                  # Testing/debugging file
│   └── make_hash.php             # Password hashing utility
│
├── .gitignore                    # Git ignore file
├── .cursorrules                  # Cursor IDE rules (excluded from git)
└── README.md                     # This file
```

---

## 📖 Usage

### For Users

#### 1. Register a New Account

1. Navigate to `http://localhost/rms/register.php`
2. Fill in the registration form:
   - Username (must be unique)
   - Email (must be unique)
   - Password
   - Optional: Profile photo
3. Click **"تسجيل"** (Register)
4. You'll be redirected to login page upon successful registration

#### 2. Login

1. Navigate to `http://localhost/rms/login.php`
2. Enter your username and password
3. Click **"دخول"** (Login)
4. You'll be redirected to your user dashboard

#### 3. Submit a Complaint

1. From the user dashboard, click **"إضافة شكوى جديدة"** (Add New Complaint)
2. Fill in the complaint form:
   - **Title**: Brief description of the issue
   - **Description**: Detailed explanation of the problem
   - **Photo** (optional): Upload a photo of the issue
3. Click **"إرسال الشكوى"** (Submit Complaint)
4. You'll see a success message upon submission

#### 4. View Your Complaints

1. From the user dashboard, click **"شكاويي"** (My Complaints)
2. View all your submitted complaints with their current status
3. Status options:
   - **Pending** (قيد الانتظار): Complaint is awaiting review
   - **Seen** (تم الاطلاع): Complaint has been viewed by admin
   - **Fixed** (تم الحل): Issue has been resolved

### For Administrators

#### 1. Login as Admin

1. Navigate to `http://localhost/rms/login.php`
2. Login with admin credentials
3. You'll be redirected to the admin dashboard

#### 2. View All Complaints

1. From admin dashboard, click **"عرض جميع الشكاوي"** (View All Complaints)
2. See a complete list of all submitted complaints
3. View complaint details including:
   - Complaint ID
   - Submitting user
   - Title and description
   - Status
   - Submission date
   - Attached photo (if any)

#### 3. Update Complaint Status

1. In the complaints list, use the dropdown menu in the **"تحديث الحالة"** (Update Status) column
2. Select new status:
   - **Pending** → **Seen**: Mark complaint as reviewed
   - **Seen** → **Fixed**: Mark issue as resolved
3. Status updates automatically when you select a new value

#### 4. Manage Users

1. From admin dashboard, click **"إدارة المستخدمين"** (Manage Users)
2. **View Users**: See all registered users
3. **Add User**: Click to add a new user manually
4. **Edit User**: Modify user information
5. **Delete User**: Remove a user (cascades to delete their complaints)

---

## 🔒 Security Features

### Password Security

- Passwords are hashed using PHP's `password_hash()` with `PASSWORD_DEFAULT` algorithm
- Passwords are verified using `password_verify()` - never stored in plain text
- Minimum security: bcrypt algorithm with automatic cost factor

### SQL Injection Prevention

- All database queries use **PDO prepared statements**
- User input is never concatenated directly into SQL queries
- Example:

```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ?");
$stmt->execute([$username]);
```

### XSS (Cross-Site Scripting) Prevention

- All user-generated output is sanitized using `htmlspecialchars()`
- Example:

```php
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
```

### Session Security

- Session-based authentication
- Role-based access control (admin vs user)
- Session validation on every protected page
- Automatic redirect to login if session is invalid

### File Upload Security

- File type validation
- Unique filename generation to prevent overwrites
- Secure file storage in `uploads/` directory

---

## 📄 File Structure Details

### Core Files

#### `rms/db.php`

- **Purpose**: Database connection and session initialization
- **Key Features**:
  - PDO connection with UTF-8 support
  - Exception handling
  - Session auto-start
  - Connection configuration

#### `rms/login.php`

- **Purpose**: User authentication
- **Key Features**:
  - Username/password validation
  - Session creation
  - Role-based redirect (admin → admin dashboard, user → user dashboard)

#### `rms/register.php`

- **Purpose**: New user registration
- **Key Features**:
  - User input validation
  - Password hashing
  - Profile photo upload
  - Duplicate username/email prevention

#### `rms/logout.php`

- **Purpose**: Session termination
- **Key Features**:
  - Destroys session
  - Redirects to login page

### Admin Panel Files (`rms/admin/`)

- **`admin_dashboard.php`**: Main admin interface with navigation
- **`view_complaint.php`**: View and manage all complaints
- **`view_users.php`**: List all registered users
- **`add_users.php`**: Add new users manually
- **`edit_users.php`**: Edit user information
- **`delete_users.php`**: Delete users and their associated data

### User Panel Files (`rms/user/`)

- **`user_home.php`**: User dashboard with navigation
- **`add_complaint.php`**: Complaint submission form
- **`my_complaints.php`**: View user's own complaints

### Assets

- **`css/styles.css`**: Main stylesheet with RTL support
- **`js/main.js`**: Client-side JavaScript for interactivity

---

## 🤝 Contributing

Contributions are welcome! If you'd like to contribute to this project:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/your-feature-name`
3. **Make your changes** following the project's coding standards
4. **Test thoroughly** before submitting
5. **Commit your changes**: `git commit -m 'Add some feature'`
6. **Push to the branch**: `git push origin feature/your-feature-name`
7. **Open a Pull Request**

### Coding Standards

- Follow PSR-12 coding standards for PHP
- Use prepared statements for all database queries
- Sanitize all user input and output
- Add comments explaining complex logic
- Maintain RTL/Arabic language support

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

## 👥 Authors

### Team Leader

**Heba Abd Al-Jalil**

- **GitHub**: [@heba-mustafa59](https://github.com/heba-mustafa59)
- **LinkedIn**: [☆ Heba Mustafa ☆](https://www.linkedin.com/in/heba-mustafa)
- **Email**: hebajalil12@gmail.com

### Team Member

**Amer Abuyaqob**

- **GitHub**: [@Amer-Abuyaqob](https://github.com/Amer-Abuyaqob)
- **LinkedIn**: [Amer Abuyaqob](https://www.linkedin.com/in/amer-abuyaqob)
- **Email**: amer.abuyaqob@gmail.com

---

## 🙏 Acknowledgments

- **Bootstrap**: For the responsive UI framework
- **PHP Community**: For excellent documentation and resources
- **MySQL**: For robust database management
- **XAMPP**: For easy local development environment

---

**Made with ❤️ for better municipal services**
