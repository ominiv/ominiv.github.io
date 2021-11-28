---
layout: post
title: [Django] preview
date: 2021-11-28 19:20:23 +0900
category: Django
---
# WEB Programming

web이란? 흔한 웹사이트를 의미한다.  (ex, 네이버, 구글)
web page가 묶여서 Web page가 된다. (네이버 뉴스페이지 + 블로그페이지 + 메인페이지 -> 네이버 웹사이트)



|                          front end                           |                           back end                           | persistence layer |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :---------------: |
| FrontEnd : 대표적으로 웹 페이지에서 구조를 담당 <br />- 틀을 만드는 HTML<br />- 디자인효과를 주는 CSS <br />- 다양한 효과 제공 등의 기능을 하는 JavaScript 를 제공 | python (MVCpattern)<br />- model : db 다루는 영역   <br />- view  : 데이터가 처리되는 로직 정의<br />- template : 웹페이지에 보여질 페이지 (html, css, script) |        DB         |



## 💡 Django 는 뭘까? 

우선 framework에 대해 알아보자. django 는 framework중 하나다. (*django / *flask / Tornado)
framework는 쉽게 말해서 개발자가 더 빠르게 구현할수 있도록 미리 만들어진 뼈대임
여기에 개발자는 살만 추가하면 됨

Django 는 backend를 담당하는 framework다. 
즉, django는 호스트측에서 클라이언트의 요청에 대해 데이터 처리 등의 기능을 하고 사용자에게 응답하는 로직을 담당한다. 

**Django의 장점**

- 장고는 파이썬 언어를 기반으로함
- 다양한 기능이 라이브러리로 제공됨
- 장고에서는 기본적인 admin 페이지를 제공
  나같이 처음 웹을 접하는 사람은 admin page 이 왜 장점인지 모른다.
  admin page는 **관리자용 페이지**다. 즉, 해당 백엔드 서버에 존재하는 DB 데이터에 대해 웹에서 더 쉽게 접근하고 컨트롤할수 있음



## **💡 MVC가 뭔데?**

**[Model]**
model 은 실제 데이터베이스와 직접적으로 연관되는 개념.

1. models.py에 model을 클래스로 만들고, 내부 멤버 변수로 데이터의 타입등을 지정함. 
2. make migrations  명령어로 migrations 파일들을 생성 
3. migrate 명령어를 통해 migrations 파일들을 생성

즉, models.py 에 만든 하나의 model 이 데이터베이스에서 하나의 테이블이 되는 개념

**[View]**
View는 사용자에게 보여주는 화면이다. 우리는 templates 폴더가 생각날 것이다. 
templates  폴더안에 html파일을 두었고, 함수에서 로직처리 후 특정 html을 보여줌

**[Controller]**
Controller는 views.py과 연관있다. 
Controller는 사용자에게 보이는화면에 대한것이 아닌 그 뒤에서 진행되는 내부적인 로직을 담당함 
예를 들어 사용자의 입력을 받아서 이를 변형 및 저장하거나 또 다른 데이터를 꺼내오는 등 다양한 작업을 함

views.py에서는 함수들을 정의하며, 특정함수 내에서 특정 로직을 처리하도록 함

|    MVC     | 장고 프로젝트 관련 파일 및 폴더 |   MTV    |
| :--------: | :-----------------------------: | :------: |
|   Model    |            models.py            |  Model   |
|    View    |        templates folder         | Template |
| Controller |            views.py             |   View   |



## **💡 CRUD가 뭔데?**

CRUD는 대부분의 컴퓨터 소프트웨어가 가지는 기본적인 데이터 처리기능인 Create / Read / Update / Delete를 묶어서 일컫는 말이다. 사용자 인터페이스가 갖추어야할 기능 을 가리키는 용어로 사용.



## 💡Static file 관리(e.g. img/js/css)

웹 사이트는 일반적으로 이미지, JavaScript 또는 CSS와 같은 추가 파일을 제공해야 함
Django에서는 이러한 파일을 《static files》라고 하며, :mod:〉django.contrib.static files’를 제공하여 파일 관리를 도와줌 

내가 개발한 프로젝트를 운영서버로 배포하다보면 static파일을 한데 모으는 `python manage.py collectstatic` 이란 명령어를 접하게 된다. 이는 Django project의 여러 app에서 사용하는 static file을 한곳으로 모아주는 역할을 함



