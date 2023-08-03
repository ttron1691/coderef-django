# coderef-django
## Install the Django package via pip
```Shell
python -m pip install Django
```
## Create new Django Project
Start a new django project via the following command in 
```Shell
django-admin startproject [PROJECT-NAME]
# Example
django-admin startproject myproject
```
This gives you the following structure of files
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```
## Create a new app
Create a new app within the existing Django project
```Shell
python manage.py startapp [APP-NAME]
# Example
python manage.py startapp myapp
```
which results in the following file structure
```
myapp/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
    [urls.py]
```
It is good practice to add a separate urls.py file for each app. 
## Run development server
In order to start the build-in development webserver use the following command
```Shell
python manage.py runserver [URL]
# Example
python manage.py runserver 0.0.0.0:8000
```
The corresponding website will be accessible by default under the following URL
```
http://localhost:8000
```
with port number 8000.
## Create templates

## Create static files
