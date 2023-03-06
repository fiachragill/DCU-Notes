
## Create a django project

In the terminal make sure you are in the repository folder you cloned from git and type

> `python -m django startproject labone`

This will create a new django project inside a folder called `labone` with a bunch of files in it (we’ll go through them in the lecture)

### Test out the server

Now we have enough to test if django is properly up and running, move inside the `Labone` folder (`cd labone` ) and type

> `python [manage.py](<http://manage.py>) runserver 0.0.0.0:8000` and in your browser go to `[<http://127.0.0.1:8000>](<http://127.0.0.1:8000>)` to view the default django page.

## Create an app

Django is useless without an app, this is where you write ******************your code****************** , you can call this anything you want, I will call it templates

Inside the terminal type

> `python [manage.py](<http://manage.py>) startapp templates`

This will create a new folder called `templates` containing your app - this folder is where we will be doing most of our development in

===================================================================

Finally we have to _install_ the app, under the backend folder open `[settings.py](<http://settings.py>)` and add your app to the `INSTALLED_APPS` list, your INSTALLED_APPS should look something like this

Finally we have to _install_ the app, under the backend folder open `[settings.py](<http://settings.py>)` and add your app to the `INSTALLED_APPS` list, your INSTALLED_APPS should look something like this

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'templates', #Replace with your app name
]
```

# Create a homepage

We want to create our first homepage in an app. In django we need three things to do this

-   a url - that our page can be reached at
-   A view - a function that loads our webpage for the user
-   A template - the actual HTML that can be provided to the user

Before we can do this we need a bit of setup

## Mapping the _projects_ urls to the _apps_ urls

> Inside your django application folder (the folder that contains `[models.py](<http://models.py>)` create a new file called `[urls.py](<http://urls.py>)`)

The next step is to link the django project urls to the app's urls. Inside the project [urls.py](http://urls.py) file (the folder with `asgi.py`) add a link to the apps [urls.py](http://urls.py)

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('', include('your_app_name.urls')),
    path('admin/', admin.site.urls),

```

## Create "Hello World" View

Inside your app folder create a new folder called `templates` - this is where we will store the HTML that will be shown to the user. (so inside our folder `templates` we should ahve another folder called `templates`

> Inside the `templates` folder create a new file called `index.html`

```html
<!-- index.html -->
<html>
	<head>Hello World</head>
	<body>
		<p>Hello world</p>
	</body>
</html>
```

### Create the view in [views.py](http://views.py)

Inside your `[views.py](<http://views.py>)` add in the code to display the webpage. This is the code that will be triggered when the user requests the homepage of our app. All it does is returns the `index.html` file we created to the user.

```python
from django.http import HttpResponse
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

### Create the url mapping

Inside `your_app_name/urls.py` create the url mapping

# Create our first model

In `[models.py](<http://models.py>)` inside your apps folder create a model called Book, remember the structure of a model is

```python
# This code is just an example, do not copy/paste
# Use this as a reference to create your model called Book !
class MyModel(models.Model):
   id = models.AutoField(primary_key=True)
   someattribute = models.TextField()
   another_field = models.CharField(max_length=10) # charfields have to have a max length
	 some_date = models.DateField()
   an_integer = models.IntegerField()
   a_decimal = models.DecimalField(max_digits=5, decimal_places=2) # number from 0.0-999.99
```

Your model Book should have the following fields:

-   id
-   year
-   author
-   price
-   title
-   synopsis

Look through the example above and the [Django model field reference](https://docs.djangoproject.com/en/4.1/ref/models/fields/#field-types) to create your model.

## Makemigrations & migrate

**Every time** a model in Django is changed we must

-   Save our [models.py](http://models.py) file
-   call `python [manage.py](<http://manage.py>) makemigrations` - to prepare the migration to the database
-   then call `python [manage.py](<http://manage.py>) migrate` - to add the model to our database

## Add to Admin interface

A model’s great, but without any actual data, it’s useless. We are going to add some data to our model using the Admin interface.

-   In `[admin.py](<http://admin.py>)` make sure your models are imported at the top of the file `from .models import *`
-   To make sure your model can be viewed in the admin interface add
-   `admin.site.register(YourModel)` - replace `YourModel` with the name of the model (_******class)******_ you created in `[models.py](<http://models.py>)`

## Create superuser

Before we can go to our admin interface we have to create a superuser account.

-   Call `python [manage.py](<http://manage.py>) createsuperuser` to create a superuser account
-   Follow the instructions
-   Go to [](http://127.0.0.1:8000/admin)[http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin) and sign in using your admin `username` (not the admin email address) and password.
  
## Page to view a single book

We are now going to create a page to view a single book. It would eb too much trouble to hardcode a url for each book individually, so we are going to use URL paths.

### View

In `[views.py](<http://views.py>)` create a function called `view_single_book` this function will take in the request as normal and an additional parameter called `bookid` representing the id of a single book.

```python
def view_single_book(request, bookid):
   
```

The code for this view will be

-   Load the book with the id `bookid` or return a 404 page
-   Pass the **********************individual********************** book to a template to display

To load an object or return a 404 page we will use the Django shortcut function `get_object_or_404`

The parameters f the function are

-   The object you are trying to get (a class defined in your `[models.py](<http://models.py>)` )
-   The filter= e.g. where `id=x`

We will then pass it to a page called `single_book.html` as a variable called `book`

```python
from django.shortcuts import get_object_or_404

def view_single_book(request, bookid):
	single_book = get_object_or_404(Book, id=bookid)
	return render(request, 'single_book.html', {'book':single_book})
```

### URL

Our URL is how we are going to pass `bookid` as a parameter into the function `view_single_book` to do this we will use [URL Paths](https://docs.djangoproject.com/en/4.1/topics/http/urls/#example)

Add the following to your `urlpatterns` in the `[urls.py](<http://urls.py>)` file in your app folder

```python
path('books/<int:bookid>', view_single_book, name='single_book')
```

Now `/books/1` will take us to a page containing the book with id 1 , `/books/2` for id 2 etc…

### Template

Create a file called `single_book.html` and copy the base template shown earlier [Url](https://www.notion.so/Url-94a266475532499abdf48e9982ee49a9)

In this case we are looing at a single variable called `book` is it not a list so no for loop is necessary

# Exercises

## Show info on a single book

Design the page `single_book.html` so that is shows all information about a single book.

Remember to print out a variable into a template you have to use `{{ }}`

e.g.

```python
<h3>{{ book.title }}</h3>
```

Will print out the title of a book inside a 3rd level heading tag

## Forms

To start with forms, inside your app folder (the same folder that contains `[views.py](<http://views.py>)` create a new file called `[forms.py](<http://forms.py>)`

Inside `[forms.py](<http://forms.py>)` add the following imports to the top of the file

```python
#imports for forms.py 
from django import forms
from .models import * # import all of your models
```

For these notes we will be looking at employees and departments with the following `[models.py](<http://models.py>)`

```python
from django.db import models

# Create your models here.

class Department(models.Model):
    id = models.AutoField(primary_key=True)
    name = models.TextField()
    address = models.CharField(max_length=10)

    def __str__(self):
        return "{} - {}".format(self.address, self.name) # self.address + " - " + self.name
    

class Employee(models.Model):
    id = models.AutoField(primary_key=True)
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
    department = models.ForeignKey(Department, on_delete=models.CASCADE)
```

## Form to create a new instance of a model

To make a form that is tied to a model we created in `[models.py](<http://models.py>)` we need

-   a form in `[forms.py](<http://forms.py>)`
-   a view in `[views.py](<http://views.py>)`
-   a url in `[urls.py](<http://urls.py>)`
-   a template to show the form in our templates folder

### [forms.py](http://forms.py)

```python
# example code for forms.py do not copy/paste
# form to create a new employee
# Remember the imports for forms.py <https://www.notion.so/scrineym/Week-4-No-Lab-Forms-Exercises-Notes-300b698993bf47799c801bca7d14228d#2bb18f5c0e234895a0258a13e42f371c>
class Employeeform(forms.ModelForm):
	class Meta:
		model = Employee # picked up from importing models.py
		# list of strings representing the attributes of the model Employee 
		#    that we want a user to be able to enter
    # e.g. we do not list the attribute 'id' here because we don't want a user to see that on the form
		fields = ['first_name','last_name','department'] 
```

### [urls.py](http://urls.py)

There’s nothing special about the URL to display a form, it is the same as showing any other page for our app

```python
path('createemployee',views.create_employee, name='create_employee')
```

### v[iews.py](http://Views.py)

Our view is now a bit different, we need to have three conditions handled

-   The user wants to view the form
-   The user has filled in the form and we want to save it
-   The user has filled in the form, but it contains errors and we need to show it back to them

```python
def create_employee(request):
    if request.method == "POST":
				# create a new copy of the form with the data the user 
				# entered , it is stored in request.POST
        form = EmployeeForm(request.POST)
        if form.is_valid():
            emp = form.save() # create the Employee object and save it
						# send the user to a confirmation page saying
						# confirming that they filled in the form and the data was saved 
            return render(request, 'created.html', {'emp':emp})
        else:
						# form has errors
						# send the form back to the user
            return render(request, 'create_emp.html', {'form': form})
    else:
        # normal get reuqest, user wants to see the form 
        form = EmployeeForm()
        return render(request, 'create_emp.html', {'form': form})
```

### template

The code to display most forms is pretty much the same, we need to wrap it in a `<form>` tag and add a submit button.

We need to make sure we add a `[csrf](<https://owasp.org/www-community/attacks/csrf>)`token.

```python
<!-- create_emp.html -->
{% extends 'base.html' %}

{% block content %}
    <form action="" method="POST">
        {% csrf_token %}
        {{ form.as_table }}
        <button type="submit">Create Employee</button>
    </form>
{% endblock %}
```

We also need a simple confirmation page

```python
<!--created.html-->
{% extends 'base.html' %}
{% block content %}
    Employee created {{emp}} 
{% endblock %}
```

## Custom form validation + error messages

To add in custom validation we just need to override the forms `clean`method, the view, url and template from before do not need to be changed

```python
# forms.py 
class Employeeform(forms.ModelForm):
	class Meta:
		model = Employee # picked up from importing models.py
		fields = ['first_name','last_name','department']

	def clean(self):
		# all fields are stored in self.cleaned data 
		# this is a dictionary containing the fields we defined in the "Meta" class
    # and the values the user entered
		data = self.cleaned_data
		first_name = data['first_name']
		last_name = data['last_name']
		department = data['department']
		# Once we extract all the data here we can do any rules we may need
		# e.g. check if an employee with that name already exists
		# we add .exists at the end of a query to check and see if anything matches that filter criteria
		employee_exists = Employee.objects.filter(first_name=first_name, last_name=last_name).exists()
		if employee_exists:
			# if there is an error , raise it as a validation error
			raise forms.ValidationError("An employee of that name already exists")
		elif:
			# another check
		elif
			# another ...etc		
		return data # always return self.cleaned_data at the end of clean
			
```

## Form to edit an existing instance of a model.

To edit an existing object in a form all we need to do is change the url and view to allow us to select individual objects.

This is a very similar approach to creating a page to view a single object.

### [urls.py](http://urls.py)

We need a URL that takes in an id which allows us to select an individual object

```python
path('updateemployee/<int:empid>',views.update_employee, name='update_employee')
```

### [views.py](http://views.py)

Most of the work is done inside our [views.py](http://views.py) method where we load the id we need and use it as a base to create our form using the `instance` parameter when creating our form

We can use the same form template used before to display our form

```python
from django.shortcuts import render, get_object_or_404

def update_employee(request, empid):
	employee = get_object_or_404(id=empid) # load the employee object
	if request.method=="POST":
		form = EmployeeForm(request.POST, instance=employee)
		if form.is_valid():
			form.save() # update our employee
			# redirect to a simple page confirming update was successful
			return render(request, 'update_confirmation.html', {'emp':employee})
		else:
			
			return render(request, 'create_emp.html.html', {'form':form})
	else:
		form = EmployeeForm(instance=employee)
		return render(request, 'create_emp.html.html', {'form':form})
```

## Form with additional workflow

Sometimes after creating a form we don’t want to save it instantly, or we want to add in additional steps into the create process. To do this we edit our function in [views.py](http://views.py) to prevent saving the form until we choose using the `commit=False` parameter in the `save`method

e.g.

```python
def create_employee(request):
    if request.method == "POST":
				# create a new copy of the form with the data the user 
				# entered , it is stored in request.POST
        form = EmployeeForm(request.POST)
        if form.is_valid():
            emp = form.save(commit=False) # create the Employee object and don't save it yet
						## other steps go here possibilities include
							# creating other objects
							# editing attributes of employee
						emp.save() # finally save the employee object
            return render(request, 'created.html', {'emp':emp})
        else:
						# form has errors
						# send the form back to the user
            return render(request, 'create_emp.html', {'form': form})
    else:
        # normal get reuqest, user wants to see the form 
        form = EmployeeForm()
        return render(request, 'create_emp.html', {'form': form})
```

## Custom form not tied to a model

Finally, sometimes we need a form but do not want it to be tied to a model

In these cases we can create our own forms using `forms.Form`

[Django](https://docs.djangoproject.com/en/4.1/topics/forms/#building-a-form-in-django)

```python
class NonModelForm(forms.Form):
    name = forms.CharField(max_length=6, widget=forms.TextInput(attrs={'id':'myid', 'class':'some-class'}))
```

# Exercises

## Setup

Create a new folder in your repo called `Lab_4` and copy the code from `Lab_3` into it.

We will be adding forms onto the bookshop created last week

## Form to create new book

Create a form that allows a user to add a new book.

When creating a book add the following validation rules

-   A book of the same title doesn’t already exist
    
-   The year the book is published cannot be in the future
    
    -   You can get the current year using the `datetime` library
    
    ```python
    from datetime import datetime
    current_datetime = datetime.now()
    current_year = current_datetime.year
    ```
    

## Form to edit an existing book

Create a form that allows you to edit an existing book

## Checkout book form

This form will

-   Show the details of an individual book (like the last exercise)
-   When the form is submitted, check
    -   There is enough inventory to allow a user to check out the book
        -   (i.e. inventory ≠ 0)
    -   Then create a new borrow object (can be tied to the user with the id=1) representing the book that was borrowed.
        -   Assume the due date is the current datetime + 1 week see the following link on how to add to dates/times in python