### ✔ 웹서버와 웹어플리케이션

Django를 이용해 웹 어플리케이션을 개발할때 Django에 내장된 경량의 웹서버를 사용하게 됨 
하지만 이는 실제 웹서버가 아니므로 Production 환경에서는 사용하면 안된다.

> *don’t use this server in anything resembling a production environment. It’s intended only for use while developing. (We’re in the business of making Web frameworks, not Web servers.)* 
> *https://docs.djangoproject.com/en/1.10/intro/tutorial01/#the-development-server*

**runserver** 로 사용하는 개발용 서버는 서버가 아니다.
실제 Production 환경에서는 Apache / Nginx 와 같은 웹서버를 사용해야한다. 
즉, 사용자의 request가 들어오면 웹서버가 받아서 적절한 처리후에 웹 어플리케이션에 넘겨주고 웹 애플리케이션은 우리가 작성한 로직에 따라 적절한 처리 후에 웹서버에 돌려주어 사용자에게 request하는 것이다.

간단히 도식화 하면 아래 그림과 같다. 
웹서버와 웹애플리케이션 사이에는 Web Server Gateway Interface 라는 규약으로 통신을 함.

![image-20210817165133890](Django.assets/image-20210817165133890.png)

*image Ref.https://crynut84.github.io/2016/11/14/django-static-file/*

### ✔ static file을 한데 모으는 이유?

http 프로토콜을 이용해 단순히 파일을 응답하는 처리는 웹서버가 잘한다. 
사용자 요청의 url을 해석해 서버내 물리적인 위치의 파일을 찾아 http 응답으로 돌려주는 단순한 작업이기 때문이다. 

그에 반해 웹 애플리케이션은 동적인 데이터를 처리하기위해 만들어졌음. e.g. 사용자마다 다르게 보이게 하는처리

CSS, js , image 파일들로 이루어진 static file을 웹어플리케이션인 django가 처리하기에는 너무 비효율적임
그래서 Django는 Production 에서의 static파일을 처리하는 기능을 담고있지 않다.

### ✔ 개발할 때 보니까 되던데?

Django 개발할 때는 static 파일이 잘 전송되는 것을 볼 수 있다. 이것은 `INSTALLED_APPS`의 django.contrib.staticfiles이라는 모듈이 담당하고 있으며, 그마저도 settings.py의 `DEBUG` 속성을 False로 바꾸면 동작하지 않게된다.

이때부터는 static 파일의 처리는 웹서버가 담당하게 되는 것이다. 아파치 설정 중에도 static 파일의 경로를 정의하는 설정이 포함되는 것을 알 수 있다.

### ✔ Static 관련 설정

앱에 포함된 기본 static 파일의 경로는 {APP_NAME}/static이다. 
manage.py의 커맨드 명령어인 `findstatic`을 수행하면 우리가 찾고자 하는 static 파일의 풀 경로를 보여준다.

```python
# settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rootWEB',
    'FrontApp',
    'chartApp',
]

# 실 서버 배포 시 static 파일을 collectstatic 하기위한 절대 경로이다. 기본 값은 None
# STATIC_ROOT = "/var/www/example.com/static/"
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

# URL로써 static 파일의 위치를 가르킬 때 사용하는 위치이다. 기본 값은 None
# STATIC_URL = "http://static.example.com/"
STATIC_URL = "/static/"

# 앱에 포함된 static 파일의 위치를 추가할 수 있다. 기본값은 [](비어있는 리스트)
# STATICFILES_DIRS = [
#    "/home/special.polls.com/polls/static",
#    "/home/polls.com/polls/static",
#    "/opt/webfiles/common",
#]
STATICFILES_DIRS=[
    os.path.join(BASE_DIR, 'FrontApp', 'static')
]

# STATICFILES_DIRS 지정 시 Optional 속성으로 Prefix를 넣을 수 있다
STATICFILES_DIRS = [
    # ...
    ("downloads", "/opt/webfiles/stats"),
]

```



------



## Web을 만들어보자 

### 0.가상환경 설정 및 활성화

```bash
python -m venv WWG
source WWG/scripts/activate
```

### 1. Django 설치 및 프로젝트 생성

```bash
#-- Django 설치
$ conda install django

#-- Django Project 생성
$ django-admin startproject [Project_Name]
```

### 2. settings.py  수정 필수

