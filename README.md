# Anam Hospital Web Application

A full-stack web application for a hospital website, built with Flask and SQLite. Visitors can read about the hospital, submit an appointment enquiry through a contact form, and sign in through a login form. All submissions are stored in a SQLite database using parameterized queries.

This project is a frontend and backend learning project. It demonstrates how an HTML/CSS frontend communicates with a Python backend and a relational database.

## Features

- Landing page with hospital information and patient reviews
- Contact form that collects name, age, gender, email, phone, department and message
- Form data stored in a SQLite database
- Login form that validates credentials against a users table
- Automatic database and table creation on first run
- SQL queries written with parameter placeholders to prevent SQL injection

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Database | SQLite (sqlite3 module) |
| Frontend | HTML5, CSS3 |
| Templating | Jinja2 |
| Icons and Fonts | Font Awesome, Google Fonts (Poppins) |
| Version Control | Git, GitHub |

## Project Structure

```
Anam-Hospital-Flask/
|-- app.py                  Flask application, routes and database setup
|-- requirements.txt        Python dependencies
|-- templates/
|   |-- index.html          Single page template (home, contact, login)
|-- static/
|   |-- style.css           Stylesheet
|   |-- images/             Images used on the page
|-- database.db             SQLite database (created automatically, not tracked)
|-- DOCUMENTATION.md        Detailed technical documentation
|-- README.md
```

## How It Works

1. The browser requests `/` and Flask renders `templates/index.html`.
2. The user fills the contact form, which sends a POST request to `/contact`.
3. Flask reads the form data and inserts it into the `contact_messages` table.
4. The user is redirected back to the home page.
5. The login form sends a POST request to `/login`, and Flask checks the email and password against the `users` table.

## Routes

| Route | Method | Description |
|---|---|---|
| `/` | GET | Renders the home page |
| `/contact` | POST | Saves a contact form submission to the database |
| `/login` | POST | Validates login credentials |

## Database Schema

**contact_messages**

| Column | Type | Notes |
|---|---|---|
| id | INTEGER | Primary key, auto increment |
| name | TEXT | Required |
| age | INTEGER | Required |
| gender | TEXT | Required |
| email | TEXT | Required |
| phone | TEXT | Required |
| department | TEXT | Required |
| message | TEXT | Optional |

**users**

| Column | Type | Notes |
|---|---|---|
| id | INTEGER | Primary key, auto increment |
| email | TEXT | Unique, required |
| password | TEXT | Required |

## Getting Started

### Prerequisites

- Python 3.5 or higher
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/akramwasim-in/Anam-Hospital-Flask.git
cd Anam-Hospital-Flask

# Install dependencies
pip install -r requirements.txt

# Run the application
python app.py
```

Open `http://127.0.0.1:5000` in your browser. The database file and tables are created automatically on the first run.

### Demo Login

A demo account is created automatically for testing:

- Email: `admin@gmail.com`
- Password: `admin123`

This account is for local demonstration only.

##
- <img width="954" height="321" alt="image" src="https://github.com/user-attachments/assets/8f2ad3ea-a44b-4362-aa56-e66fcd90c26f" />




## Author

**Wasim Akram**
GitHub: [akramwasim-in](https://github.com/akramwasim-in)
LinkedIn: [akramwasim-in](https://linkedin.com/in/akramwasim-in)
