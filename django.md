# NEW DJANGO PROJECT

1. Create new virtual environment: ```virtualenv env```
2. Activate the VR: Windows: ```/env/Scripts/activate```, for Mac: ```/env/bin/activate```
3. Install Django on the VR: ```pip install django```
4. Start new Django project: ```django-admin startproject NAME```
5. Test the localhost by using this command: ```python manage.py runserver```
6. Create new folders for the statics ```static``` and for the templates ```temp```, and then place all the statics (e.g. ```.css``` and ```.js```) in the static folder, and the templates ```.html``` in the temp folder.
7. Create a new Django application: ```django-admin startapp NAME```
8. Call the new app from the Django project settings (```PROJECTNAME/settings.py```). Add new line (e.g. ```APP NAME``` in the ```INSTALLED_APPS```
9. Create a ```urls.py``` in the app directory, and write the following:
```
from django.urls import path
from . import views


urlpatterns = [
    path('', views.home, name='index'),
]
```

10. Go to the ```urls.py``` of the project files, and write the following:
```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    
    path('', include('index.urls')),
    path('admin/', admin.site.urls),
    
]
```

11. Add the following in the ```views .py``` (for testing only, and then we will change the ```HttpResponse``` to ```render```): 
```
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
    return HttpResponse("test");
```

12. Test the localhost by using this command: ```python manage.py runserver```
13. Go to the (```PROJECTNAME/settings.py```), and add the following line on the top of the page: ```import os```
14. Call the templates and the statics from the (```PROJECTNAME/settings.py```) by add the following in the ```TEMPLATES``` ```'DIRS':```:
```
'DIRS': [os.path.join(BASE_DIR, 'temp')],
```

15. Go to ```views.py``` file in the app directory, and change the ```HttpResponse``` in the ```def``` to ```render```, to be like the following:
```
def home(request):
    return render(request, "index.html");
```

16. On the buttom of the file, next to the ```STATIC_URL = '/static/'```, add the following lines: 
```
MEDIA_URL = '/media/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
VENV_PATH = os.path.dirname(BASE_DIR)
STATIC_ROOT = os.path.join(VENV_PATH, 'static_root')
MEDIA_ROOT = os.path.join(VENV_PATH, 'media_root')
```

17. Now collect the statics by using the following command: ```python manage.py collectstatic```
18. Create ```base.html``` ```head.html``` ```nav.html``` in the ```temp``` directory
19. Go to the ```index.html``` and cut the ```<head>``` and paste it in the ```head.html```, and the ```<!-- Navigation -->``` and paste it in the ```nav.html```
20. Add ```{% load static %}``` on the top of all the html pages.
21. Add the following in the ```base.html``` file:
```
<!DOCTYPE html>
<html>

{% include "head.html" %}

    <body>
    {% include "nav.html" %}

    {% block content %}
    {% endblock content %}

    </body>

</html>
```
22. for the ```index.html``` page, add the following on the top of the page:
```
{% extends 'base.html' %}
{% block content %}
{% load static %}
```
and the following on the bottum of the page:
```
{% endblock content %}
```
23. Call the static files (```.css``` and ```.js```) by using Jinja syntax before the static path, e.g.:
```
{% static 'vendor/jquery/jquery.min.js' %}
```


## CREATE DATABASE (SQLITE3)

1. Go to the ```settings.py```, and find: ```DATABASES = {```. To be as the following:
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

2. Go to the ```models.py``` and add class that you want for your app. E.g.:
```
from django.db import models

class Text(models.Model):
    title = models.CharField(max_length=50)
    source = models.CharField(max_length=50)
    img = models.ImageField()
    quote = models.TextField()
    speaker = models.CharField(max_length=50)

    def __str__(self):
        return self.title
```

3. Install Pillow for the images: ```python -m pip install Pillow```
4. Create super user to log in the admin panel ```/admin```: ```python manage.py createsuperuser```
5. Go to ```admin.py``` and add the following:
```
from django.contrib import admin
from .models import Text

admin.site.register(Text)
```
