# Docker
Docker is a way to isolate and run entire applications. With Docker it doesn’t matter if you are using a Mac, Windows, or Linux computer anymore. The entire development environment is isolated: programming language, software packages, databases, and more.

With Docker we now longer have to mess around with virtual environments. We can faithfully reproduce a production environment locally. And Docker can be shared among team members so everyone is working on the same setup. Wins all around.

## Linux Containers
### Docker is really just Linux containers which are a type of virtualization.

Virtualization has its roots at the beginning of computer science when large, expensive mainframe computers were the norm. How could multiple programmers use the same single machine? The answer was virtualization and specifically virtual machines which are complete copies of a computer system from the operating system on up.

An analogy we can use here is that of homes and apartments. Virtual Machines are like homes: stand-alone buildings with their own infrastructure including plumbing and heating, as well as a kitchen, bathrooms, bedrooms, and so on. Docker containers are like apartments: they share common infrastructure like plumbing and heating, but come in various sizes that match the exact needs of an owner.

## Containers vs Virtual Environments

Virtual environments are used to isolate Python software packages locally. We can create an isolated box for individual projects so one can use Python 2.7 and Django 1.5 while another can use Python 3.5 and Django 2.1 on the same computer. Virtual environments are great.

virtual environments can only isolate Python packages. They still rely on a global, system-level installation of Python albeit they can refer to the proper version. So when we use Python 2.7 in a project, we’re pointing to an installation of Python 2.7 on the computer itself, not actually within the virtual environment.

Also we can’t run a production database or other services within virtual environments so compared to Docker containers they are far more limited.

## to install Docker
we need to download the desktop app from this site https://www.docker.com/get-started/

then you have to install Docker Compose using `sudo pip install docker-compose`

then you should use `docker run hello-world` to check that every thing is installed correctly, it should give the screen below:

```

$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete
Digest: sha256:9572f7cdcee8591948c2963463447a53466950b3fc15a247fcad1917ca215a2f
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 ```
 ### another command to run is `docker info`, in the output foucs on the top lines :
 ```
 $ docker info
Containers: 1
 Running: 0
 Paused: 0
 Stopped: 1
Images: 1
```
## Images and Containers
An image is a snapshot in time of what a project contains. A container is a running instance of the image.

we use `Dockerfile` to create our own image and we use `docker-compose.yml` fils to run the containers .

A baking analogy we can use here is as follows:

- A Dockerfile is the recipe for a cake
- An image is a snapshot of the recipe at a given time
- A docker-compose.yml says how to make the cake
- And the container is the actual, baked cake

## Images
First create a local directory on your computer for our code, now define the image with `DockerFile` , Dockerfiles are read from top-to-bottom. The first instruction must be the FROM command which lets us import a base image to use for our image. This base image could be another Docker image or one we create entirely from scratch.

### Image Builds
to create the image for the first time use use the following command `docker image build .`

There will be a lot of output here ending with Successfully built and the hash id, b2c276538711, for the image, the actual has will changes .

use `docker image ls` to check existant images

### Image Layers
Every image is made up of one or more image layers. The base layer is often a flavor of Linux. 
image layering exists for two main reasons. First, each image layer is immutable–unchanged–like a git commit. This helps ensure consistency when two developers build the same image. The second reason is performance. Docker caches the steps in a `Dockerfile` to speed up subsequent builds.

## Containers
Now that we have our Python image how do we run it? Well just as a Dockerfile is a list of image instructions there is also a docker-compose.yml file that is a list of container instructions.

To demonstrate a real-world image and container example we will now “Dockerize” a basic Django web app.

Creat new Django project and run the server tomake sure that everything is working fine

Stop the local server with the command Control+c. And exit the virtual environment by also typing exit.


## Dockerized Django
 We’ll now create a Dockerfile for our image which will completely replace our local dev environment, so this will have Python 3 and Django. Then we’ll add a docker-compose.yml for the container instructions. Make each file via the command line.
```
$ touch Dockerfile
$ touch docker-compose.yml
```
 This Dockerfile has several commands. RUN, COPY, and ADD each create a new layer.
