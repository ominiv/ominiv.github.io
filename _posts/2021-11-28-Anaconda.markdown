---
layout: post
title: [Python] Anaconda
date: 2021-11-28 19:20:23 +0900
category: Python
---
# Anaconda 란?

기본적으로 파이썬 뿐만아니라 머신러닝을 위한 math, science 관련 패키지, 쥬피터 노트북까지 함께 설치됨
데이터분석을 하려면 아나콘다를 설치하고 시작하는게 편함 ^_^
(단! 아나콘다와 파이썬을 동시에 설치할경우 환경변수에 문제가 발행할 수 있으니 주의!)

## Git Bash 와 아나콘다 연동 in window

1. 아나콘다를 설치

   https://www.anaconda.com/distribution/ 

2. 아나콘다 환경변수 설정

   시스템 환경 변수 설정 > 환경변수 > Path에 아래 4개 추가

   ![image-20210714165520382](anaconda.assets/image-20210714165520382.png)

3. cmd에서 확인

   python를 입력해서 실행되는지 확인.![image-20210714165734549](anaconda.assets/image-20210714165734549.png)



### Warning message 해결방법

1. CMD 

   ```
   c:/Users/user/anaconda3/Scripts/activate
   conda activate base
   python
   ```

   ![image-20210714170013954](anaconda.assets/image-20210714170013954.png)

2. Git Bash

   우선 git bash_profile에 옵션 추가. 

   ```
   #git bash에게 anaconda와 python이 있 는지 알려줘서 실행가는 하게 함.
   echo 'export PATH="$PATH:[YOUR_PATH]:[YOUR_PATH]/Scripts"' >> .bash_profile
   
   #어디서는  python이라는 명령어를 치면 'winpty python.exe'가 실행됨
   eho 'alias python="winpty python.exe"' >> .bash_profile
   
   #적용
   source .bash_profile
   ```

   Git Bash 실행 후, 아래 명령어 수행.

   ```
   c:/Users/user/anaconda3/Scripts/activate
   source ~/anaconda3/etc/profile.d/conda.sh
   conda activate base
   python
   
   # bash profile에 추가해주면 편함.
   echo ". c:/Users/user/anaconda3/etc/profile.d/conda.sh" >> .bash_profile
   ```

   ![image-20210714171014742](anaconda.assets/image-20210714171014742.png)

   

## conda를 이용해 패키지 설치

conda install 패키지이름

conda install -c conda-forge python-pyglet

conda install --channel conda-forge pyglet

## pip을 이용하여 패키지 설치

pip install 패키지이름



## 가상환경 만들기

### 버전확인

conda --version

### 목록확인

conda info --envs

### 가상환경 추가

conda create -n tensorEnv python=3.8

### 특정 가상환경으로 접근

conda activate tensorEnv

### 가성환겅에서 빠져나오기 

conda deactivate

### 가상환경 제거(base 에서 진행)

conda env remove -n tensorEnv


+ 가상환경에 jupyter notebook 설치
  (tensorEnv) C:\WINDOWS\system32> conda install jupyter notebook

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
