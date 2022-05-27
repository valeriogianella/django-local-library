# django-local-library
Local Library Website

# Notes on django
To start a project
````
django-admin startproject locallibrary
````
## Commands from the powershell
### Migrations
````
python3 manage.py makemigrations
python3 manage.py migrate
````
### Run the website locally
More informations under [https://docs.djangoproject.com/en/4.0/ref/django-admin/#runserver]
````
python3 manage.py runserver
````
### Create a superuser
````
python3 manage.py createsuperuser
````
### Make queries from the command prompt
Run servers - import object - run queries (? am I missing something ?)

## Views

### Forms
Print form errors: print(form_name.errors)

### Model based views
#### single model views

````
from django.views import generic
...
class CustomClassName(generic.DetailView):
    model = ModelClass
    template_name = "page_name.html"      # this valued defaults to "modelclass_detail.html"
````
in the urls page add the corresponding reference, i.e.
````
path("modelclass/<int:pk>", views.CustomClassName.as_view(), name="modelclass-detail"),
````
````
from django.views.generic.edit import CreateView, DeleteView, UpdateView
...

````
#### list view

When creating a model based vied specify the model you are referring to, e.g.
```
from django.views import generic
...
class CustomClassName(generic.ListView):
    model = ModelClass
    paginate_by = 10      # number of elements per page
    template_name = "page_name.html"      # if not specified it result in "modelclass_list.html"
```
in the urls page add the corresponding reference, i.e.
````
path("modelclass[pluralized]/", views.CustomClassName.as_view(), name="modelclass[pluralized]")
````

## Login
The integrated authentication system is added with the service
````
urlpatters += [path('accounts/', include('django.contrib.auth.urls')),]
````
which adds the following urls
````
accounts/ login/ [name='login']
accounts/ logout/ [name='logout']
accounts/ password_change/ [name='password_change']
accounts/ password_change/done/ [name='password_change_done']
accounts/ password_reset/ [name='password_reset']
accounts/ password_reset/done/ [name='password_reset_done']
accounts/ reset/<uidb64>/<token>/ [name='password_reset_confirm']
accounts/ reset/done/ [name='password_reset_complete']
````
A rudimental login can be implemented in a html page as follows
````
<!DOCTYPE html>
<html lang="en">
<head></head>
<body>
    <h1>Authentication</h1>
<form method="post" action="{% url 'login' %}">
    {% csrf_token %}
    <table>
        <tr>
            <td>Username:</td>
            <td><input id="username" type="text" name="username"></td>
        </tr>
        <tr>
            <td>Password:</td>
            <td><input id="password" type="text" name="password"></td>
        </tr>
    </table>
    <input type="submit" value="login" />
    <input type="hidden" name="next" value="{{ next }}" />
</form>
</body>
</html>
````
## Settings
For date format: DATE_FORMAT in settings file, e.g. 
````
DATE_FORMAT = "l j/n/Y"
USE_L10N = False (otherwise the date format is determined by this)
````
