---
title: Colab Mount (구글드라이브 내 파일 접근)
date: 2022-01-19 00:00:01
categories:
- Python
tags:
- Mount
- Colab
---

# Colab Mount 구글드라이브 내 파일 접근하는 방법
코랩에서 아래 코드를 실행시키면 연동할 것이냐는 메세지 창이 뜬다. 
```
from google.colab import drive
drive.mount('/content/drive')
```

연동 후 원하는 디렉토리로 이동해서 분석을 진행하면된다. <br>`cd` = change directory / `ls` = 현재 디렉토리 내에 있는 dir,file 출력
```
cd /content/drive/MyDrive/
ls
```