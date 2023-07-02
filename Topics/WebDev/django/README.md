# django

### Install Django
``` bash
pip3 install django
```

### Create a Django Web Server
``` bash
django-admin startproject <P_NAME>
```

### Start Server
``` bash
python3 manage.py runserver
```

stdout >>

```
...
Django version <SomeThing>, using settings '<P_NAME>.settings'
Starting development server at <Local Server URL>
Quit the server with CONTROL-C.
```

- this gives the URL for the Django Server. 

---

## Setting up a Web App

### <u>Step 1</u> : Create a Web App in a Django Project
``` bash
python3 manage.py startapp <APP_NAME>
```

### <u>Step 2</u> : Install the Web App into the ZDjango Project
in `<P_Name>/settings.py` file, add `<APP_NAME>` as a string element in `INSTALLED_APPS` list
``` Python
...
INSTALLED_APPS = [

    '<APP_NAME>',
    
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
...
```

### <u>Step 3</u> : Defining `Views.py` for `<APP_NAME>`

in `<APP_NAME>/views.py` file

``` Python
# Added by default
from django.shortcuts import render

# Added by me
from django.http import HttpResponse

# Create your views here.
def index(request):
    return HttpResponse("Hello, world!")
```

- Essentially, we are creating a Module, containing specified function add a dynamic nature to the Web App 

### <u>Step 4</u> : Adding URL Configuration for Installed Web App

**Step 1**: Create `urls.py` file in `<APP_NAME>` directory, add
APP_NAME
``` Python
from django.urls import path

# To add function form views.py
from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```

**Step 2**: in `<P_Name>/urls.py` file, Add a path entry for `<APP_NAME>/urls.py`. Import `include()`

``` Python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('<Path_for_<APP_NAME>>/', include("<APP_NAME>.urls"))
]
```

---

## Adding a Subdirectory Path 

### Step 1 : Path Entry
Inside the `urls.py` file of `<APP_NAME>` directory, add the `path()` entry with the subdirectory name

``` Python
from django.urls import path

# To add function form views.py
from . import views

urlpatterns = [
    path("", views.index, name="index"),
    path("karan/", views.karan, name="karan"),
]
```

### Step 2 : Create the Function in views.py
Inside `<APP_NAME>/views.py` file
``` Python
...
def karan(request):
    return HttpResponse("Hello, Karan Boss!")
...
```

---

## Input from Path

In the above example, I tried to make a special path to a webpage that justs greet me, but if we want to greet everyone (or essentially every sub-path), we can do the following:

### Step 1 : Path to Variable
We can add `urlpatterns` entry in `<APP_NAME>/urls.py`

``` Python
from . import views

urlpatterns = [
    path("", views.index, name="index"),
    path("<str:Name>", views.greet, name="greet"),
]
```

Now, this will take the subpath in a variable `Name`, and pass it to a function `greet()` defined in the `./views.py`

### Step 2 : Creating `greet()` function
Inside `<APP_NAME>/views.py` file
``` Python
...
def greet(request, Name):
    return HttpResponse(f"Hello, {Name}")
...
```

---

## HTML as Template
Although, entire HTML can be inserted into `HttpResponse()` function but that make the project quite tedious. So, we can use HTML page as a template and use functions in `view.py` file to fill necessary changes in HTML. 

### Step 1 : Create a HTML template
Create `<APP_NAME>/templates/<PAGE_Name>/index.html` file & it's Parent Directories.
``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Random Page</title>
</head>
<body>
    <h1>Hi, {{ Name }}!!</h1>
</body>
</html>
``` 
here,
- `{{ Name }}` is a Variable for Django's HTML Template.
- We can also integrate CSS and JS in `<PAGE_NAME>` directory

### Step 2 : Create a Function in `views.py`
``` Python 
def greet(request):
    return render(request, "<PAGE_NAME>/index.html", { 
        "Name": Name.capitalize()
    })
