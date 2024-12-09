# JWT Authentication Project

## Overview
This project implements JSON Web Token (JWT) authentication in a Django REST Framework application. It provides secure endpoints for user authentication, token management, and protected resources.

## Features
- User registration and authentication
- JWT token generation and validation
- Token refresh mechanism
- Protected API endpoints
- Custom user model support
- Role-based access control

## Technologies Used
- Python 3.x
- Django 4.x
- Django REST Framework
- PyJWT
- SQLite/PostgreSQL

## Installation

1. Clone the repository: 

git clone https://github.com/Shreyescodes/JWT-Authentication.git


cd jwt-auth-project

2. Create and activate virtual environment:

```bash
python -m venv env
source env/bin/activate  # On Windows use: env\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Apply migrations:
```bash
python manage.py migrate
```

5. Create superuser (optional):
```bash
python manage.py createsuperuser
```

## Project Structure
```
jwt-auth-project/
├── auth/
│   ├── authapp/
│   │   ├── migrations/
│   │   ├── __init__.py
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── urls.py
│   │   └── views.py
│   ├── auth/
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   └── wsgi.py
│   └── manage.py
├── requirements.txt
└── README.md
```

## API Endpoints

### Authentication
- `POST /api/auth/register/` - Register new user
- `POST /api/auth/login/` - Login and receive tokens
- `POST /api/auth/refresh/` - Refresh access token
- `POST /api/auth/logout/` - Logout and invalidate tokens

### Protected Routes
- `GET /api/user/profile/` - Get user profile
- `PUT /api/user/profile/` - Update user profile
- `GET /api/protected-resource/` - Access protected resource

## Usage

### Registration
```bash
curl -X POST http://localhost:8000/api/auth/register/ \
    -H "Content-Type: application/json" \
    -d '{"username":"testuser","password":"testpass123","email":"test@example.com"}'
```

### Login
```bash
curl -X POST http://localhost:8000/api/auth/login/ \
    -H "Content-Type: application/json" \
    -d '{"username":"testuser","password":"testpass123"}'
```

### Accessing Protected Routes
```bash
curl http://localhost:8000/api/protected-resource/ \
    -H "Authorization: Bearer <your_access_token>"
```

## Configuration

### JWT Settings
Add the following to your `settings.py`:

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}

SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=1),
    'ROTATE_REFRESH_TOKENS': False,
    'BLACKLIST_AFTER_ROTATION': True
}
```

## Security Considerations
- Store tokens securely
- Use HTTPS in production
- Implement rate limiting
- Regular token rotation
- Proper error handling
- Input validation

## Testing
Run the test suite:
```bash
python manage.py test
```

## Contributing
1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Authors
- @Shreyescodes

## Acknowledgments
- Django REST Framework documentation
- PyJWT documentation
- Simple JWT documentation
```