```python
import os

BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
# BASE_DIR = Path(__file__).resolve().parent.parent

ALLOWED_HOSTS = ['127.0.0.1', 'localhost']
# ALLOWED_HOSTS = []

# ROOT_URLCONF 와 TEMPLATES DIRS는 동일하게 쌍으로 변경해야함
ROOT_URLCONF = 'sampleWEB.urls'
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        #-- 수정
        'DIRS': [os.path.join(BASE_DIR, 'sampleWEB/templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        #-- 수정
        'NAME': os.path.join(BASE_DIR , 'db.sqlite3'),
    }
}

TIME_ZONE = 'Asia/Seoul'
```



### 3. server 실행

```bash
$ python manage.py runserver

#-- app을 이용하지 않을경우 Project 내에 views.py & templates > *.html 생성
# (urls.py에 링크 생성 & views.py에서 함수 생성 & 표현할 html 생성)

# urls.py
from django.contrib import admin
from django.urls import path, include
from advanceWEB import views

urlpatterns = [
    path('admin/', admin.site.urls),
    #http://127.0.0.1:8000/index
    path('index/', views.index),
    path('login/', views.login),
    path('parameter/', views.parameter),
    path('blog/', include('blogApp.urls')),
]

#views.py
from django.shortcuts import render

def index(request) :
    print('run index func.')
    return render(request, 'index.html')

# request - response
def login(request) :
    if request.method == 'POST' :
        id = request.POST['id']
        pw = request.POST['pw']
        context = {'msg': 'request post'}
        return render(request, 'result.html', context)
    if request.method == 'GET' :
        id = request.GET['id']
        pw = request.GET['pw']
        context = {'msg': 'request get'}
        return render(request, 'result.html',context)

def parameter(request) :
    print('run web para.')
    context = {'msg' : 'a tag parameter'}
    return render(request, 'result.html',context)

#index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div align = 'center'>
        <h1>index introduction!</h1>
    </div>
    <hr/>
    ::form processing
    <form action='http://127.0.0.1:8000/login/', method='post'>
        {% csrf_token %}
        ID : <input type = 'text', name='id', id='id'> <br/>
        PW : <input type = 'password', name='pw', id='pw'><br/>
        <input type = 'submit', value='LOGIN'>
    </form>
    :: a tag <p/>
    <a href = '../parameter?id=test'> a tag를 이용한 데이터 전송방식(get)</a>
</body>
</html>
```



### 4. App을 만드는 방법과 WEB 연결

```python manage.py startapp blogApp
# App 생성
python manage.py startapp [App_Name]

# App을 만들때마다 꼭 settings.py 에 App_Name 추가
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
	#-- app function addition
    'App_Name'
]
```



### 5. 사용자가 서버와 통신하는 방법

보안상의 문제 때문에 get보다 post 방식을 지향함 
[GET METHOD] url = URL ? QueryString(KEY=VALUE) 
[POST METHOD] url = URL 

```html
# plan 1
::form processing
<form action='http://127.0.0.1:8000/login/', method='post'>
    {% csrf_token %}
    ID : <input type = 'text', name='id', id='id'> <br/>
    PW : <input type = 'password', name='pw', id='pw'><br/>
    <input type = 'submit', value='LOGIN'>
</form>

# plan 2
:: a tag <p/>
<a href = '../parameter?id=test'> a tag를 이용한 데이터 전송방식(get)</a>
```



### 6. model 작성 

```python
#[ProjectName]>[AppName]>models.py

from django.db import models
# Create your models here.
# ORM Object Relationship Mapping
# class - instance - table
# create table WebBlog
class WebBlog(models.Model) :
    title = models.CharField(max_length=100)
    regDate = models.DateField()
    body = models.TextField()
```



### 7. admin 등록

```python
#[ProjectName]>[AppName]>admin.py

from django.contrib import admin
from .models import *
# Register your models here.
admin.site.register(WebBlog)
```



### 8. 테이블을 만들자 (migration)

model의 경우 단순히 models.py 파일만 수정해서 적용되지 않는다.
꼭 아래 명령어를 실행해줘야함

```bash
# migration 생성 
# migration 이란, 단순히 데이터베이스에 전해 줄 초안과 같은 역할을 함
$ python manage.py makemigrations
# 실제 테이블을 만들자!
$ python manage.py migrate

#관리자 계정 생성 (최초 1번만 진행)
$ python manage.py createsuperuser
admin
ominiv1014@gmail.com
0514030518
```

