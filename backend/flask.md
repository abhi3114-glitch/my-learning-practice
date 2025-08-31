# Flask

## Overview
Flask is a lightweight WSGI Python web framework that is easy to get started with and scales to complex applications.

## Basic Setup
```python
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!'

@app.route('/api/users', methods=['GET', 'POST'])
def users():
    if request.method == 'POST':
        data = request.json
        return jsonify(data), 201
    return jsonify([])

if __name__ == '__main__':
    app.run(debug=True)
```

## Routing
```python
@app.route('/user/<int:user_id>')
def user(user_id):
    return f'User {user_id}'

@app.route('/search')
def search():
    q = request.args.get('q', '')
    return f'Searching for: {q}'
```

## Blueprints
```python
from flask import Blueprint

api = Blueprint('api', __name__, url_prefix='/api')

@api.route('/users')
def get_users():
    return jsonify([])

app.register_blueprint(api)
```

## Templates (Jinja2)
```python
from flask import render_template

@app.route('/profile/<name>')
def profile(name):
    return render_template('profile.html', name=name)
```

## Error Handling
```python
@app.errorhandler(404)
def not_found(error):
    return jsonify({'error': 'Not found'}), 404
```

## Best Practices
1. Use **Blueprints** for modular code
2. Use **Flask extensions** (Flask-SQLAlchemy, Flask-Login)
3. Configure with **environment variables**

## Resources
- Flask Documentation
