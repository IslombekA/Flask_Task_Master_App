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
- Install Flask and other dependencies using pip3 install flask flask_sqlalchemy.

### Application structure
- app.py: The main application file containing the Flask app and routes.

- templates/: Directory containing HTML templates for rendering pages.

- static/: Directory for static files like CSS.

- text.db: SQLite database file.

## Details

### Database Model
```python
class Todo(db.Model):
    id = db.Column(db.Integer, primary_key = True)
    content = db.Column(db.String(200), nullable = False)
    completed = db.Column(db.Integer, default = 0)
    date_created = db.Column(db.DateTime, default=datetime.utcnow)
    
    def __repr__(self):
        return '<task %r>' % self.id
```

### Create and Read a task
```python
@app.route('/', methods = ['POST', 'GET'])
def index():
    if request.method == 'POST':
        task_content = request.form['content']
        new_task = Todo(content = task_content) 
        
        try:
            db.session.add(new_task)
            db.session.commit()
            return redirect('/')
        except:
            return "There was an issue adding your task"
    else:
        tasks = Todo.query.order_by(Todo.date_created).all()
        return render_template('index.html', tasks=tasks)
```

### Update a task
```python
@app.route('/update/<int:id>', methods=['GET', 'POST'])
def update(id):
    task = Todo.query.get_or_404(id)

    if request.method == 'POST':
        task.content = request.form['content']
        
        try:
            db.session.commit()
            return redirect('/')
        except:
            return 'There was an issue updating your task'
        
    else:
        return render_template('update.html', task=task)
```

### Delete a task
```python
@app.route('/delete/<int:id>')
def delete(id):
    task_to_delete = Todo.query.get_or_404(id)

    try:
        db.session.delete(task_to_delete)
        db.session.commit()
        return redirect('/')
    except:
        return 'There was an issue trying to delete that task'
```
## Conclusion
This CRUD application provides a foundational understanding of how to manage data using Flask and SQLite. It can be expanded with additional features such as user authentication, more complex data models, and integration with other databases like PostgreSQL or MySQL.
