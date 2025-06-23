# Task1: Library Database Schema

## Overview
This repository contains a MySQL database schema for a Library Management System, designed as a learning project to practice database design principles.

It demonstrates:
- Entity-relationship (ER) modeling
- Normalization (up to 3rd Normal Form)
- Use of primary keys, foreign keys, and indexes

The system manages authors, categories, books, members, and loan transactions.

## Schema Details
The schema consists of a single database named `library_db` and includes the following tables:

### author
| Column Name | Type                | Description          |
|-------------|---------------------|----------------------|
| author_id   | INT, PK, AUTO_INCREMENT | Unique author ID      |
| name        | VARCHAR(100)        | Author's full name    |
| bio         | TEXT                | Short biography       |

Stores information about book authors.

### category
| Column Name | Type                    | Description           |
|-------------|-------------------------|-----------------------|
| category_id | INT, PK, AUTO_INCREMENT | Unique category ID    |
| category_name | VARCHAR(100), UNIQUE   | Name of the category  |

Stores book categories or genres.

### book
| Column Name       | Type                            | Description                      |
|-------------------|---------------------------------|--------------------------------|
| book_id           | INT, PK, AUTO_INCREMENT         | Unique book ID                  |
| title             | VARCHAR(255)                    | Title of the book               |
| isbn              | VARCHAR(13), UNIQUE             | ISBN number (unique)            |
| publication_year  | INT                            | Year of publication            |
| category_id       | INT, FK                       | Reference to category           |
| status            | ENUM('available', 'borrowed'), default 'available' | Availability status             |

Tracks books and their categories.

### book_author
| Column Name | Type       | Description                    |
|-------------|------------|-------------------------------|
| book_id     | INT, FK    | Reference to book              |
| author_id   | INT, FK    | Reference to author            |

Many-to-many relationship between books and authors.

### member
| Column Name | Type                  | Description                |
|-------------|-----------------------|----------------------------|
| member_id   | INT, PK, AUTO_INCREMENT | Unique member ID           |
| first_name  | VARCHAR(50)           | Member’s first name         |
| last_name   | VARCHAR(50)           | Member’s last name          |
| email       | VARCHAR(100), UNIQUE  | Member’s email address      |
| address     | VARCHAR(255)          | Member’s residential address|

Stores details of library members.

### loan
| Column Name | Type                  | Description                   |
|-------------|-----------------------|-------------------------------|
| loan_id     | INT, PK, AUTO_INCREMENT | Unique loan transaction ID   |
| book_id     | INT, FK               | Reference to the loaned book  |
| member_id   | INT, FK               | Reference to the member       |
| loan_date   | DATE                  | Date when book was borrowed   |
| return_date | DATE                  | Date when book was returned   |

Records book loan transactions.  
One book can only be loaned to one member at a time (enforced by UNIQUE on book_id).

## Relationships
- Author to Book: Many-to-Many (via book_author table)  
- Category to Book: One-to-Many (1:N)  
- Book to Loan: One-to-One (1:1, enforced via UNIQUE on book_id)  
- Member to Loan: One-to-Many (1:N)  

All foreign keys use `ON DELETE CASCADE` or `ON DELETE SET NULL` to maintain referential integrity.

## Prerequisites
- MySQL Server  
- MySQL Workbench  
- A MySQL user account with privileges to:
  - Create databases  
  - Create tables  
  - Add foreign keys and indexes  

## Usage
1. Clone or download this repository.  
2. Open the SQL script (`library_schema.sql`) in MySQL Workbench.  
3. Run the script to create the `library_db` database and its schema.  
4. Use the ER diagram tool in Workbench to visualize relationships.




