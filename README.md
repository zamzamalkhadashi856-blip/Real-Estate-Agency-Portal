# Real Estate Agency Portal


A web-based Real Estate Agency Portal built with PHP and MySQL that allows agents, buyers, and renters to interact with property listings and agency services.

## Features

- **Agents**: Add and manage property listings, view all inquiries and transactions
- **Buyers**: Browse properties, save favorites, submit inquiries, purchase properties
- **Renters**: Browse rental properties, save favorites, submit inquiries, rent properties
- **Secure Login**: Password hashing with `password_hash()` and `password_verify()`
- **Role-Based Access Control**: Different permissions based on user type
- **MySQL Integration**: Stored procedures, views, triggers, and prepared statements

## Technology Stack

- PHP 8.1+
- MySQL 8.0+
- HTML5 / CSS3
- PDO for database access

## Setup Instructions

### 1. Clone or Download the Project

```bash
git clone <repository-url>
cd real-estate-portal
```

### 2. Create the MySQL Database

Open phpMyAdmin or MySQL command line and run the SQL script:

```bash
mysql -u root -p < sql/real_estate_portal_db.sql
```

Or import `sql/real_estate_portal_db.sql` through phpMyAdmin.

This script will:
- Create the database `real_estate_portal_db`
- Create all 5 tables (Users, Properties, Inquiries, Transactions, Favorites)
- Create stored procedures (`AddOrUpdateUser`, `ProcessTransaction`)
- Create the view (`PropertyListingView`)
- Create the trigger (`AfterTransactionInsert`)
- Insert sample data (3 users, 3 properties, 3 inquiries, 3 transactions, 3 favorites)

### 3. Configure Database Connection

Edit `config/config.php` to match your MySQL credentials:

```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'real_estate_portal_db');
define('DB_USER', 'root');
define('DB_PASS', '');  // MySQL password
```

### 4. Run the Application

Place the project folder in your web server's document root:

- **XAMPP**: `htdocs/real-estate-portal/`
- **WAMP**: `www/real-estate-portal/`
- **MAMP**: `htdocs/real-estate-portal/`

Access the application at:
```
http://localhost/real-estate-portal/
```

## Demo Accounts

| Role   | Username     | Password    |
|--------|-------------|-------------|
| Agent  | john_smith  | password123 |
| Buyer  | sarah_jones | password123 |
| Renter | mike_wilson | password123 |

## Project Structure

```
real-estate-portal/
  config/
    config.php           # Database configuration
  classes/
    Database.php         # PDO connection class
    RealEstateDatabase.php  # Main database operations class
  includes/
    header.php           # Page header template
    footer.php           # Page footer template
  assets/
    style.css            # Stylesheet
  sql/
    real_estate_portal_db.sql  # Database setup script
  index.php              # Homepage
  login.php              # Login page
  register.php           # Registration page
  properties.php         # Browse properties
  property_details.php   # View single property
  add_property.php       # Add new property (agent only)
  submit_inquiry.php     # Submit property inquiry
  favorites.php          # View saved properties
  dashboard.php          # User dashboard
  logout.php             # End session
  README.md              # This file
```

## MySQL Components

### Tables
- **Users**: Stores all registered users
- **Properties**: Stores property listings
- **Inquiries**: Stores buyer/renter inquiries
- **Transactions**: Stores completed purchases and rentals
- **Favorites**: Stores saved properties

### Stored Procedures
- **AddOrUpdateUser**: Add or update a user record
- **ProcessTransaction**: Record a transaction and update property status

### Views
- **PropertyListingView**: Combined property and agent information

### Triggers
- **AfterTransactionInsert**: Auto-update property status after transaction

## Implemented PHP Methods

- `addUser()` - Register new users with hashed passwords
- `getUserByUsername()` - Retrieve user for login
- `getUserDetails()` - Get user with inquiries, favorites, and transactions
- `addProperty()` - Add property listings (agent)
- `getAllProperties()` - Browse all properties
- `getPropertyById()` - View property details
- `getPropertiesByCity()` - Search by city
- `getPropertiesByPriceRange()` - Filter by price
- `addInquiry()` - Submit property inquiries
- `addFavorite()` / `removeFavorite()` - Manage saved properties
- `getPropertyListingView()` - Use the database view
- `getStatistics()` - Dashboard statistics

## Security Features

- Password hashing with `password_hash()` using bcrypt
- Password verification with `password_verify()`
- Session management with `session_regenerate_id()`
- Role-based access control on restricted pages
- Prepared statements for all SQL queries (prevents SQL injection)
- Output escaping with `htmlspecialchars()` (prevents XSS)
- CSRF protection considerations