![image-20210813113712781](Django.assets/image-20210813113712781.png)



### 9. Django - orm(insert, select)

#### 9.1 html form data 받아오기

아래와 같은 from이 있다면 action의 url을 urls.py에 설정함

> crsf 이란?
> 장고의 기능 중 post데이터를 받을 때 CSRF보안코드가 포함되어 있지 않으면, Error페이지를 출력

```django
<!--*.html-->

<form action="/emaillist/add" method="">
    {% csrf_token%}
    First name: <input type="text" name="fn" value="" ><br>
    Last name: <input type="text" name="ln" value=""><br>
    Email address: <input type="text" name="email" value=""><br>
    <input type="submit" value="submit">
</form>
```

```django
<!--urls.py-->
urlpatterns = [
    ...
    path('emaillist/add', emaillist_views.add),
	...
]
```

`HttpResponse()`는 text를 그대로 화면에 출력해주는 기능

```python
from emaillist.models import Emaillist
from django.http import HttpResponseRedirect

def add(request):
    emaillist = Emaillist()
    emaillist.first_name = request.POST['fn']
	emaillist.last_name = request.POST['ln']
    emaillist.email = request.POST['email']
    emaillist.save()

    # insert 후에는 꼭 redirect 처리!
    return HttpResponseRedirect('/emaillist')
```



------



## 🛠 차트를 적용해보자!

### 1. highchart 에서 원하는 이미지 선택

codepen을 검색하면 html/ css/ js 코드를 제공해준다. 

https://www.highcharts.com/demo/spline-symbols

### 2. chartApp 생성

```bash
python manage.py startapp chartApp
```

### 3. static>chart , templates>chart 폴더 생성

일반적으로 App명/static/App명 과 같이 각 App의 static 폴더 안에 다시 "App명"" 서브폴더를 둘 것을 권장함
이는 Deployment 시 collectstatic 을 실행할 때, 각 static 폴더 밑의 내용을 그대로 복사하므로 동명 파일들이 충돌하지 않게 하기 위함이다

![image-20210817171436549](Django.assets/image-20210817171436549.png)

### 4. urls.py에 링크생성

```python
from django.urls import path
from chartApp import views

urlpatterns = [
    path('main/', views.index),
    path('line/', views.line),
    path('bar/', views.bar),
    path('word/', views.word),
]
```



### 5. views.py 함수생성

```python
from django.shortcuts import render

# Create your views here.
def index(request):
    print('chartApp START')
    return render(request, 'chart/index.html')
    
def line(request):
    print('chartApp START')
    seoul = [15, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, 26.5, 23.3, 18.3, 13.9, 9.6]
    london = [8, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8]
    context={
        'seoul' : seoul , 'london' : london
    }
    return render(request, 'chart/line.html', context)
def bar(request):
    print('bar START')
    Year1800 = [10700, 31, 635, 203, 2]
    Year1900 = [133, 156, 947, 408, 6]
    Year2000 = [814, 841, 3714, 727, 31]
    Year2016 = [1216, 1001, 4436, 738, 40]
    context={
        'Year1800' : Year1800 , 'Year1900' : Year1900, 'Year2000' : Year2000, 'Year2016' : Year2016
    }
    return render(request, 'chart/bar.html', context)
def word(request):
    print('bar START')
    return render(request, 'chart/word.html')
```



### 6. line.html 파일 생성 (hichart code copy&paste)

static files을 사용하기 위해서는 꼭 `{% load static %}`  태그를 적어야한다.

*실제 static 파일을 가리키기 위해서는 아래 link 태그에서 보이듯이 "{% static '리소스명' %}" 와 같이 static 템플릿 태그를 사용하여 해당 리소스를 지정한다.* 

```django
line.html
{% load static %}

<link rel ='stylesheet' href="{% static 'FrontApp/css/style.css' %}"
      
<img src="{% static 'FrontApp/img/avatar.png' %}"/>

<script>
    seoul ={{seoul}}
    london ={{london}}
    console.log(seoul)
    console.log(london)
    </script>
    <script src="{%static 'chart/js/line.js'%}"></script> 

```



example

