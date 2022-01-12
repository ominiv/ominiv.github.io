---
title: resizing image with Python PIL
date: 2022-01-12 00:00:01
categories:
- Python
tags:
- resizing
- image
- PIL
---

# 파이썬을 활용해 이미지 사이즈 조절하기
굉장히 편하다. 일괄적으로 모든 이미지의 사이즈를 조절할 수 있다.<Br>`PIL` library를 활용하자 

```python

from PIL import Image
import os

file_list = os.listdir('C:/Users/user/images')

for jpg in file_list :
    path = 'C:/Users/user/images'+jpg
    img = Image.open(path)
    img_resize = img.resize((460, 410))
    img_resize = img_resize.convert('RGB')
    img_resize.save(path)

```