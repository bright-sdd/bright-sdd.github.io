---
layout:     post
title:      'Setting up a sample Django Project with PostgreSQL'
date:       2020-09-09 0:00:00
author:     'bright-sd'
permalink:  /:title/
category:   'Django'
---

This tutorial deals with setting up a sample Django Project with PostgreSQL and not with real basics of Python or Django.

### *Okay, let's start*

# **Installing PostgreSQL:**

* Search PostgreSQL on google and download it for your OS. (I'm using windows)
* Install PostgreSQL.
* Use the search bar to search pgAdmin and open it.
* It opens up in your browser.
* Create a new server and a new database, name the database 'BookDb' or anything you want.
* You'll need the ENGINE, NAME, USER, PASSWORD, HOST, PORT values later so have them ready.

# **Setting up a new Django Project:**

* Zeroth things zeroth, have Python 3.7 or something installed, explaining how to do that is outside the scope of this tutorial.
* Install Pycharm or any IDE, have a virtualenv set up.
* You'd be building a sample project for book management, we'll be performing crud operations from the django admin site.
* Firstly, Create a new Pycharm project named 'BookDb' or anything you want.
* Then, start a new terminal window, we need to run some commands.

### **Installing Django and PostgreSQL driver:**

Run the following command in the terminal:

`pip install django psycopg2`

### **Creating the Django Project:**

Run the following command in the terminal:

`django-admin startproject bookdb .`

This creates the project.

### **Creating the books app:**

Then, create an app. A project can have multiple apps which can be reused in different projects.

Run the following command in the terminal:

`python manage.py startapp books`

This creates the books app.

### **Creating the Book model:**

This is how your books/models.py should look:

```python
from django.db import models


class Book(models.Model):
    name = models.CharField(max_length=255)
    author = models.CharField(max_length=255)
```

### **Adding the books app to settings.py:**

Add this to the list of INSTALLED_APPS in settings.py:
`'books.apps.BooksConfig'`

### **Creating the BookAdmin**:

This is how your books/admin.py should look:

```python
from django.contrib import admin
from .models import Book


class BookAdmin(admin.ModelAdmin):
    list_display = ('name', 'author')


admin.site.register(Book, BookAdmin)
```

### **Setting the DATABASES dict in settings.py:**

This is how DATABASES in settings.py should probably look:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'Bookdb',
        'USER': 'postgres',
        'PASSWORD': 'admin',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

### **Running migrations:**

Run the following commands in the terminal:

`python manage.py makemigrations`

`python manage.py migrate`

### **Running the project:**

Run the following command in the terminal:

`python manage.py runserver`

### **Creating a superuser:**

Start a new terminal window.

Then, create a superuser using which you can login to the admin site from where you can perform CRUD operations.

`python manage.py createsuperuser`

It asks for a username, email address and password. Enter anything you like(and remember the username and password). If it says your password doesn't meet the required validations, just press y.

### **Logging in to the admin site using the created superuser:**

You can see all books, add a new book, update an existing book, delete a new book from there and see the changes being reflected in the PostgreSQL database. 

### *Thank you, that's it for this tutorial.*