```
# Dockerfile

# Python version
FROM python:3.7-alpine

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set work directory
WORKDIR /code

# Install dependencies
COPY Pipfile Pipfile.lock /code/
RUN pip install pipenv && pipenv install --system

# Copy project
COPY . /code/
```
 Order matters in Dockerfiles since they are executed from top-to-bottom. First we use FROM to install python:3.7-alpine as our base image and set two environment variables with ENV. The first, PYTHONDONTWRITEBYTECODE will remove .pyc files from our container which is a good optimization. The second, PYTHONUNBUFFERED will buffer our output so it will look “normal” within Docker for us.

 Then we used the WORKDIR command to create and set /code as our default directory within Docker. That means if in the future we want to run a command like python manage.py runserver we don’t have to also specify it should be run in the /code folder.

 The Pipfile contains information on our software packages so we copy that over, too. (Technically we could use COPY Pipfile . and because of the WORKDIR setting it would still go in the /code folder!)

 And then we install Pipenv itself via pip and then run pipenv install to install the software packages in our Pipfile. Note that we added the --system tag so that software packages are available throughout the entire container, not within a virtual environment which is Pipenv’s default but doesn’t make sense here since the entire Docker container is a virtual environment.



 An important point to make here is that the order in a Dockerfile matters a lot. Because of layer caching when a step changes in the Dockerfile, all subsequent work needs to be redone.

 For example, the very last line here is COPY . /code. That means any code changes locally will be copied over. However there are no commands after that; nothing else needs to be rebuilt. If we had put this command earlier in the Dockerfile, say, before we install the Pipfile, then every time there is a local code change all our requirements would have to be reinstalled on the image. Wasteful.

 Without going too far down this rabbit hole, remember that order is extremely important for performance and managing image size.

 Now time for docker-compose.yml.
```
# docker-compose.yml
version: '3.7'

services:
  web:
    build: .
    command: python /code/manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - 8000:8000
```
 At the top we specify we’re using the 3.7 version of Docker Compose and then set up a service, which is running within our container.

 Multiple services can run within a Docker host–for example, we might add a db service for a running PostgreSQL database in the future–but for now we have a single web service.

 We tell it to build the current directory, execute runserver on startup which will start the Django server. Then volumes will sync our local directory to the Docker container. And as a final step we expose port 8000 which is Django’s default so the container will expose it, too.

 Instead of running separate commands to build the image and run the container we can do that with one now. Check this out!
```
$ docker-compose up --build
Creating network "djangoapp_default" with the default driver
Building webStep 1/6 : FROM python:3.7-alpine
...
Successfully built 047a6d848c5b
Successfully tagged djangoapp_web:latest
Recreating djangoapp_web_1 ... done
Attaching to djangoapp_web_1
web_1  | Performing system checks...
web_1  |
web_1  | Watching for file changes with StatReloader
web_1  | System check identified no issues (0 silenced).
web_1  |
web_1  | You have 17 unapplied migration(s). Your project may not work properly until you apply the migrati
ons for app(s): admin, auth, contenttypes, sessions.
web_1  | Run 'python manage.py migrate' to apply them.
web_1  | January 21, 2020 - 14:49:16
web_1  | Django version 3.0, using settings 'example_project.settings'
web_1  | Starting development server at http://0.0.0.0:8000/
web_1  | Quit the server with CONTROL-C.
```
 There will be a lot of output here but if it all worked you can now visit http://127.0.0.1:8000/ in your web browser and see that Django is running entirely within a container now.






# Django for APIs - Library Website
 The most important takeaway is that Django creates websites containing webpages, while Django REST Framework creates web APIs which are a collection of URL endpoints containing available HTTP verbs that return JSON.

 To illustrate these concepts, we will build out a basic Library website with traditional Django and then extend it into a web API with Django REST Framework.


## Django REST Framework
 Django REST Framework is added just like any other third-party app. On the command line type the below.

```
(library) $ pipenv install djangorestframework~=3.11.0
```
 Or if you are poetry user use this command:
 
