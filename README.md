# Flasky

A lightweight message board web application built with Flask and PostgreSQL. Users can post messages with comma-separated tags and browse all posts on the main page.

## Tech Stack

- **Python 3** — application runtime
- **Flask 1.0** — web framework
- **Flask-SQLAlchemy** — ORM layer
- **PostgreSQL** — database
- **Jinja2** — HTML templating

## Prerequisites

- Python 3.6+
- PostgreSQL running locally
- A database named `py_flasky` created in PostgreSQL

```sql
CREATE DATABASE py_flasky;
```

## Installation

```bash
# Clone the repository
git clone https://github.com/Alexxfromgit/Flasky-application.git
cd Flasky-application

# Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS / Linux

# Install dependencies
pip install -r requirments.txt
```

## Configuration

The database connection string is set in `app.py`:

```python
app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://postgres:root@localhost/py_flasky.db'
```

Update the username, password, host, and database name to match your local PostgreSQL setup. Tables are created automatically on first run via `db.create_all()`.

## Running the App

```bash
python app.py
```

The development server starts at `http://127.0.0.1:5000`.

## API / Routes

| Method | Path | Description |
|--------|------|-------------|
| `GET` | `/` | Welcome page |
| `GET` | `/main` | Lists all messages with their tags |
| `POST` | `/add_message` | Submits a new message; form fields: `text`, `tag` (comma-separated) |

## Data Model

```
Message
  id    INTEGER  PK
  text  VARCHAR(1024)

Tag
  id          INTEGER  PK
  text        VARCHAR(32)
  message_id  INTEGER  FK → Message.id
```

Each message can have multiple tags. Tags are parsed from a comma-separated string at creation time.

## Project Structure

```
.
├── app.py              # Application entry point, models, and routes
├── templates/
│   ├── index.html      # Welcome page
│   └── main.html       # Message board with submission form
└── requirments.txt     # Python dependencies
```

## License

This project is open source and available under the MIT License.
