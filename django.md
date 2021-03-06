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

11. Test the localhost by using this command: ```python manage.py runserver```
12. Call the templates and the statics from the (```PROJECTNAME/settings.py```) by add the following in the ```TEMPLATES``` ```'DIRS':```:
```
'DIRS': [os.path.join(BASE_DIR, 'temp')],
```
