# Docker_Django_deployment_tool

Log in to the project root folder and copy these files there.

```
$ git clone https://github.com/cavidanhasanli/Docker_Django_deployment_tool.git
$ mv Dockerfile ../
$ mv docker-compose.yml ../
$ souce .venv/bin/activate
$ pip install Uwsgi
$ pip freeze
$ pip freeze > requirements.txt
$ touch uwsgi.ini
$ nano uwsgi.ini
# add uwsgi.ini and change 2 line  "env = DJANGO_SETTINGS_MODULE=mysite.settings" path project settings path
"""
[uwsgi]
env = DJANGO_SETTINGS_MODULE=mysite.settings
env = UWSGI_VIRTUALENV=/venv
env = IS_WSGI=True
env = LANG=en_US.UTF-8
workdir = /code
chdir = /code
module = mysite.wsgi:application
master = True
pidfile = /tmp/app-master.pid
vacuum = True
max-requests = 500000
processes = 5
cheaper = 2
cheaper-initial = 5
gid = root
uid = root
http-socket = 0.0.0.0:$(HTTP_PORT)
stats = 0.0.0.0:$(STATS_PORT)
harakiri = $(TIMEOUT)
print = Your timeout is %(harakiri)
static-map = /static=%(workdir)/static
static-map = /media=%(workdir)/media

"""

$ docker-compose up --build -d
```