```django
<!DOCTYPE html>
{% load static %}
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    #-------------------------------------------------------------------#
    <script src="https://code.highcharts.com/highcharts.js"></script>
    <script src="https://code.highcharts.com/modules/series-label.js"></script>
    <script src="https://code.highcharts.com/modules/exporting.js"></script>
    <script src="https://code.highcharts.com/modules/export-data.js"></script>
    
    <link rel ='stylesheet' href="{%static 'chart/css/line.css'%}">
    #-------------------------------------------------------------------#
</head>
<body>
    #-------------------------------------------------------------------#
    <figure class="highcharts-figure">
        <div id="container"></div>
        <p class="highcharts-description">
        This chart shows how symbols and shapes can be used in charts.
        Highcharts includes several common symbol shapes, such as squares,
        circles and triangles, but it is also possible to add your own
        custom symbols. In this chart, custom weather symbols are used on
        data points to highlight that certain temperatures are warm while
        others are cold.
        </p>
    </figure>
    #-------------------------------------------------------------------#
    <script>
    seoul ={{seoul}}
    london ={{london}}
    console.log(seoul)
    console.log(london)
    </script>
    <script src="{%static 'chart/js/line.js'%}"></script> 
    #-------------------------------------------------------------------#
</body>
</html>

```



### 7. css 파일 생성 (hichart code copy&paste)

```css
.highcharts-figure, .highcharts-data-table table {
    min-width: 310px; 
    max-width: 800px;
    margin: 1em auto;
  }
  
  .highcharts-data-table table {
      font-family: Verdana, sans-serif;
      border-collapse: collapse;
      border: 1px solid #EBEBEB;
      margin: 10px auto;
      text-align: center;
      width: 100%;
      max-width: 500px;
  }
  .highcharts-data-table caption {
    padding: 1em 0;
    font-size: 1.2em;
    color: #555;
  }
  .highcharts-data-table th {
      font-weight: 600;
    padding: 0.5em;
  }
  .highcharts-data-table td, .highcharts-data-table th, .highcharts-data-table caption {
    padding: 0.5em;
  }
  .highcharts-data-table thead tr, .highcharts-data-table tr:nth-child(even) {
    background: #f8f8f8;
  }
  .highcharts-data-table tr:hover {
    background: #f1f7ff;
  }

```



### 8. js 파일 생성

```js
        
Highcharts.chart('container', {
    chart: {
        type: 'spline'
    },
    title: {
        text: 'Monthly Average Temperature'
    },
    subtitle: {
        text: 'Source: WorldClimate.com'
    },
    xAxis: {
        categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
        'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
    },
    yAxis: {
        title: {
        text: 'Temperature'
        },
        labels: {
            formatter: function () {
                return this.value + '°';
            }
        }
    },
    tooltip: {
        crosshairs: true,
        shared: true
    },
    plotOptions: {
        spline: {
        marker: {
            radius: 4,
            lineColor: '#666666',
            lineWidth: 1
        }
        }
    },
    series: [{
        name: 'Seoul',
        marker: {
            symbol: 'square'
        },
        // data: [7.0, 6.9, 9.5, 14.5, 18.2, 21.5, 25.2, 26.5, 23.3, 18.3, 13.9, 9.6]
        data : seoul
    }, {
        name: 'London',
        marker: {
        symbol: 'diamond'
        },
        // data: [3.9, 4.2, 5.7, 8.5, 11.9, 15.2, 17.0, 16.6, 14.2, 10.3, 6.6, 4.8]
        data : london
    }]
    });

```



-----

## 🛠 JQuery의 Ajax 통신하기

Django에서  비동기식 통신을 해보려 한다. 흔히 Ajax라고 하며 JQuery에서 쓰이는 $.ajax를 많이씀.



### 1. JQuery library를 넣어주자. 

```html
#-- html 
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>

<script src="{% static '/resources/plugins/jQuery/jQuery-2.1.4.min.js' %}"></script>
```



### 2. JavaScript 코드가 필요하다.

버튼을 눌렸을때 실행되게 하기위해 버튼에 꼭 id를 지정해 준다.

