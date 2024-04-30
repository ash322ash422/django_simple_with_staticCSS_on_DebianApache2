# django_simple_with_staticCSS_on_DebianApache2
 
NOTE: I used virtual env. with python interpreter=python3.11 on VSCode IDE.

Steps on how to create this simple app:
1) Open  the terminal and at the prompt, type "python -m pip install -r .\requirements.txt".
 To freeze -> ..\django_simple_with_staticCSS_on_DebianApache2> python -m pip freeze > requirements.txt

2) At the prompt, type "django-admin startproject mysite". (This creates a django project called 'mysite'.) At the prompt, type "cd mysite". This would take you inside 'mysite' directory.

3) At the prompt, type "python manage.py migrate". This would create some predefined admin apps that are very helpful.

4) At the prompt(in dir mysite), type "django-admin startapp notes".

..\django_simple_with_staticCSS_on_DebianApache2\mysite> django-admin startapp notes

 Make appropriate changes to notes/{urls.py,views.py,/templates/notes/{index.html..}, /static/notes/{css/,img/,js/} }. 

5) At the prompt(in dir mysite), type "django-admin startapp blog".
    Make appropriate changes to blog/{urls.py, views.py, templates/blog/index.html}, etc...

6)  Go to mysite/settings.py and make appropriate changes (i.e. create ../settings/{base.py,production.py,development.py})

7)  Go to mysite/urls.py and make appropriate changes

8) Change manage.py to reflect both development and production environment.

9)  At the prompt, type "python manage.py runserver 0.0.0.0:8000" or "python manage.py runserver localhost:8000". This would start development server on local machine at port 8000. YOU MAY HAVE TO CHANGE manage.py TO SWITCH BETWEEN DEVELOP./PROD.
 
10) Go to web browser and type '127.0.0.1:8000'. You will see 'notes' welcome page. Congratulations!!!!!

##########################################
Now we take care of the problem where static CSS, js, img, etc are not being displayed because DEBUG=False during production:
11) Now goto settings\{base.py,} and set "STATIC_ROOT = BASE_DIR / 'static_root'" and then goto mysite\urls.py and add

if not settings.DEBUG:
  urlpatterns = urlpatterns + [
    re_path(r'^static/(?P<path>.*)$', serve,{'document_root': settings.STATIC_ROOT}),
  ]


12) run 'python manage.py collectstatic':

..\django_simple_with_staticCSS_on_DebianApache2\mysite> python manage.py collectstatic

################################################
END: 'python -m pip freeze > requirements.txt'