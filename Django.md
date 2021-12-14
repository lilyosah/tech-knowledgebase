# Django
%%
#coding 
#concept

**Related:**
-  [[Model-View-Controller (MVC)]]
-  [[Rails Views]]
-  [[Rails Models]]
-  [[Rails Controllers]]
-  [[Rails Routing]]

%%
https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Models

## Structure
Follows MVT (Model View Template). Like [[Model-View-Controller (MVC)]]

| Rails      | Django   |
| ---------- | -------- |
| Model      | Model    |
| Controller | View     |
| View       | Template |

### Views 
Receive HTTP requests from web clients and return HTTP responses. This can involve getting/manipulating database info, rendering templates, etc.
- All views receive an `HttpRequest` object as a parameter and returns an `HttpResponse` object.

**Ex: ✏**  
```Python
# filename: views.py (Django view functions)

from django.http import HttpResponse

def index(request):
    # Get an HttpRequest - the request parameter
    # perform operations using information from the request.
    # Return HttpResponse
    return HttpResponse('Hello from Django!')
```

#### Filtering Model Data
- After importing the model, use `[model].objects.filter()` to query for data
- Field name and match type are separated by double underscores 

**Ex: ✏**  
```Python
## filename: views.py

from django.shortcuts import render
from .models import Team

def index(request):
    list_teams = Team.objects.filter(team_level__exact="U09")
    context = {'youngest_teams': list_teams}
    return render(request, '/best/index.html', context)
```

### Models
Define structure of stored data, including field types and other restrictions. 

**Ex: ✏**  
```Python
# filename: models.py

from django.db import models

class Team(models.Model):
	# team name is a character field w/ 40 max chars
    team_name = models.CharField(max_length=40)

	# levels can be one of several values so it's a choice field, 
	# TEAM_LEVELS maps data to be stored and choices to be displayed
    TEAM_LEVELS = (
        ('U09', 'Under 09s'),
        ('U10', 'Under 10s'),
        ('U11', 'Under 11s'),
        ...  #list other team levels
    )
	#u11 is default
    team_level = models.CharField(max_length=3, choices=TEAM_LEVELS, default='U11')
```

### Templates
Django has native templating and supports Jinja2

**Ex: ✏**  
```HTML
## filename: best/templates/best/index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Home page</title>
</head>
<body>
  {% if youngest_teams %}
    <ul>
      {% for team in youngest_teams %}
        <li>{{ team.team_name }}</li>
      {% endfor %}
    </ul>
  {% else %}
    <p>No teams are available.</p>
  {% endif %}
</body>
</html>
```

## Routing
URL Mapping is done in `urls.py`. A URL mapper is a list of `paths` or `re_paths` (use [[Regular Expressions]]) that represent URL patterns and corresponding view functions. 

Within the URL, angle brackets define parts of the URL that are captured and passed to the function as named args. 

The second list item is a function that will be called when the pattern is matched. `views.book_detail` means that the `book_detail()` method can be found in a module (file) called `views`.

**Ex: ✏**  
```Python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('book/<int:id>/', views.book_detail, name='book_detail'),
    path('catalog/', include('catalog.urls')),
    re_path(r'^([0-9]+)/$', views.best),
]
```

## Virtual Environments
Should develop in a Python virtual env to ease differences between platforms. 
[Helpful set-up guide](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/development_environment)

📝 Had to install virtualenvwrapper-win through pip after opening command prompt as admin

Useful commands: 
- `mkvirtualenv [name]` creates and switches to env
- `deactivate` exits env 
- `workon` lists envs
- `workon [name]` switches to that env 

## Using
1. To create a new project: `django-admin startproject [name]` 
2. To create an app within the project: `py manage.py startapp [name]`
3. To start the webserver: Be in the right env and directory of project, `py manage.py runserver
4. Add app to the project in `settings.py`
5. Set up URLS
6. Make migration files `python manage.py makemigrations`
7. Run migrations `python manage.py migrate`


## Forms
## User Auth and permissions
## Caching
So that you can cache parts of a rendered page so that it doesn't get re-rendered unless necessary
## Admin site
## Serialising Data
Data can be serialised as JSON