```
here, `render()` is taking:

1. `request`
2. Path to HTML Template
3. Variables in Dictionary

### Conditions

``` HTML
<body>
    {% if bool_variable %}
        <h1>True</h1>
    {% else %}
        <h1>False</h1>
    {% endif %}
</body>
```

### for Loops

``` HTML
<body>
    {% for x in sequence_variable %}
        <h1>x</h1>
    {% endfor %}
</body>
```

### Adding HTML Via Views.py into HTML TEMPLATE

``` HTML
<body>
    {{ Content|safe }}
</body>
```

``` Python
def RenderPage(request):
        return render(request, "page.html", {
        "Content": "<h1>HEllo!</h1>"
})
```

## Static Files
While making a WebApp, we prefer to have a centralized location for static files like `.css` file, `.js` file or Other Assets.

### Step 1 : Place the Static files to `<APP_NAME>/static/<PAGE_NAME>/` 

### Step 2 : Add following to the top of the Template
```
{% load static %}
```

### Step 3 : Add links to the Assets (Wherever Required) in following format
``` 
" {% static %} '<PAGE_NAME>/PATH/ASSET' "
```

---

## Template Inheritance 

In a WebApp, Generally, we have a lot of HTML content like `<head>` common across all the pages. To Avoid Copy-Pasting, we can use HTML Templates Inheritance.

### Step 1 : Create a Layout 
Create `Layout.html` file in `<APP_NAME>/templates/<PAGE_NAME>` dir

``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Todo App</title>
</head>
<body>
    {% block <NAME> %}
    {% endblock %}
</body>
</html>
```
here,
``` HTML
    {% block <NAME> %}
    {% endblock %}
```
represents as the position where the block of named `<NAME>` will go.

### Step 2 : Adjust other pages
Remove the HTML defined in the `Layout.html` file from all the pages of your WebApp & just keep the necessary bits of code enclose within a block

**PAGE1.html**
``` HTML
{% extends "<PAGE_NAME>/layout.html" %}

{% block Body %}
    <h3> This is Page 1</h3>
{% endblock %}
```

**PAGE2.html**
``` HTML
{% extends "<PAGE_NAME>/layout.html" %}

{% block Body %}
    <h3> This is Page 2</h3>
    <p>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do.
    </p>
{% endblock %}
```

here,
- `{% extends "<PAGE_NAME>/layout.html" %}` line links the html page to its layout.html

---

## Connecting Pages 
Although we can Copy-Page links into the Pages to connect them, but, Theirs a better way........

`urls.py` file of this WebApp
``` Python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.page1, name="Page1"),
    path("page2", views.page2, name="Page2")
]
```

`views.py` file of this WebApp
``` Python
from django.shortcuts import render

# Create your views here.

def page1(request):
    return render(request, "<PAGE_NAME>/PAGE1.html")
    
def page2(request):
    return render(request, "<PAGE_NAME>/PAGE2.html")
```

Now, We can Add links to the HTML pages

### Step 1 : Defining `app_name` in `urls.py`

We need to define a variable `app_name = "<APP_NAME>"` inside `urls.py file` to avoid namespace conflicts.

``` Python
from django.urls import path
from . import views

app_name = "<APP_NAME>"

urlpatterns = [
    path("", views.page1, name="Page1"),
    path("page2", views.page2, name="Page2")
]
```

### Step 2 : Add Links to the HTML Pages

**PAGE1.html**
``` HTML
{% extends "<PAGE_NAME>/layout.html" %}

{% block Body %}
    <h3> This is Page 1</h3>

    <a href="{% url '<APP_NAME>:Page1' %}">Go to Page 2</a>
{% endblock %}
```

**PAGE2.html**
``` HTML
{% extends "<PAGE_NAME>/layout.html" %}

{% block Body %}
    <h3> This is Page 2</h3>
    <p>
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do.
    </p>

    <a href="{% url '<APP_NAME>:Page2' %}">Back to Page 1</a>
{% endblock %}
``` 

