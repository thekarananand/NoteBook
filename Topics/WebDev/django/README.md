``` bash
django-admin startproject core .
```

``` bash
python manage.py startapp invoices
```

``` bash
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include("invoices.urls"))
]
```

``` bash
python manage.py startapp api
```
