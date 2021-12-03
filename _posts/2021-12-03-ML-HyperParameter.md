---
title: ML HyperParameter
date: 2021-12-03 23:30:09
categories:
- ML
tags:
- hyperparameter
---

# [ML] HyperParameter



## What is the Difference Between a Parameter and a Hyper Parameter?



> Parameter 와 Hyper-Parameter 는 다르다. 



**Parameter** 는 모델 내부에서 결정되는 변수로 그 값은 데이터로부터 결정됨

이는 모델 내부적으로 결정되는 값으로 사용자에 의해 조정되지 않음

*example) 한클래스에 속한 학생들의 키에 대해 정규분포를 그린다고 하자. 정규분포를 그릴때 평균과 표준편차가 구해집니다. 여기서 평균과 표준편차를 parameter라고 함* 



**Hyper Parameter** 는 사용자가 직접 세팅을 해주는 값을 뜻함

*example) SVM의 C , sigma/ KNN / K-means etc ..*



즉, 사용자가 직접 값을 설정하면 Hyper Parameter 이고 모델 혹은 데이터에 의해 결정되면 Pameter 이다.