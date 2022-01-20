---
title: ML/Clustering MeanShift
date: 2022-01-20 00:00:01
categories:

- ML
tags:
- Clustering
- MeanShift
---

# [ML/Clustering] MeanShift
MeanShift는 중심을 **데이터가 모여있는 밀도가 가장 높은 곳**으로 이동시킨다. *(Kmeans는 중심에 소속된 데이터의 평균거리 중심으로 이동)*<br>평균이동 군집화는 데이터의 분포도를 이용해 군집 중심점을 찾는다. 확률 밀도 함수가 피크인점을 군집 중심점으로 선정하며 일반적으로 주어진 모델의 확률 밀도 함수를 찾기 위해 KDE(Kernel Density Estimation)를 이용한다.

특정 데이터를 반경 내에 데이터 분포 확률 밀도가 가장 높은 곳으로 이동하기 위해 주변 데이터와의 거리값을 KDE함수 값으로 입력한 뒤 그 반환 값을 현재 위치에서 업데이트 하면서 이동하는 방식을 취한다. 이 과정을 반복적으로 적용하여 데이터의 군집 중심점을 찾아낸다.

✔ 평균 이동 군집화 기법은 이미지나 영상 데이터에서 특정 개체를 구분하거나 움직임을 추적 할때 주로 사용한다.

|장점|단점|
|---|---|
|특정 분포도 기반의 모델로 가정하지 않기에 더 유연한 군집화가 가능<Br>영향력도 크지 않고, 미리 군집의 개수를 정할 필요가 없음|수행시간 오래걸림 <Br>band-width 지정 어려움|

---
## KDE (Kernel Density Estimation)
커널 함수를 통해 어떤 변수의 확률 밀도 함수 PDF(Probability Density Function)를 추정하는 대표적인 방법이다.<Br>관측된 데이터 각각에 커널 함수를 적용한 값을 모두 더한 뒤 데이터 건수로 나눠 확률 밀도 함수를 추정한다. PDF는 널리 알려진 정규분포함수를 포함해 감마분포, t분포 등이 있다. 대표적인 커널함수로는 **가우시안 분포함수**가 사용된다.

오른쪽의 **빨간점선은 개별 관측데이터에 대한 가우시안 커널 함수**를 의미한다.<br> **파란선은 커널함수를 모두 더한 KDE 결과**를 나타낸다. [image ref](https://upload.wikimedia.org/wikipedia/commons/4/41/Comparison_of_1D_histogram_and_KDE.png)

<img src='https://upload.wikimedia.org/wikipedia/commons/4/41/Comparison_of_1D_histogram_and_KDE.png' width=500>

KDE는 다음과 같은 커널 함수식으로 나타낼수 있다. <br>($K$=커널함수, $h$=대역폭(bandwidth), $x$= 확률변수값, $x_i$= 관측값 )

$$
KDE = \frac{1}{n}\sum_{i=i}^{n}K_h(x-x_i) = \frac{1}{nh}\sum_{i=i}^{n}K(\frac{x-x_i}{h})
$$

대역폭은 KDE형태를 뾰족하거나 완만한 형태로 Smoothing하는 데 적용한다. $h$값을 어떻게 지정하느냐에 따라 확률 밀도 추정 성능을 크게 좌우할 수 있다. **평균이동 군집화는 오로지 대역폭크기에 따라 군집화를 수행한다.**<br>$h$값이 작을 수록 좁고 뾰족한 KDE를 가지게 되어 변동성이 Over-fitting을 초래한다. 반대로 $h$값이 클수록 과도하게 smoothing되어 단순화된 방식으로 PDF를 추정하여 under-fitting을 초래하기 쉽다. 

일반적으로 대역폭(band-width)이 클수록 적은수의 클러스터 군집 중심점을 갖는다. 

<img src='https://drive.google.com/uc?export=download&id=1pf9FK41Id_Uu6wsbS7magqlcpXsSS5YZ' width=600>

---

## Tutorial
```python
import numpy as np 
import pandas as pd 
from sklearn.datasets import make_blobs
from sklearn.cluster import MeanShift, estimate_bandwidth   

X,y = make_blobs(n_samples=200, n_features=2, centers=3,cluster_std=0.7,random_state=0)

# 최적 bandwidth 계산
bandwidth=estimate_bandwidth(X)
print('band width :',bandwidth)

# 평균이동 군집화
meanshift = MeanShift(bandwidth=bandwidth)
cluster_labels = meanshift.fit_predict(X)
print('cluster labels 유형 : ',np.unique(cluster_labels))
```

---

##  Practice

- Clustering [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/Clustering.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적