```html
#-- html 
$('#replyBtn').click(function() {
	alert('replyBtn')
	alert($('#time_writer').val())
	alert($('#time_txt').val())
	alert($('#id').val())
	$.ajax({
		url : '../bbs_reply/',
		type : 'post',
		data : {'csrfmiddlewaretoken' : '{{csrf_token}}',
				time_writer : $('#time_writer').val(),
				time_txt : $('#time_txt').val(),
				board_id : $('#id').val(),
				},
		dataType : 'json' ,
		success  : function(list) {
			alert(list)
			$('#cnt').text('['+list.length+']') 
			txt =''
			$.each(list, function(idx, data){
				alert(data.writer+ ", "+data.txt+ "," +data.board_id)
				txt = "<li class = 'time-label'>"
				txt += data.txt +'&nbsp;&nbsp;&nbsp';
				if ('{{session_user_name}}' == data.writer){
					txt += "<a href = 'javascript:removeReply({{line.id}}, {{line.board_id}})' class='btn btn-primary btn-xs'>X</a>"
				}
				txt += '</li>'
			})
			$('#reply_result').html(txt)
		}
	})
```



ajax를 만들었으니 통신할 url , view 을 만들자.

```python
#-- urls.py
urlpatterns=[
	path('bbs_reply/', views.bbsReply ,  name='bbs_reply'),
]

#--views.py
def bbsReply(request) :
    print('bbsApp bbsReply - ')
    time_writer = request.POST['time_writer']
    time_txt = request.POST['time_txt']
    board_id = request.POST['board_id']
    print('param - ' , time_writer, time_txt, board_id)

    #insert
    line = Timeline(writer = time_writer , txt = time_txt , board_id = board_id)
    line.save()

    #select : where = get() | filter()
    lines = Timeline.objects.filter(board_id =board_id)
    print('line result - ', type(lines) , lines)
    lineList = []
    
    for l in lines :
        lineList.append({
            'writer' : l.writer ,
            'txt' : l.txt ,
            'board_id' : l.board_id
        })
    return JsonResponse(lineList , safe=False)
```



--------

## 🛠csv 파일을 불러와 model을 구축하자

### 1. 모델을 만든후 admin에 저장

```python
#-- models.py
# csv -> model
class CsvToModel(models.Model):
    nickName = models.CharField(max_length=50)
    profileImg = models.CharField(max_length=50)
    marriage = models.CharField(max_length=50)

#-- admin.py
from django.contrib import admin
from .models import *

# Register your models here.
admin.site.register(BbsUser)
admin.site.register(Bbs)
admin.site.register(Timeline)
admin.site.register(CsvToModel)

```





## 📌FAQ

### - 127.0.0.1:8000이 무엇일까?

처음실행시킨 프로젝트를 접속할때 127.0.0.1:8000 으로 접속한다.
이때 127.0.0.1 과 localhost는 동일한 의미다. 말그대로 local환경을 뜻함.

```bash
$ python manage.py runserver  <사용하려는 포트번호>
```



### - bootstrap이 무엇일까?

bootstrap은 트위터에서 개발한 UI library임 
이것이 탄생한 이유는 아래와 같다.

- 웹사이트 디자인때문에 개발시간이 길어지는 문제를 해결 
- 모바일 환경에 적합한 반응형 웹사이트 개발

https://getbootstrap.com/



### - template tag

```django
#{% %} 를 이용하면 html파일 내부에서 파이썬 문법 사용 할 수 있음
{% for todo in todos%}

#{{}}는 사용자에게 직접 보여주는 값을 의미
{{todo.content}}

#id = #
#class = .
```



### - tag

```
<br/> : 줄바꿈
<input type="button">
<input type="checkbox">
<input type="color">
<input type="date">
<input type="datetime-local">
<input type="email">
<input type="file">
#-- 화면에 보이지않지만 value가 지정됨
<input type="hidden"> 
<input type="image">
<input type="month">
<input type="number">
<input type="password">
<input type="radio">
<input type="range">
<input type="reset">
<input type="search">
<input type="submit">
<input type="tel">
<input type="text" name readonly|disable|required>
<input type="time">
<input type="url">
<input type="week">

```

### - 트래킹매커니즘 

- session
- cookie

- 화면분기 방법으로 render redirects

- `HttpResponse()`는 text를 그대로 화면에 출력해주는 기능

---------



## 🔗Reference

http://pythonstudy.xyz/python/article/314-Static-%ED%8C%8C%EC%9D%BC

https://crynut84.github.io/2016/11/14/django-static-file/

https://jungeunlee95.github.io/django/2019/06/20/Django-orm(insert,-select)-%EC%8B%A4%EC%8A%B5/


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
