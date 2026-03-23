# EmployeeRecordManagement

# Employee Records Management System (ERM 2.0)

A robust, secure, and offline-capable Laravel 12 web application for managing local government unit or corporate employee records. It features role-based access control (RBAC), sophisticated UI components with Light/Dark mode transitions, dynamic data table interactions, and powerful Excel exporting tools.

## Features at a Glance

* *Role-Based Access Control (RBAC):*
  * ADMINISTRATOR: Full control over the system, modifying schemas, managing roles, approving/rejecting user registrations, and handling potentially destructive actions like deleting rows.
  * USER: Human Resources level access. Can manage (Create/Read/Update) employee and employment records, Offices, and Positions, but cannot change global app settings, user roles, or delete anything.
  * GUEST: Default newly registered state. Can only read information after administrative approval. Cannot view management tools.
* *Security First:* Accounts are locked by default upon registration and wait for administrators to Approve them inside the User Management dashboard.
* *UI/UX Polish:* Built with Tailwind CSS, Alpine.js, and Simple-DataTables. The software features an extensive dark mode that matches the aesthetics seamlessly.
* *Smart Reporting:* Excel generation tools through Maatwebsite to quickly extract all newly hired personnel, promotions, or general employment info.

## Prerequisites

Ensure your system meets the following requirements before installing:

* *PHP:* >= 8.2 (with mbstring, xml, pdo, curl, zip extensions enabled)
* *Composer:* Latest stable version
* *Node.js & NPM:* Latest stable version LTS
* *Database:* MySQL, MariaDB, or PostgreSQL (The codebase expects MySQL/MariaDB locally via XAMPP/WAMP/Laragon)
* *Git:* For version control tracking

## Step-by-Step Installation Guide

Follow these steps to deploy ERM 2.0 to your local or remote server environment.

### 1. Clone the Repository
Open your terminal and clone the source code into your desired directory:
git clone <repository_url> employee-records-management
cd employee-records-management

### 2. Install PHP Dependencies
Use Composer to install the required Laravel packages:
composer install

### 3. Install JavaScript/NPM Dependencies
Install the frontend tools (Tailwind CSS, Alpine.js, etc.) required to compile the layout:
npm install

### 4. Create and Configure Environment File
Duplicate the provided example environment config file:
copy .env.example .env     # Windows
cp .env.example .env       # Linux / Mac
Open the newly created .env file in your text editor and modify the database credentials:
env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=employee_records   # Or your preferred database name
DB_USERNAME=root               # Your DB username
DB_PASSWORD=                   # Your DB password

### 5. Generate Application Key
Generate the Laravel encryption key to secure user sessions and internal encryption routing:
php artisan key:generate

### 6. Create the Database
Ensure that you have created the empty database locally (e.g., employee_records) through phpMyAdmin, TablePlus, or the MySQL CLI before continuing.

### 7. Run Migrations & Seeders
Build the database structure and populate it with initial data (such as Default Roles, Offices, Job Classifications, and the primary Admin account):
php artisan migrate --seed

### 8. Link Storage Directories
Because the project handles file uploads (Account Avatars, Personal ID photos, etc.), you must link the storage directory to the public directory:
php artisan storage:link

### 9. Build Frontend Assets
Compile the Tailwind CSS styles and any bundled JavaScript using Vite.
* For local development / live updating:
  
  npm run dev
  
* For production deployment:
  
  npm run build
  

### 10. Start the Application
Boot up the built-in PHP web server:
php artisan serve
By default, the application will be accessible at: http://localhost:8000

## Initial Login Credentials

The --seed command automatically provisions a super administrator account for immediate setup control. 
- *Email:* admin@example.com
- *Password:* password

Note: Immediately update this password via the "Profile" link in the top right corner once logged in.

## Production Deployment Notes

If deploying to a live production server (e.g. Apache, NGINX):
1. Point your web server's document root to the /public directory (NEVER the root folder to prevent exposing .env files).
2. Ensure you run composer install --optimize-autoloader --no-dev.
3. Ensure you run npm run build so Vite correctly outputs the optimized production CSS/JS.
4. Set folder permissions correctly (ensure storage and bootstrap/cache are writable by the web server user):
   
   chmod -R 775 storage bootstrap/cache
   chown -R www-data:www-data storage bootstrap/cache
   
