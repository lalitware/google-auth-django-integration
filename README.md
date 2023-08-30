# Google OAuth integration with django

## Steps for setup on local.

### Create virtual environment

```bash
python -m venv env
```

### Fork the repo and then clone it on local using terminal

```bash
git clone {your_repo.git}
cd {project_directory}
```

### Activate the environment

```bash
source ../env/bin/activate
```

### Install all the dependencies

```bash
pip install -r requirements.txt
```

### Setup Google Auth in Google Console

#### Create a project visit https://console.cloud.google.com/

#### Set the scope to profile and email

#### add the below URIs

http://127.0.0.1:8000
http://127.0.0.1:8000/accounts/google/login/callback/
http://localhost:8000/accounts/google/login/callback/

#### Get the credentials json file which has client id and client secret in it

## Apply migrations

```bash
source ../env/bin/activate
python manage.py migrate
```

## Create Superuser

```bash
python manage.py createsuperuser
```

### Create SITE_ID for your site in settings.py
http://127.0.0.1:8000

```python
SITE_ID = 2
```

### Create social application in django via admin panel

Use client id and clent secret mentioned in .json file that we downloaded from google console.

### Runserver

```bash
python manage.py runserver
```
