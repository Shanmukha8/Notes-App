# Personal Notes App with Login System

A secure web application built with Python, Flask, and SQLite that allows users to register, log in, and manage personal notes with full CRUD functionality.

## Features

### 🔐 User Authentication
- Secure user registration with password hashing (Werkzeug)
- Login/logout functionality
- Session management for personalized user data
- Password validation (minimum 6 characters)

### 📝 Note Management (CRUD)
- **Create**: Add new notes with title and content
- **Read**: View all notes in dashboard or individual note details
- **Update**: Edit existing notes
- **Delete**: Remove notes with confirmation

### 🎨 User Interface
- Clean, modern responsive design
- Purple gradient theme
- Card-based note display
- Flash messages for user feedback
- Mobile-friendly layout

## Technology Stack

- **Backend**: Python 3.x, Flask
- **Database**: SQLite3
- **Security**: Werkzeug password hashing
- **Frontend**: HTML5, CSS3 (embedded in templates)

## Project Structure

```
personal-notes-app/
│
├── app.py                      # Main Flask application
├── notes.db                    # SQLite database (auto-created)
│
└── templates/
    ├── base.html              # Base template with navbar
    ├── login.html             # Login page
    ├── register.html          # Registration page
    ├── dashboard.html         # Notes dashboard
    ├── create_note.html       # Create note form
    ├── edit_note.html         # Edit note form
    └── view_note.html         # View note details
```

## Installation & Setup

### Prerequisites
- Python 3.7 or higher
- pip (Python package manager)

### Step 1: Install Dependencies

```bash
pip install flask
```

### Step 2: Create Project Structure

Create a folder called `personal-notes-app` and inside it:
1. Create `app.py` with the main Flask code
2. Create a `templates` folder
3. Add all the HTML template files in the `templates` folder

### Step 3: Run the Application

```bash
python app.py
```

The application will start on `http://127.0.0.1:5000/`

## Usage Guide

### First Time Setup

1. **Access the Application**: Open your browser and go to `http://127.0.0.1:5000/`

2. **Register an Account**:
   - Click "Register here" on the login page
   - Fill in username, email, and password
   - Password must be at least 6 characters
   - Click "Register"

3. **Login**:
   - Enter your username and password
   - Click "Login"

### Managing Notes

**Creating a Note**:
1. Click "Create New Note" from the dashboard
2. Enter a title and content
3. Click "Save Note"

**Viewing Notes**:
- All notes are displayed on the dashboard in card format
- Click "View" to see full note details

**Editing a Note**:
1. Click "Edit" on any note card
2. Modify the title or content
3. Click "Update Note"

**Deleting a Note**:
1. Click "Delete" on any note card
2. Confirm deletion in the popup

**Logout**:
- Click "Logout" in the navbar to end your session

## Database Schema

### Users Table
```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT UNIQUE NOT NULL,
    email TEXT UNIQUE NOT NULL,
    password TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
)
```

### Notes Table
```sql
CREATE TABLE notes (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER NOT NULL,
    title TEXT NOT NULL,
    content TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users (id)
)
```

## Security Features

- **Password Hashing**: All passwords are hashed using Werkzeug's security functions
- **Session Management**: Flask sessions store user authentication state
- **SQL Injection Prevention**: Parameterized queries protect against SQL injection
- **User Isolation**: Each user can only access their own notes
- **Input Validation**: Server-side validation for all form inputs

## Configuration

### Change Secret Key (Important for Production!)

In `app.py`, update the secret key:

```python
app.secret_key = 'your-very-secure-secret-key-here'
```

Generate a secure key using:
```python
import secrets
print(secrets.token_hex(32))
```

### Database Location

By default, `notes.db` is created in the same directory as `app.py`. To change this, modify the database connection in `app.py`:

```python
conn = sqlite3.connect('/path/to/your/database.db')
```

## Production Deployment Considerations

Before deploying to production:

1. **Change the secret key** to a strong, random value
2. **Set debug mode to False**: `app.run(debug=False)`
3. **Use a production WSGI server** (Gunicorn, uWSGI)
4. **Implement HTTPS** for secure data transmission
5. **Add rate limiting** to prevent brute force attacks
6. **Set up proper logging**
7. **Use environment variables** for sensitive configuration
8. **Consider PostgreSQL or MySQL** instead of SQLite for better concurrent access

## Troubleshooting

**Issue**: Database locked error
- **Solution**: Close any other connections to the database or restart the application

**Issue**: Template not found
- **Solution**: Ensure all HTML files are in the `templates` folder

**Issue**: Import errors
- **Solution**: Install Flask using `pip install flask`

**Issue**: Session not persisting
- **Solution**: Make sure the secret key is set in `app.py`

## Future Enhancements

Potential features to add:
- Note categories/tags
- Search functionality
- Rich text editor
- Note sharing between users
- Export notes to PDF/text
- Email verification
- Password reset functionality
- Dark mode toggle
- Note archiving

## License

This project is open source and available for educational purposes.

## Author

Built with Flask, demonstrating secure user authentication and CRUD operations.

---

**Note**: This is a development application. For production use, implement additional security measures and use a production-grade database and web server.
