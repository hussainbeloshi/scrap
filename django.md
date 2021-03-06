# NEW DJANGO PROJECT

1. Create new virtual environment: ```virtualenv env```
2. Activate the VR: Windows: ```/env/Scripts/activate```, for Mac: ```/env/bin/activate```
3. Install Django on the VR: ```pip install django```
4. Start new Django project: ```django-admin startproject NAME```
5. Create new folders for the statics ```static``` and for the templates ```temp```, and then place all the statics (e.g. ```.css``` and ```.js```) in the static folder, and the templates ```.html``` in the temp folder.
6. Create a new Django application: ```django-admin startapp NAME```
7. Call the new app from the Django project settings (PROJECTNAME/settings.py). Add new line (e.g. ```APP NAME``` in the ```INSTALLED_APPS```
9. Create a ```urls.py``` in the app directory, and write the following:
```
from django.urls import path
from . import views


urlpatterns = [
    path('', views.home, name='index'),
]
```

10. 

#################
enviroment and django
#################


\env\Scripts\activate.bat
pip install django
\myProject\django-admin startproject myProject
django-admin startapp index

put all template files in static folder

create floder for template and put htmls inside it

SETTINGS:
INSTALLED_APPS = [ 'appname',

create urls.py in the app:
put -> 
from django.urls import path
from . import views

urlpatterns = [
    path('/', views.home, name='home'),

]

in the urls.py from main:
path('', include('index.urls')),

in the views.py:
from django.shortcuts import render
from django.http import  HttpResponse

# Create your views here.

def home(request):

    return HttpResponse("hello");


[os.path.join(BASE_DIR, 'template')]
STATICFILES_DIRS = [
        os.path.join(BASE_DIR, 'static_in_env'),
]
VENV_PATH = os.path.dirname(BASE_DIR)
STATIC_ROOT = os.path.join(BASE_DIR, 'static_root')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(VENV_PATH, 'media_root')

URLS:
from django.conf import settings
from django.conf.urls.static import static
if settings.DEBUG:
    urlpatterns += static(settings.STATIC_URL,
                          document_root=settings.STATIC_ROOT)
    urlpatterns += static(settings.MEDIA_URL,
                          document_root=settings.MEDIA_ROOT)

python manage.py makemigrations
python manage.py migrate
python manage.py runserver


after making statics

python manage.py collectstatic

python manage.py startapp post
pip install pillow => to work with images

