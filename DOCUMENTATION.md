# Technical Documentation

## 1. Project Overview

Anam Hospital is a small full-stack web application. The frontend is a single HTML page styled with CSS. The backend is a Flask application that handles form submissions and stores data in a SQLite database.

**Purpose:** Practice building a complete request-response flow: browser form, Python route, database insert, and redirect.

## 2. Architecture

```
Browser (HTML, CSS)
      |
      |  HTTP request (GET / , POST /contact , POST /login)
      v
Flask application (app.py)
      |
      |  SQL queries (sqlite3)
      v
SQLite database (database.db)
```

## 3. Backend (app.py)

### 3.1 Database initialization

The function `init_db()` runs when the application starts. It:

1. Opens a connection to `database.db`
2. Creates the `contact_messages` table if it does not exist
3. Creates the `users` table if it does not exist
4. Inserts a demo user using `INSERT OR IGNORE`, so the demo user is not duplicated on restart
5. Commits and closes the connection

### 3.2 Routes

**GET /**
Renders `templates/index.html` using `render_template`.

**POST /contact**
1. Reads `name`, `age`, `gender`, `email`, `phone`, `department` and `message` from `request.form`
2. Inserts them into `contact_messages` using a parameterized query
3. Redirects to `/`

**POST /login**
1. Reads `email` and `password` from `request.form`
2. Runs `SELECT * FROM users WHERE email = ? AND password = ?`
3. Returns a success message if a matching user exists, otherwise an error message with a link back to the home page

### 3.3 Security practices used

- Parameterized SQL queries (`?` placeholders) protect against SQL injection
- Database connection is closed after each operation
- `NOT NULL` constraints on required columns
- `UNIQUE` constraint on user email

## 4. Frontend

### 4.1 Page sections (templates/index.html)

| Section | Id | Description |
|---|---|---|
| Navigation | - | Logo, menu links, support phone number |
| About | `about` | Hospital description, search box and image |
| Reviews | `review-section` | Three patient review cards with star ratings |
| Contact | `contact-form` | Appointment enquiry form |
| Login | `login` | Email and password form |
| Footer | - | Social media icons and copyright |

### 4.2 Forms

**Contact form** posts to `/contact`. Fields: name (text), age (number), gender (select), email (email), phone (tel), department (select), message (textarea). Browser-side validation is applied with the `required` attribute and input types.

**Login form** posts to `/login`. Fields: email and password.

### 4.3 Styling (static/style.css)

- Flexbox is used for the navigation bar, about section and review cards
- CSS Grid is used for the review cards (three columns) and the contact form (two columns)
- Font: Poppins from Google Fonts
- Static files are linked with `url_for('static', filename=...)`

## 5. Database Design

### contact_messages

| Column | Type | Constraint |
|---|---|---|
| id | INTEGER | PRIMARY KEY AUTOINCREMENT |
| name | TEXT | NOT NULL |
| age | INTEGER | NOT NULL |
| gender | TEXT | NOT NULL |
| email | TEXT | NOT NULL |
| phone | TEXT | NOT NULL |
| department | TEXT | NOT NULL |
| message | TEXT | - |

### users

| Column | Type | Constraint |
|---|---|---|
| id | INTEGER | PRIMARY KEY AUTOINCREMENT |
| email | TEXT | UNIQUE NOT NULL |
| password | TEXT | NOT NULL |

## 6. How to Run Locally

```bash
python app.py
```

Application URL: `http://127.0.0.1:5000`

## 7. Testing Checklist

| Test | Expected result |
|---|---|
| Open `/` | Home page loads with all sections |
| Submit contact form with valid data | Redirect to home page, new row in `contact_messages` |
| Submit contact form with empty required field | Browser blocks submission |
| Login with demo credentials | Success message |
| Login with wrong password | Error message with link to retry |
| Restart application | Demo user is not duplicated |



