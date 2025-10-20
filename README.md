# ALX Travel App

A comprehensive Django-based travel listing platform with REST API support, Swagger documentation, and PostgreSQL database integration.

## Project Overview

The ALX Travel App is a real-world Django application designed as a foundation for a travel listing platform. This project demonstrates industry-standard best practices for Django development, including modular configuration, secure environment variable management, and comprehensive API documentation.

## Features

- **Django REST Framework**: Full REST API support for building scalable backend services
- **Swagger/OpenAPI Documentation**: Automatic API documentation available at `/swagger/`
- **PostgreSQL Database**: Robust database configuration with environment variable management
- **CORS Support**: Cross-Origin Resource Sharing for frontend integration
- **Celery Integration**: Ready for background task processing
- **Environment-based Configuration**: Secure settings management using `django-environ`

## Technology Stack

- **Backend Framework**: Django 5.2.7
- **API Framework**: Django REST Framework 3.16.1
- **Database**: PostgreSQL
- **API Documentation**: drf-yasg (Swagger/OpenAPI)
- **Task Queue**: Celery with Redis
- **CORS**: django-cors-headers

## Project Structure

```
alx_travel_app/
├── alx_travel_app/          # Main project directory
│   ├── __init__.py
│   ├── settings.py          # Project settings with environment variables
│   ├── urls.py              # Main URL configuration with Swagger setup
│   ├── wsgi.py
│   └── asgi.py
├── listings/                 # Listings app
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│   ├── urls.py
│   └── migrations/
├── venv/                     # Virtual environment (not tracked in git)
├── .env                      # Environment variables (not tracked in git)
├── .env.example              # Environment variables template
├── .gitignore                # Git ignore rules
├── requirements.txt          # Python dependencies
├── manage.py                 # Django management script
└── README.md                 # Project documentation
```

## Installation

### Prerequisites

- Python 3.8 or higher
- PostgreSQL 12 or higher
- pip (Python package manager)
- Virtual environment tool

### Setup Instructions

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/alx_travel_app.git
   cd alx_travel_app
   ```

2. **Create and activate virtual environment**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```

   Edit `.env` file with your configuration:
   ```
   SECRET_KEY=your-secret-key-here
   DEBUG=True
   DB_NAME=alx_travel_app_db
   DB_USER=postgres
   DB_PASSWORD=your_password
   DB_HOST=localhost
   DB_PORT=5432
   ```

5. **Create PostgreSQL database**
   ```bash
   psql -U postgres
   CREATE DATABASE alx_travel_app_db;
   \q
   ```

6. **Run migrations**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

7. **Create superuser (optional)**
   ```bash
   python manage.py createsuperuser
   ```

8. **Run development server**
   ```bash
   python manage.py runserver
   ```

The application will be available at `http://localhost:8000`

## API Documentation

Once the server is running, you can access the API documentation at:

- **Swagger UI**: http://localhost:8000/swagger/
- **ReDoc**: http://localhost:8000/redoc/
- **JSON Schema**: http://localhost:8000/swagger.json

## Configuration

### Environment Variables

The project uses `django-environ` for environment variable management. Key variables include:

- `SECRET_KEY`: Django secret key (required)
- `DEBUG`: Debug mode (True/False)
- `ALLOWED_HOSTS`: Comma-separated list of allowed hosts
- `DB_NAME`: PostgreSQL database name
- `DB_USER`: Database user
- `DB_PASSWORD`: Database password
- `DB_HOST`: Database host
- `DB_PORT`: Database port
- `CORS_ALLOWED_ORIGINS`: Comma-separated list of allowed CORS origins

### REST Framework Settings

Default configuration includes:
- Pagination: 10 items per page
- Authentication: Session-based
- Permissions: AllowAny (customize for production)

### CORS Configuration

CORS is configured to allow requests from:
- http://localhost:3000
- http://localhost:8000
- http://127.0.0.1:3000
- http://127.0.0.1:8000

Customize in `settings.py` for production environments.

## Development

### Running Tests

```bash
python manage.py test
```

### Creating a New App

```bash
python manage.py startapp app_name
```

Don't forget to add the app to `INSTALLED_APPS` in `settings.py`.

### Database Migrations

```bash
# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate

# Show migrations
python manage.py showmigrations
```

## Deployment

### Production Checklist

- [ ] Set `DEBUG=False` in production
- [ ] Change `SECRET_KEY` to a strong, random value
- [ ] Configure `ALLOWED_HOSTS` with your domain
- [ ] Set up proper database credentials
- [ ] Configure CORS origins for your frontend domain
- [ ] Set up static files serving
- [ ] Configure HTTPS
- [ ] Set up proper logging
- [ ] Use environment-specific settings

### Recommended Production Setup

- **Web Server**: Gunicorn or uWSGI
- **Reverse Proxy**: Nginx
- **Database**: PostgreSQL (managed service)
- **Static Files**: AWS S3 or similar
- **Environment**: Docker containers
- **Task Queue**: Celery with Redis

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Best Practices

- Always use virtual environments
- Never commit `.env` file or sensitive data
- Follow PEP 8 style guidelines
- Write tests for new features
- Document your API endpoints
- Use meaningful commit messages
- Keep dependencies up to date

## Troubleshooting

### Database Connection Issues

If you encounter database connection errors:
1. Ensure PostgreSQL is running
2. Verify database credentials in `.env`
3. Check if the database exists
4. Ensure PostgreSQL is listening on the correct port

### Import Errors

If you see import errors:
1. Ensure virtual environment is activated
2. Reinstall dependencies: `pip install -r requirements.txt`
3. Check Python version compatibility

## License

This project is part of the ALX Software Engineering program.

## Contact

For questions or support, please contact the ALX team.

## Acknowledgments

- ALX Africa for the project structure and requirements
- Django and Django REST Framework communities
- Contributors and maintainers

---

**Happy Coding!** ✨