# 🏆 Auto deploy Django projects on Heroku using GitHub repository - (🔥🔥 tutorial )

Original Written For Medium 

Link : https://medium.com/@abdullah-mughal/auto-deploy-django-projects-on-heroku-using-github-repository-6ff170598a8b

This article addresses followings

-   Create a simple django project    
-   Add dependency and modify configuration for CI/CD (Heroku)    
-   Upload project on git repository    
-   Create app on Heroku server    
-   Configure git repo with heroku    
-   Set pipeline for auto deployment on Heroku server for each git push
      

Without further ado

  

# 0. What’s It About

This tutorial focuses on django’s deployment on Heroku. We are using github as our code repository. Whenever code is updated our project on heroku is updated.

## 0.1 Django

Django is a high-level Python web framework that enables rapid development of secure and maintainable websites

## 0.2 Github

GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

  

## 0.3 Heroku

Heroku is a platform as a service (PaaS) that enables developers to build, run, and operate applications entirely in the cloud.

## 0.4 Code Repo

Code is hosted on [https://github.com/iAbdullahMughal/djheroku_project](https://github.com/iAbdullahMughal/djheroku_project)

Heroku app is running on [https://djheroku-project.herokuapp.com/](https://djheroku-project.herokuapp.com/)

# 1. Django Project & App

## 1.1 Preparing Environment

### 1.1.1 Python version

Let’s start by checking the version of python, I am currently working with python3 (version 3.10.0). You can check the version by entering the python -V  command on the terminal / console.

  

```shell
C:\Users\abdullah\python>python -V  
Python 3.10.0
```

  

### 1.1.2 Creating virtual environment

Execute python -m venv env  command on terminal to create a virtual environment. This command will create a virtual environment in the current directory location.

```shell
C:\Users\abdullah\python>python -m venv env
C:\Users\abdullah\python>dir
 Volume in drive C has no label.
 Volume Serial Number is 8C8F-7182

 Directory of C:\Users\abdullah\python

16/12/2021  08:53 PM    <DIR>          .
16/12/2021  08:53 PM    <DIR>          ..
16/12/2021  08:53 PM    <DIR>          env
               0 File(s)              0 bytes
               3 Dir(s)  72,877,871,104 bytes free

```

  

### 1.1.3 Activate virtual environment

After creating a virtual environment, execute the following commands to activate the virtual environment.

  

-   Windows OS command env\Scripts\activate
    
  


```shell
C:\Users\abdullah\python>env\Scripts\activate
(env) C:\Users\abdullah\python>
```
  

-   Linux OS command source env/bin/activate
    

  


```shell
source env/bin/activate
(env) $
```

  

We are working on windows os, commands will be same on linux machine.

## 1.2 Install Django

### 1.2.1 Installing django package using pip

Execute python -m pip install django command in terminal and install django in newly created virtual environment.

  
```shell
(env) C:\Users\abdullah\python>python -m pip install django
Collecting django
  Downloading Django-4.0-py3-none-any.whl (8.0 MB)
     |████████████████████████████████| 8.0 MB 22 kB/s
Collecting asgiref<4,>=3.4.1
  Using cached asgiref-3.4.1-py3-none-any.whl (25 kB)
Collecting tzdata
  Downloading tzdata-2021.5-py2.py3-none-any.whl (339 kB)
     |████████████████████████████████| 339 kB 20 kB/s
Collecting sqlparse>=0.2.2
  Using cached sqlparse-0.4.2-py3-none-any.whl (42 kB)
Installing collected packages: tzdata, sqlparse, asgiref, django
Successfully installed asgiref-3.4.1 django-4.0 sqlparse-0.4.2 tzdata-2021.5
WARNING: You are using pip version 21.2.3; however, version 21.3.1 is available.
You should consider upgrading via the 'C:\Users\abdullah\python\env\Scripts\python.exe -m pip install --upgrade pip' command.

(env) C:\Users\abdullah\python>

```

## 1.3 Setting Up Django Project

### 1.3.1 Strat Project

Once the django library is installed we can create a django project by using command django-admin startproject djheroku_project you can use your own project name instead of djheroku_project.

  ```shell
  **(env) C:\Users\abdullah\python>django-admin startproject djheroku_project  
  
(env) C:\Users\abdullah\python>**
```

  

Following will be the structure of djheroku_project after executing the command.
```shell
(env) C:\Users\abdullah\python>tree djheroku_project /A /F
Folder PATH listing
Volume serial number is 8C8F-7182
C:\USERS\ABDULLAH\PYTHON\DJHEROKU_PROJECT
|   manage.py
|
\---djheroku_project
        asgi.py
        settings.py
        urls.py
        wsgi.py
        __init__.py


(env) C:\Users\abdullah\python>

```

  

### 1.3.2 Run Django Project

Execute python djheroku_project\manage.py runserver command to check django project is running successfully.

  
```shell
(env) C:\Users\abdullah\python>python djheroku_project\manage.py runserver
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
December 16, 2021 - 21:50:16
Django version 4.0, using settings 'djheroku_project.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.


```

  

### 1.3.3 Django Project Web Interface

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) in the browser to check if the django project is installed successfully.

![](https://lh5.googleusercontent.com/CAGihr1leElmLiQEsH5pLucvFKdAydzKet8DQ2CLPHyyMbbpIO8-Z_M42eGw-A2aUeMIDEi-EaGTMspF5oHBYrp_PXw9zuJzif0PMpqZ78NaexrkqmIHK1nMxTzUX9AnPrI-ZZEj)

### 1.3.4 Creating Django App

Let's change the directory and move into the newly created project’s directory and execute python manage.py startapp example command in the root of django start project. You can use your own app name instead of an example.

  
```shell
(env) C:\Users\abdullah\python>cd djheroku_project

(env) C:\Users\abdullah\python\djheroku_project>python manage.py startapp example

(env) C:\Users\abdullah\python\djheroku_project>

```

Following is structure of example app
```shell
(env) C:\Users\abdullah\python\djheroku_project>tree example /A /F
Folder PATH listing
Volume serial number is 00000066 8C8F:7182
C:\USERS\ABDULLAH\PYTHON\DJHEROKU_PROJECT\EXAMPLE
|   admin.py
|   apps.py
|   models.py
|   tests.py
|   views.py
|   __init__.py
|
\---migrations
        __init__.py


```

### 1.3.5 Configure App with Project

Open settings.py file Django Project’s root directory and add app name example in INSTALLED_APPS list.

```python
# Application definition
 
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'example',
]

```
 

### 1.3.6 Configuration View In Visual Studio Code

Following image showing settings.py and added configuration in file to integrate django app with django project.

![](https://lh6.googleusercontent.com/rAev5lZ_OdfD7pPoovQ69tKmjb3nLAeagLissNJGPjW_qau7IZksw7lZl92_1hb765Hxjgc0Z1GBgXBrGJfNOKZn8N72jiMTr2ePrnrSnzS1q2c_kAclNBEZEAT5xsqRh4ZrjHgn)

  
  

## 1.4 Modifying App For Static Resource Usage

To make things more clear I will be adding an image, css file in the app's html home page. You can extend it by adding multiple resources as per need so the following are additions in code.

  

1.4.1 Addition of Index.html in templates

-   Created a folder named templates in example app folder
    
-   Added an index.html file in templates folder
    

  

djheroku_project/example/templates/Index.html
```html
{%load static%}
<html>
<head>  
    <!-- for html code page & css check https://codepen.io/Sonick/pen/HthaI -->
    <meta charset="utf-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover"/>
    <meta http-equiv="X-UA-Compatible" content="ie=edge"/>
    <meta http-equiv="Content-Language" content="en"/>
    <meta name="msapplication-TileColor" content="#206bc4"/>
    <meta name="theme-color" content="#206bc4"/>
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"/>
    <meta name="apple-mobile-web-app-capable" content="yes"/>
    <meta name="mobile-web-app-capable" content="yes"/>
    <meta name="HandheldFriendly" content="True"/>
    <meta name="MobileOptimized" content="320"/>
    <title>Simple Django, Heroku Tut Using Github Repo</title>
    <link rel="stylesheet" type="text/css" href='{% static "css/style.css" %}'>
    <style>
        body {
            background: #310404 url('{%static "images/maxresdefault.jpg"%}')no-repeat center center fixed;
        }
        </style>
</head>
<body>
    <div class="sp-container">
        <div class="sp-content">
            <div class="sp-globe"></div>
            <h2 class="frame-1">AWESOME</h2>
            <h2 class="frame-2">DJANGO PROJECT WITH GITHUB REPO</h2>
            <h2 class="frame-3">RUN WITH HEROKU</h2>
            <h2 class="frame-4">TEST IT!</h2>
            <h2 class="frame-5">
                <span>FORK,</span>
                <span>CHANGE,</span>
                <span>EXPERIENCE.</span>
            </h2>            
        </div>
       
    </div>    
   
</body>
</html>

```

  
  

1.4.2 Addition of image & css file

-   Created a folder named static in example app folder
    
-   Added two more folders named as css & images, both folders contain a css file and an image file which are used in index.html.
    

  

1.4.3 Adding View For Index Template

I am adding function views.py in an example app to render a template upon request.

  

djheroku_project/example/views.py

  
```python
from django.shortcuts import render
 
# Create your views here.
def homepage_view(request):
    return render(request=request, template_name="index.html")
```
  

1.4.4 Adding Url Config For Index View

To view the index.html, we need to configure the url in urls.py so that we can show our template upon the url hit. For basic understanding I have configured the index template on default address.

  

djheroku_project/djheroku_project/urls.py
```python
from django.contrib import admin
from django.urls import path
from example.views import homepage_view
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', homepage_view, name="homepage"),
]

```
  

1.5 Django Project & App Ready

Our single page django app is ready upon python manage.py runserver following can be observed on the web browser.

![](https://lh5.googleusercontent.com/t8ypyBDry42vsvznh_zV2ubzxXlO35AHxE_LmVOashw7DRDmolKu1FsVXiWqC8i_Mzs8cHxXYoDbHFETdGMgTDsIT3LF7q_aCcH1WMOeG_gtUaYaq8kqWjpzn-zN_7rbSUWVmSDN)

## 1.5 Freezing Requirements

Now execute python -m pip freeze > requirements.txt  command to pin all used dependencies

```shell
(env) C:\Users\abdullah\python\djheroku_project>python -m pip freeze > requirements.txt  
  
(env) C:\Users\abdullah\python\djheroku_project>
```


# 2. Github Repo

## 2.1 Install Git & create account on github

Just click sign up and it will guide you, verify your account. Lets move to next step (it’s free)

  

## 2.2 Create A Repository

-   Click on New repository
    

![](https://lh4.googleusercontent.com/xSHlyN7Dsc6Y7YBdeQ-5KfJ4prWl20dSAYyhCRBjzHVWwuf-Z2uGuIWWMWpfB8LWVeBhjQ3EW3pZAI4QvsUeu3UBI9A_4ncuQ_sfxtTrT7dunyfUMLOYmdRBSV_kjSwit8SIn3td)

  

-   Provide a Repository name and hit Create Repository.
    

![](https://lh6.googleusercontent.com/vzZt_mBaxFRPEZGIRfo-k_YX1o5RHgd2epMWBfyF7Kg22WS7yTGhrAeQoE46JShkrTLibkrbxmRjlRTN0P5oyDStRcPYh2chLzI_O_TsXxGkiRGkCxwqpxkcGvJZndJTuOQYt8vE)

-   Once repository is created we can push our code in it.
    

![](https://lh6.googleusercontent.com/Ls0oK3PcG3uQ2hFCFAuXu67KExOGLw54g1fUCOOKXEiF9r3nC4Maq0OFX5af3mFeUZ6IWPxuSen8qTGxEGeZPBe2leYp8jP_6T3vkivpAhnfLazbOpBy6akY-IfXJf7T6zdDv7JR)

  

## 2.3 Add SSH / GPG Keys in you git account

Follow official github guide https://docs.github.com/en/authentication/managing-commit-signature-verification

## 2.4 Commit local code and push on github

1.  Come to project’s root folder and enter git init
    
```shell
(env) C:\Users\abdullah\python\djheroku_project>git init
Initialized empty Git repository in C:/Users/abdullah/python/djheroku_project/.git/

(env) C:\Users\abdullah\python\djheroku_project>
```

2.  Execute git add . command on project’s root folder
    
```shell
(env) C:\Users\abdullah\python\djheroku_project>git add .

(env) C:\Users\abdullah\python\djheroku_project>
```
  

3.  Add commit using git commit -m "initial commit"
    
```shell
(env) C:\Users\abdullah\python\djheroku_project>git commit -m "initial commit"
[main (root-commit) b612cb9] initial commit
 29 files changed, 778 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 db.sqlite3
 create mode 100644 djheroku_project/__init__.py
 create mode 100644 djheroku_project/__pycache__/__init__.cpython-310.pyc
 create mode 100644 djheroku_project/__pycache__/settings.cpython-310.pyc
 create mode 100644 djheroku_project/__pycache__/urls.cpython-310.pyc
 create mode 100644 djheroku_project/__pycache__/wsgi.cpython-310.pyc
 create mode 100644 djheroku_project/asgi.py
 create mode 100644 djheroku_project/settings.py
 create mode 100644 djheroku_project/urls.py
 create mode 100644 djheroku_project/wsgi.py
 create mode 100644 example/__init__.py
 create mode 100644 example/__pycache__/__init__.cpython-310.pyc
 create mode 100644 example/__pycache__/admin.cpython-310.pyc
 create mode 100644 example/__pycache__/apps.cpython-310.pyc
 create mode 100644 example/__pycache__/models.cpython-310.pyc
 create mode 100644 example/__pycache__/views.cpython-310.pyc
 create mode 100644 example/admin.py
 create mode 100644 example/apps.py
 create mode 100644 example/migrations/__init__.py
 create mode 100644 example/migrations/__pycache__/__init__.cpython-310.pyc
 create mode 100644 example/models.py
 create mode 100644 example/static/css/style.css
 create mode 100644 example/static/images/maxresdefault.jpg
 create mode 100644 example/templates/index.html
 create mode 100644 example/tests.py
 create mode 100644 example/views.py
 create mode 100644 manage.py
 create mode 100644 requirements.txt
```
  
  

Execute git push command to push code in github

  
```shell
(env) C:\Users\abdullah\python\djheroku_project>git push --set-upstream origin main
Enumerating objects: 38, done.
Counting objects: 100% (38/38), done.
Delta compression using up to 4 threads
Compressing objects: 100% (34/34), done.
Writing objects: 100% (38/38), 44.45 KiB | 3.17 MiB/s, done.
Total 38 (delta 2), reused 0 (delta 0), pack-reused 0
```
  

# 3. Heroku Cloud

## 3.1 Setting Up Heroku App

### 3.1.1 Create account on Heroku

Create a new account on Heroku cloud using their official guide, remember it’s free

[https://signup.heroku.com/](https://signup.heroku.com/)

### 3.1.2 Login & Access Dashboard

Now login into your heroku account and open [https://dashboard.heroku.com/apps](https://dashboard.heroku.com/apps).

### 3.1.3 Create an app

-   Click on new & then click on Create new app
    

![](https://lh5.googleusercontent.com/kIF7kEd7EZyovFikBMTK6SHmacG3GnAVw9aAspIvdjdOK-_FzpAyyf9LryBlje-A1G6PW5_e2_JSg6XI77kV4fM9J1GXA100hqxphQMADzauqog2WJ2NAZiQMWKUKo4xIJQhF-CW)

-   Provide app name and click on Create app
    

  

![](https://lh3.googleusercontent.com/2NJEtPUfZibfM5ZmpbI60vDsMt0fm9_I3CMlRRbKrHWVRmvfygAsGB6Blc5i-DC9gXXHIdd-oYTM1SmyzN8cnvFKSBor_07rh4n8P_xAt5CsG-3aQ84diEb4txEX7iyNcGxC1Kq_)

-   Once the app create you will be redirected to the app's dashboard.
    

### 3.1.4 Connect Github with Heroku

-   Click on Github button in front of Deployment method
    
-   Once dropdown menu is opened click on Connect to Github
    

![](https://lh4.googleusercontent.com/TAHeNekolRMtqUK-BZDWOUB47uqxamDRvkxmBBr2T8fWgXGaoNuDHgYh7hJmi-SxGSFkmqj3tliISXTE3CRDjwn2y3dgdoazTd1k1LobY6Xz2-Dbg-su6xhS6YbQnDrWyMbMEuov)

-   Allow app to access your github public repositories.
    

  

### 3.1.5 Connect Github Repo with Heroku App

-   Once github is configure, search your repo, once repository is listed press connect button.
    

![](https://lh6.googleusercontent.com/jCvqLHWq5eN_57srwZ9LRw_f7IHGy76be8iQkICMh76vVVf_33_lbwRCDijUX1cIMMZ5kODYwl0oqOHLKscnpFzVT2eduYzXuYp459kym-Un4sLWNiwUwztGD1Q3qY77gcEjdLEe)

-   Now click on Enable Automatic Deploys and select the branch that you want to deploy. For the tutorial I am leaving the main deploy branch. Press Deploy Branch.
    

![](https://lh3.googleusercontent.com/YpbgdeJwu_4FXu7ljeD5XQJ1cNJHP7Z3xmnaDpdaKkahTudKMiQGooAZlp6ivJhosJzIM_N-_5B1_4jVSVMAvXTYO8fK9pXUmCmM9hn1u2iRKm-NcARthNhPHhfrTHixjv4zYOdf)

### 3.1.5 Heroku app failed to deploy (Expected)

-   Our first Deploy will be failed and following error will appear on Heroku logs.
    

![](https://lh5.googleusercontent.com/iFSvLiAxSM0_yvgebyw6rAj_x3CXcNzzfjiPs3eoyH4YYPBfcHrUuc6IDDvAkd-LDcTpWkifMNvbUWaUcr0psH4kQ2-m-kfLFnyRy3XH_AKSqvqqlHQFttQAWrwOaeIJjG_j8gGK)

-   Now we need some tweaks in our django project to make it compatible with Heroku cloud.
    

  

## 3.2 Django & Heroku Configuration Dependencies

### 3.2.1 Additional dependencies

We need to add & install gunicorn, whitenoise and django-heroku in requirements.
```shell
python -m pip install gunicorn
python -m pip install whitenoise
python -m pip install django-heroku
```
    

  

After adding these dependances our requirements.txt looks like this

```
asgiref==3.4.1
dj-database-url==0.5.0
Django==4.0
django-heroku==0.3.1
gunicorn==20.1.0
psycopg2==2.9.2
sqlparse==0.4.2
tzdata==2021.5
whitenoise==5.3.0
```

### 3.2.2 Modifying settings.py

After adding these dependencies we need to update some configurations in settings.py

  
```python
STATIC_URL = 'static/'
 
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```

  

Adding following settings after STATIC_URL for handling static files.

  

### 3.2.3 Adding static folder in project root

To make heroku copy static files like images, js, css we will create a folder in project root.

This folder will contain an empty file with .keep name, so the folder can be stored on git and copied on heroku cloud.

![](https://lh4.googleusercontent.com/n_mlee9iF4Onz61WkQ8mfmyvjG7kWeyZcdA2cXfyksUyHo622lsiv6RO0Npn6HH60lQRkMcI0EIy8PO6uBfGsFeOTu52xFafxUqIBMX31T67O0vWwJY0EStE_Hm2atsOj_96qC-R)

  

### 3.2.4 Adding Procfile

We will add an additional file named Procfile, although heroku knows our application is django python but we will add this file to guide Heroku worker to perform actions as per our instructions and requirements.

  

Content of Procfile

``web: gunicorn djheroku_project.wsgi``

  
  

### 3.2.5 Git add and pushing to main branch
```shell
(env) C:\Users\abdullah\python\djheroku_project>git add .

(env) C:\Users\abdullah\python\djheroku_project>git commit -m "Adding support for heroku cloud"
.
.
Files List
.
.
(env) C:\Users\abdullah\python\djheroku_project>git commit -m "Adding support for heroku cloud"
(env) C:\Users\abdullah\python\djheroku_project>git push --set-upstream origin main

```

  

### 3.2.6 Successful Deployment

-   After adding heroku related configuration our build was successful.
    

![](https://lh4.googleusercontent.com/-oTY17gvSKMeG0lr-C-S-40oQSlzjKnN8rp0wxV_fxAzd8CRtEUAw6J8icNPXmv5qlzAjdVo3yGPTFvLXjPf8ws0VVqMBp_38k9Oo15TJHvhz9643IYTLS_CFgFFKuDnUAkySqEp)

# 4. Django App Running On Heroku Cloud

![](https://lh5.googleusercontent.com/VBeO2XYfPIospHdzaUSkC39-8rasMefa5-I_cnbZGrphG3mzAfA5oOxddJOZUKgqZ1KyMb1kGaFXgZMqxVM5is86kOwd-5FU5SFRmPKgNaWy2-514-ZiHVDDKfLMfeZOqjTa8Zot)

  

Our django based simple application is now live at [https://djheroku-project.herokuapp.com/](https://djheroku-project.herokuapp.com/).

  

## 4.1 Isn’t it fun

Go ahead, build and deploy your django app free on heroku server.

  

I hope this article has helped you to learn something new, if I have missed anything or you need more help feel free to post questions or send DMs.

  

Hmmm some notes ,

1.  This tutorial is intended to show how to configure django, heroku and github
    
2.  Please make sure that your app and data is secure, if not please secure it accordingly
    
3.  Whole article is for educational purposes.