# Connecting a Neon.tech hosted PostgresSQL to your Django App

![Neon](https://dfv3qgd2ykmrx.cloudfront.net/assets/media/modules/shared/assets/images/logo-686db0deced8ef91c7c583768df939a6.svg)

## Overview

This is a quick walkthrough the steps necessary for creating and connecting an online PostGreSQL database using a website called [Neon.tech](https://neon.tech/)

## Getting Started

- Sign Up for an account if you do not have one. (It is quick and easy to use GitHub)
![Imgur](https://i.imgur.com/GIdFpgcl.png)
- Click on create new project located under the banner with the elephant
![Imgur](https://i.imgur.com/f3gyP7Fl.png)
- Enter a project name, select the Postgres Version and a region near you. Then click the blue 'Create project' button.
![Imgur](https://i.imgur.com/4EWI144l.png)
- You will see the following screen. Click on the dropdown under the words connect using on the left.
![Imgur](https://i.imgur.com/obbBKnwl.png)
- Select Django and it will generate the code you need to add to the `settings.py` file.
![Imgur](https://i.imgur.com/bLhpspYl.png)

## Connecting your Django App


Copy the DATABASES code block you are given from [Neon.tech]() and store it somewhere for now. 

This code block contains information you need to connect your Django app to your online database. This information should be considered a secret you do not want to post visibly on the internet. 

It is a good habit to store this in a `.env` file and access it from there. 

Here are the steps you need to take to access the .env variables in your Django App:

### <b>1. Install Django Environ</b>

In your terminal, inside the project directory type:

```shell
pip install django-environ
```

### <b>2. Import environ in setting.py</b>

Place this toward the top of the file.

```python
import environ
```
### <b>3. Initialize environ</b>

Initialize the environment variables under the imports.

```python
import environ
# Initialize environment variables
env = environ.Env()
environ.Env.read_env()
```

### <b>4. Create your .env file</b>

In the same directory as your `settings.py`, create a file called `.env`

### <b>5. Declare your environment variables in .env</b>

Using the information which Neon.tech provided in code block it automatically generated for Django earlier, place it into your `.env` to match the following code block. Make sure you do not use quotations around strings nor the angle brackets.

```shell
SECRET_KEY=<Whatever you want it to be>
DATABASE_NAME=neondb
DATABASE_USER=<Your neon username>
DATABASE_PASS=<The password provided by neon>
DATABASE_HOST=<The host provided by neon>
DATABASE_PORT=<Port provided by neon>
```
### <b>6. IMPORTANT: Add your .env file to .gitignore</b>

If you do not have a .gitignore file yet, create one in the project root directory. Make sure the `.env` file is included.

If you are unsure what other file types belong in the `.gitignore`, visit [this link](https://www.toptal.com/developers/gitignore/api/python) for a sample.

### <b>7. Replace all references to your environment variables in settings.py</b>

```python
DATABASES = {
'default': {
'ENGINE': 'django.db.backends.postgresql',
'NAME': env('DATABASE_NAME'),
'USER': env('DATABASE_USER'),
'PASSWORD': env('DATABASE_PASS'),
'HOST': env('DATABASE_HOST'),
'PORT': env('DATABASE_PORT')
}
}
```

And 

```python
SECRET_KEY= env('SECRET_KEY')
```

### <b>8. Migrating to your online Database</b>

Once you've edited the DATABASES in your `settings.py`file you will need to migrate everything to this new database.

To do that, open up a terminal in the proper folder and run:

```sh
python3 manage.py migrate  
```

After this completes, to spin up your app, just run:

```sh
python3 manage.py runserver
```

To open your app in your browser, <kbd>command</kbd> + click on the "Local:" URL in your terminal or just go to [http://127.0.0.1:8000/](http://127.0.0.1:8000/).

## Recap

That's it! That's all you need to do to host a postgresql database online! You can see the data on the dashboard similar to MongoDB Atlas. This site also lets you share you database access with others on your team.

## Resources

- [Neon.tech](https://neon.tech/)
- [Neon.tech Django docs](https://neon.tech/docs/guides/django)
- [Setting up env variables in Django](https://alicecampkin.medium.com/how-to-set-up-environment-variables-in-django-f3c4db78c55f)
- [Default .gitignore for Django](https://www.toptal.com/developers/gitignore/api/python)