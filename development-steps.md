# Sign In using google auth in django
Tutorial link: https://www.youtube.com/watch?v=yO6PP0vEOMc&t=204s 

## Create virtual environment

```bash
python -m venv env
```

## Activate the environment

```bash
source env/bin/activate
```

## Install django

```bash
pip install django
```

## Create django project

```bash
django-admin startproject googlelogin
```

## Create an users app

```bash
cd googlelogin
python manage.py startapp users
```

## Add the app to settings.py

googlelogin -> settings.py -> INSTALLED_APPS

## Setup Google Auth in Google Console

### Get the credentials

## Add SITE_ID for your site in settings.py

```python
SITE_ID = 2
```

## Install django-allauth

```bash
source ../env/bin/activate
pip install django-allauth
```

## Add the below apps in INSTALLED_APPS of settings.py

```python
'django.contrib.sites',
'allauth',
'allauth.account',
'allauth.socialaccount',
'allauth.socialaccount.providers.google'
```

## Add variables and scopes for social account in settings.py

```python
SOCIALACCOUNT_PROVIDERS = {
    'google': {
        'SCOPE': {
            'profile',
            'email',
        },
        'AUTH_PARAMS': {'access_type': 'online'}
    }
}
```

## Add Authentication backends in end of settings.py

```python
AUTHENTICATION_BACKENDS = {
    'django.contrib.auth.backends.ModelBackend',
    'allauth.account.auth_backends.AuthenticationBackend'
}
```

## Add Redirect URLS in settings.py

```python
LOGIN_REDIRECT_URL = '/'
LOGOUT_REDIRECT_URL = '/'
```

## Add urls in urls.py of main app

```python
path('accounts/', include('allauth.urls')),
path('', include('users.urls'))
```

## Create urls.py in users app

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home),
    path('logout', views.logout_view)
]
```

## Create views in users.views.py

```python
def home(request):
    return render(request, 'home.html')


def logout_view(request):
    logout(request)
    return redirect('/')
```

## Create templates folder in the root folder and create home.html.

## Apply migrations

```bash
source ../env/bin/activate
python manage.py migrate
```

## Add template location in settings.py

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': ['templates'],
    }
]
```

## Add staticfiles and media location in settings.py and

```python
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

## Run collectstatic command

```bash
python manage.py collectstatic
```

## Create Superuser

```bash
python manage.py createsuperuser
```

## Runserver

```bash
python manage.py runserver
```

## Create social application in django via admin panel

### Go to /admin and login and add a site
For local setup add 'http://127.0.0.1:8000'

### Add social app by adding client id and secret id
