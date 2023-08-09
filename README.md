# Code Reference for Django
## Install the Django package via pip
```Shell
python -m pip install Django
```
## Check Version
```Shell
python -m django --version
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
myproject/
    manage.py
    myproject/    
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
myproject/
    manage.py
    myproject/    
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
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
We add a separate "urls.py" for each app
## Migrate
In order to migrate changes with respect to the database we can run
```Python
python manage.py migrate
```
## Django admin site
We can crate a superuser which is acting as an admin for the website
```Shell
python manage.py createsuperuser
```
The superuser is able to login to the admin platform which is available under the following URL
```
[URL]:[PORT]/admin
# Example
0.0.0.0:8000/admin
```
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
with the default development webserver port number 8000.
## URLS
As already mentioned, it is good practice to add a separate urls.py file for each app. The corresponding file "myapp/urls.py" may look as follows
```Python
from django.urls import path, include
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```
The global project "myproject/urls.py" file looks as follows
```Python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include("myapp.urls")),
]
```
For each app we include the corresponding "urls.py" file within the app directory.
## Views
### Method based views
We add the following content to "myapp/views.py" in order to serve the templates
```Python
from django.shortcuts import render

def index(request):
    return render(request, "myapp/index.html", {})
```
### Class based views
## Templates
It is good practice to create a base html template "templates/myapp/base.html" and derive all other template files. A basic index html website "myapp/templates/myapp/index.html" can then be created as follows
```html
{% extends 'myapp/base.html' %}

{% block title %}
Index
{% endblock %}

{% block content %}
<div class="container">
</div>
{% endblock %}
```
## Forms
### Form validation
We may validate a given form as follows within a defined method in "views.py"
```Python
from django.shortcuts import render
from .forms import MyForm

def form_validation(request):
    if request.method == "POST":
        form = MyForm(request.POST)
        if form.is_valid():
            form.save()
            return render(request, "template_redicted.html", {})
    else:
        form = MyForm()
        return render(request, "template_form.html", {"form": form})
```
## Static files
If we want to serve static files (e.g. css styles, images) we can create a separate static directory for each app analogously to the templates directory. For instance, we want to include additional style files "static/myapp/my_style.css", we can refer to this style file as follows
```HTML
{% load static %}
<link rel="stylesheet" href="{% static 'myapp/my_style.css' %}">
```
The same is true for images, e.g. if we consider an image "static/myapp/img1.png", we can serve the image via
```HTML
{% load static %}
<img src="{% static 'myapp/img1.png' %}" alt="My image">
```
