#### Create virtual environment
- to into the folder
- create and activate the virtual environment (deactivate)
```
PS> python -m venv venv
PS> venv\Scripts\activate
PS> deactivate
```
#### Create and manage the requirements in the virtual environment ([pip_freeze](https://stackoverflow.com/questions/6590688/is-it-bad-to-have-my-virtualenv-directory-inside-my-git-repository))
````
python -m pip freeze > requirements.txt
````
## Notes on django
- start a project
````
PS> django-admin startproject name_of_the_project
````
- migrations
````
PS> python3 manage.py makemigrations
PS> python3 manage.py migrate
````
- run the website locally (more [info](https://docs.djangoproject.com/en/4.0/ref/django-admin/#runserver)), find the website under http://127.0.0.1:8000/
````
PS> python3 manage.py runserver
````
- create a superuser
````
PS> python3 manage.py createsuperuser
````
- query from the command prompt

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
    template_name = "page_name.html"      # this value defaults to "modelclass_detail.html"
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

## Admin website
Register in admin.py the models you want to access via the admin website
````
admin.site.register(ModelName)
````
