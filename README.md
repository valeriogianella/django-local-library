# django_local_library
Local Library Website

# notes on django
## Views

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