```
(.venv) $ poetry add djangorestframework
```
 Add it to the INSTALLED_APPS config in our settings.py file. I like to make a distinction between third-party apps and local apps as follows since the number of apps grows quickly in most projects.

```python
# config/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # 3rd party
    'rest_framework', # new

    # Local
    'books',
]
```

Ultimately, our API will expose a single endpoint that lists out all books in JSON. So we will need a new URL route, a new view, and a new serializer file (more on this shortly).

There are multiple ways we can organize these files however my preferred approach is to create a dedicated api app. That way even if we add more apps in the future, each app can contain the models, views, templates, and urls needed for dedicated webpages, but all API-specific files for the entire project will live in a dedicated api app.


Let’s first create a new api app.

```
(library) $ python manage.py startapp api
```

Then add it to INSTALLED_APPS.

```python
# config/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # 3rd party
    'rest_framework',

    # Local
    'books',
    'api', # new
]
```

The api app will not have its own database models so there is no need to create a migration file and run migrate to update the database.
## URLs

Let’s start with our URL configs. Adding an API endpoint is just like configuring a traditional Django app’s routes. First at the project-level we need to include the api app and configure its URL route, which will be api/.
```python
# config/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('api.urls')), # new
    path('', include('books.urls')),
]
```

Then create a urls.py file within the api app.

```
(library) $ touch api/urls.py
```

And update it as follows:

```python
# api/urls.py
from django.urls import path
from .views import BookAPIView

urlpatterns = [
    path('', BookAPIView.as_view()),
]
```
## Views

Next up is our views.py file which relies on Django REST Framework’s built-in generic class views. These deliberately mimic traditional Django’s generic class-based views in format, but they are not the same thing.


To avoid confusion, some developers will call an API views file apiviews.py or api.py. Personally, when working within a dedicated api app I do not find it confusing to just call a Django REST Framework views file views.py but opinion varies on this point.


Within our views.py file, update it to look like the following:

```python
# api/views.py
from rest_framework import generics

from books.models import Book
from .serializers import BookSerializer


class BookAPIView(generics.ListAPIView):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

```
 On the top lines we import Django REST Framework’s generics class of views, the models from our books app, and serializers from our api app (we will make the serializers next).

 Then we create a BookAPIView that uses ListAPIView to create a read-only endpoint for all book instances. 

 The only two steps required in our view are to specify the queryset which is all available books, and then the serializer_class which will be BookSerializer.

## A serializer translates data into a format that is easy to consume over the internet, typically JSON, and is displayed at an API endpoint. For now I want to demonstrate how easy it is to create a serializer with Django REST Framework to convert Django models to JSON.

 Make a serializers.py file within our api app.
```
(library) $ touch api/serializers.py
```

Then update it as follows in a text editor.

```python
# api/serializers.py
from rest_framework import serializers

from books.models import Book


class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ('title', 'subtitle', 'author', 'isbn')

```
 On the top lines we import Django REST Framework’s serializers class and the Book model from our books app. We extend Django REST Framework’s ModelSerializer into a BookSerializer class that specifies our database model Book and the database fields we wish to expose: title, subtitle, author, and isbn.

## cURL
 We want to see what our API endpoint looks like. We know it should return JSON at the URL http://127.0.0.1:8000/api/. Let’s ensure that our local Django server is running:
```
(library) $ python manage.py runserver
```
 Now open a new, second command line console. We will use it to access the API running in the existing command line console.

 We can use the popular cURL program to execute HTTP requests via the command line. All we need for a basic GET request it to specify curl and the URL we want to call.
```
$ curl http://127.0.0.1:8000/api/
[  
   {  
      "title":"Django for Beginners",
      "subtitle":"Build websites with Python and Django",
      "author":"William S. Vincent",
      "isbn":"978-198317266"
   }
]
```
 The data is all there, in JSON format, but it is poorly formatted and hard to make sense of. Fortunately Django REST Framework has a further surprise for us: a powerful visual mode for our API endpoints.




