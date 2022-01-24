---
title: Github API Key 숨기기
date: 2022-01-24 00:00:01
categories:
- Django
tags:
- apikey
- Github
---

# Github API Key 숨기기 (.env 이용)
웹프로젝트를 깃에 올리기전에 api key를 남들이 보지 못하게 숨겨야한다.<br>
왜? 내 api key 사용하면 내가 돈을 내야하기 때문이다 ಠ_ಠ

그래서 숨기는 방법에 대해 얘기해보려한다. 

1. settings.py 파일 위치에 .env 파일을 생성한다.

2. .env 파일에 api key를 입력한다. 따옴표 없이 입력하면된다. <br>`API_KEY=<Your API KEY>`

3. .gitignore 파일에 .env를 추가한다.

4. settings.py에 `API_KEY = os.environ.get('API_KEY')`를 추가해준다.

5. template 내에 html에 api를 사용하는 방법은 아래 와 같다. `%API_KEY%` 

```Django
<script type= "text/javascript" src="https://maps.googleapis.com/maps/api/js?appkey=%API_KEY%&callback=initMap&v=weekly" async></script>

```
