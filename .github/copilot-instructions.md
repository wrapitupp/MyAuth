# MyAuth Codebase Instructions for AI Agents

## Project Overview

**MyAuth** is a Django 6.0.2 web application for authentication management. It's a straightforward Django project with a single app (`MyAuthApp`) using SQLite for data storage.

## Architecture

### Project Structure

```
MyAuth/                      # Main Django project directory
├── MyAuth/                  # Django configuration package
│   ├── settings.py         # Core Django settings (DEBUG=True, SQLite DB)
│   ├── urls.py             # Root URL configuration (admin only currently)
│   ├── wsgi.py             # WSGI application entry point
│   └── asgi.py             # ASGI application entry point
├── MyAuthApp/              # Main application
│   ├── models.py           # Database models (currently empty)
│   ├── views.py            # View functions/classes (currently empty)
│   ├── urls.py             # App-level URL routing (not yet created)
│   ├── admin.py            # Django admin configuration
│   ├── migrations/         # Database migration files
│   └── templates/          # HTML templates directory
├── manage.py               # Django management CLI
└── Pipfile                 # Python dependency management (Pipenv)
```

### Key Conventions

1. **Database**: SQLite (`db.sqlite3`) - not suitable for production
2. **Debug Mode**: `DEBUG = True` in settings - must be set to `False` for production
3. **Templates**: Django's built-in template engine (located in `MyAuthApp/templates/`)
4. **Authentication**: Uses Django's built-in `django.contrib.auth` app
5. **Admin Interface**: Enabled at `/admin/` route (no custom authentication frontend yet)

## Development Workflow

### Running the Development Server

```bash
# Activate Pipenv environment
pipenv shell

# Apply migrations
python manage.py migrate

# Start development server (default: http://localhost:8000/)
python manage.py runserver
```

### Database Migrations

- **Create migration** after model changes: `python manage.py makemigrations`
- **Apply migrations**: `python manage.py migrate`
- Migrations stored in `MyAuthApp/migrations/`

### Django Management Commands

- `python manage.py createsuperuser` - Create admin user
- `python manage.py shell` - Interactive Python shell with Django context
- `python manage.py test` - Run unit tests (from `MyAuthApp/tests.py`)

## Common Development Tasks

### Adding a New View

1. Define the view function/class in `MyAuthApp/views.py`
2. Import and add URL pattern to `MyAuthApp/urls.py` (if not exists, create it)
3. Include app URLs in root `MyAuth/urls.py` using `include()`

### Adding a New Model

1. Define the model in `MyAuthApp/models.py` with `django.db.models`
2. Run `python manage.py makemigrations`
3. Run `python manage.py migrate`
4. Register in `MyAuthApp/admin.py` for admin interface access

### Adding Templates

- Place HTML templates in `MyAuthApp/templates/MyAuthApp/` (Django convention)
- Use context processors in settings for template variables
- Render with `render(request, 'MyAuthApp/template_name.html', context)`

## Dependencies

- **Django 6.0.2**: Web framework (specified in Pipfile)
- **Python 3.14**: Required runtime version

## Critical Settings to Know

- `SECRET_KEY`: In development; must be environment variable in production
- `DEBUG = True`: Must be `False` in production
- `ALLOWED_HOSTS = []`: Must be configured with actual domain in production
- `INSTALLED_APPS`: Add new apps here after creating
- `STATIC_URL = 'static/'`: Static files configuration

## Next Steps for Development

1. Define authentication models (User extensions, roles, permissions)
2. Create views for login/registration workflows
3. Set up URL routing in `MyAuthApp/urls.py`
4. Create templates in `MyAuthApp/templates/`
5. Configure Django admin for model management
