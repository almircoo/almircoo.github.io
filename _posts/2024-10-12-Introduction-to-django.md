---
title: Set up Django project
author: Jesus Almirco
date: 2024-12-10 14:10:00 +0800
categories: [Django, Set Up]
tags: [Django]
render_with_liquid: false
---
# Django Setup Guide

This guide will help you set up a Django project from scratch.

---

## Prerequisites

Make sure you have the following installed:

- Python (3.12 or later is recommended)
- pip (Python package manager)
- Virtualenv (optional but recommended)
- PostgreSQL (for production, if required)
- SQLite (default for development)

---

## Steps to Set Up a Django Project

### Install Django

#### Create and Activate a Virtual Environment

```bash
# Create a virtual environment
python3 -m venv env

# Activate the virtual environment (MacOS/Linux)
source env/bin/activate

# Activate the virtual environment (Windows)
.env\Scripts\activate
```

#### Install Django

```bash
pip install django
```

---

### Create a Django Project

```bash
django-admin startproject project_name
cd project_name
```

---

### Run the Development Server

To verify that Django is installed and working:

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your web browser. You should see the Django welcome page.

---

### Configure Database Settings

By default, Django uses SQLite. To use PostgreSQL or another database, edit `settings.py`:

#### Example Configuration for PostgreSQL:

Install the PostgreSQL driver:
```bash
pip install psycopg2
```

Modify `DATABASES` in `settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_database_name',
        'USER': 'your_username',
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

Apply migrations to set up the database schema:

```bash
python manage.py migrate
```

---

### Create a Superuser

Create an admin user to access the Django admin panel:

```bash
python manage.py createsuperuser
```

Follow the prompts to set up the username, email, and password.

---

### Add an App

#### Create a New App

```bash
python manage.py startapp app_name
```

#### Register the App

Add the app to the `INSTALLED_APPS` list in `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'app_name',
]
```

---

### Configure Static and Media Files

#### Static Files

Add the following to `settings.py`:

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
STATIC_ROOT = BASE_DIR / 'staticfiles'
```

Collect static files:

```bash
python manage.py collectstatic
```

#### Media Files

Add the following to `settings.py`:

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

Update `urls.py` to serve media files in development:

```python
from django.conf import settings
from django.conf.urls.static import static

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

### Set Up Git (Optional)

#### Initialize Git

```bash
git init
git add .
git commit -m "Initial commit"
```

#### Create a `.gitignore` File

```bash
touch .gitignore
```

Add the following to `.gitignore`:

```
*.pyc
__pycache__/
.env
/staticfiles/
/media/
```

---

### Deploy to Production

For deploying to production, consider using:

- **PostgreSQL** as the database
- **Gunicorn** as the WSGI server
- **Nginx** for serving static files
- **Docker** for containerization

---

## Additional Resources

- [Django Documentation](https://docs.djangoproject.com/en/stable/)
- [Django Tutorials](https://www.djangoproject.com/start/)
- [Virtualenv Documentation](https://virtualenv.pypa.io/en/stable/)

