---
title: ML/FeatureExtraction LDA
date: 2022-01-14 00:00:01
categories:

- ML
tags:
- FeatureExtraction
- LDA

---

# [ML/FeatureExtraction] LDA(Linear Discrimnant Anaylsis)
LDA는 선형 판별 분석법으로 불리며 Classification과 Dimension Reduction을 사용하는 알고리즘이다.<Br>지도학습의 분류에서 사용하기 쉽도록 개별 클래스를 분별할 수 있는 기준을 최대한 유지 하면서 차원을 축소한다.<br>PCA는 데이터의 변동성이 가장 큰 축을 찾았지만, **LDA는 입력 데이터의 결정값 클래스를 최대한을 분리**할 수 있는 축을 찾는다.

**LDA는 특정 공간상에서 클래스 분리를 최대화하는 축을 찾기 위해 클래스간 분산은 최대한 크게 가져가고 클래스 내부 분산은 최대한 작게 가져가는 방식이다.**<Br> 아래 그림처럼 데이터를 특정 한 축에 사영한 후 두 범주를 잘 구분할 수 있는 직선을 찾는걸 목표로 한다.


<img src='https://drive.google.com/uc?export=download&id=1JFJ4VZbV7GLmsxdIaF26PYBUeyZfPrNS' width = 300>

---

## LDA Process
PCA와의 가장 큰 차이점은 공분산 행렬이 아니라 **클래스 간 분산과 클래스 내부 분산 행렬**을 생성한 뒤,  이 행렬에 기반해 고유 벡터를 구하고 입력 데이터를 투영한다. *([ratsgo 님의 선형판별분석](https://ratsgo.github.io/machine%20learning/2017/03/21/LDA/) 블로그에서 LDA에 대한 접근과정을 상세히 기술 해 놓았다 👍 해당 글을 읽으니 이해가 되었다. 참고)*

1. 클래스 내부와 클래스 간 분산행렬을 구한다. <br>이 두개의 행렬은 입력 데이터의 결정값 클래스 별로 개별 피처의 평균 벡터를 기반으로 구한다. 
2. 클래스 내부 분산행렬 $S_w$ , 클래스 간 분산행렬 $S_B$라고 하면 아래와 같이 두 행렬을 고유 벡터로 분해 할 수 있다. 

$$
S_w^TS_B = \begin{bmatrix}e_1& \dots &e_4 
\end{bmatrix}\begin{bmatrix}\lambda_1& \dots &0\\
\dots& \dots & \dots \\
0& \dots &\lambda_n \\ \end{bmatrix}
\begin{bmatrix}e_1^t\\\dots\\e_n^t \end{bmatrix}
$$

3. 고유값이 가장 큰 순으로 k개(LDA 변환 차수 만큼) 추출한다.
4. 고유값이 가장 큰순으로 추출된 고유벡터를 이용해 새롭게 입력 데이터를 변환한다.

---

## Tutorial

```python
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import load_iris

scaled_iris =StandardScaler().fit_transform(iris.data)
lda = LinearDiscriminantAnalysis(n_components=2)
lda.fit(scaled_iris,iris.target)
iris_lda= lda.transform(scaled_iris)
```

---

## PCA vs LDA
- LDA : unsupervised learning 
    - 원소들은 뭉치고 클래스들 사이는 멀어지는 축에 사영 (클래스 정보 이용)

- PCA : supervised learning
    - 여러개 데이터가 혼재할때, 클래스 종류와 상관없이 모든 원소들의 경향을 분석
    - 전체 원소들이 가장 넓게 퍼질 수 있는 축에 사영


---

##  Practice

- Feature extraction LDA [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/Feature%20extraction.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
- [살만한 세상 만들기 님의 LDA (Linear Discriminant Analysis), PCA (Principal Component Analysis)](https://klkl0.tistory.com/23)
- [ratsgo 님의 선형판별분석](https://ratsgo.github.io/machine%20learning/2017/03/21/LDA/)