---
title: Django SECRET_KEY 숨기기
date: 2022-01-24 00:00:01
categories:
- Django
tags:
- SECRET_KEY
- Github
---

# Django SECRET_KEY 숨기기 (json 이용)

*[grape님의 시크릿 키(SECRET_KEY) 분리 설정](https://grape-blog.tistory.com/17)<br> grape님 블로그는 더 자세히 설명되어있습니다. 위 블로그를 방문하시면 됩니다.*

처음 웹을 배울때 api, secretskey 이런것에 무지했다. <br>무식한게 용감하다고 key를 가리지 않고 배포해서 노출된 경험이 있다.....(╯°□°）╯︵ ┻━┻<br>다행이도 추가결제가 발생하지 않았지만 이제는 항상 key부터 가리고 웹프로젝트를 진행한다. 

1. manage.py 파일 위치에 secrets.json 파일을 생성한다.

2. secrets.json 파일에 api key를 입력한다.
    ```json
    {
        "SECRET_KEY": "<Your Django SECRET KEY>"
    }
    ```
3. .gitignore 파일에 secrets.json를 추가한다.

4. settings.py의 SECRET_KEY부분을 아래 처럼 수정하면된다.
    ```python
    import os, json
    from django.core.exceptions import ImproperlyConfigured

    secret_file = os.path.join(BASE_DIR, 'secrets.json')  # secrets.json 파일 위치를 명시

    with open(secret_file) as f:
        secrets = json.loads(f.read())

    def get_secret(setting):
        """비밀 변수를 가져오거나 명시적 예외를 반환한다."""
        try:
            return secrets[setting]
        except KeyError:
            error_msg = "Set the {} environment variable".format(setting)
            raise ImproperlyConfigured(error_msg)


    SECRET_KEY = get_secret("SECRET_KEY")
    ```