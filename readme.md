# Simple CRUD Application with Flask

## Introduction
A basic web application demonstrating CRUD operations using the Flask framework. This application allows users to create, read, update, and delete Tasks in a SQLite database.

## Technologies Used
- Flask
- HTML
- CSS
- SQLite
- Jinja2

## Description

### Settting up the environment
-Install Flask and other dependencies using pip3 install flask flask_sqlalchemy.

### Application structure
-app.py: The main application file containing the Flask app and routes.

-templates/: Directory containing HTML templates for rendering pages.

-static/: Directory for static files like CSS.

-text.db: SQLite database file.

## Details

### Database Model
    app = Flask(__name__)
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///text.db'
    db = SQLAlchemy(app)

    class Todo(db.Model):
        id = db.Column(db.Integer, primary_key = True)
        content = db.Column(db.String(200), nullable = False)
        completed = db.Column(db.Integer, default = 0)
        date_created = db.Column(db.DateTime, default=datetime.utcnow)
        
        
        def __repr__(self):
            return '<task %r>' % self.id
        
    with app.app_context():
        db.create_all()

### Read

### Create

### Update

### delete


