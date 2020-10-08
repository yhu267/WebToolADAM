# WebToolADAM
## Yicheng Hu yhu267@wisc.edu

### Environment: 
-	Python3.7 required 
-	Django 2.0+
-	Django-background-tasks 1.2.5 https://django-background-tasks.readthedocs.io/en/latest/#
-	Django-extensions 3.0.8 https://django-extensions.readthedocs.io/en/latest/#
-	Django-MySQL 3.8.1 https://django-mysql.readthedocs.io/en/latest/
-	Django-storages (optional) 1.10.1 https://django-storages.readthedocs.io/en/latest/

### Database setup:
-	MySQL: create a database (‘adam’ by default)
-	MySQL: create a user who has all privileges to ‘adam’
-	If not using MySQL, make sure the database has a module in Django which supports storing python lists (for MySQL, please see https://django-mysql.readthedocs.io/en/latest/index.html)

### Optimization setup:
-	Download and install Julia (version 1.1 recommended, https://julialang.org/downloads/oldreleases/)
-	Install Julia package JuMP, Clp, and Cbc by running: 
$ julia
julia> using Pkg; 
julia> Pkg.add(“JuMP”);
julia> Pkg.add(“Clp”);
julia> Pkg.add(“Cbc”);
-	Take a record of the path to Julia. 

### Modify settings.py
-	If not host on AWS, deactivate line 14: 
#from ADAM.aws.conf import *
Otherwise set up AWS keys and s3
-	Replace the Django security key with a random string including 50 characters in line 24
-	Add hosts in line 29: 
ALLOWED_HOSTS = ['127.0.0.1', 'localhost'] # add any other applicable address 
-	Edit line 83-93: Enter the database name (‘adam’ by default), username, password, and host. MySQL is used during the development of ADAM.
-	Edit line 155-160: Enter email host, email user and password. Outlook email is used during the development. 

### Change settings in other scripts (sorry for not using a global variable):
-	ADAM/ADAM/views.py line 224-235, change the email setting
-	ADAM/main/tasks.py line 16-21, change the email setting
-	ADAM/check.py line 57-61, 98-102, change the email setting 
-	ADAM/check.py line 38, change the path to Julia result folder
-	ADAM/main/tasks.py line 40, include the path to Julia here 
-	ADAM/croncheck, change the path to ADAM here 

### Load project and run:
-	$ python manage.py migrate
-	$ python manage.py runserver 8000
-	Open another screen and start to process background tasks: 
$ python3 manage.py process_tasks
-	Put the croncheck file into crontab to check model status periodically: 
$ crontab croncheck

### Create an adminnuser: 
-	Please follow steps here https://docs.djangoproject.com/en/1.8/intro/tutorial02/
