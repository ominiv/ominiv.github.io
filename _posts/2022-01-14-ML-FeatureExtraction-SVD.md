---
title: ML/FeatureExtraction SVD
date: 2022-01-14 00:00:01
categories:

- ML
tags:
- FeatureExtraction
- SVD

---

# [ML/FeatureExtraction] 특이값 분해(Singular Value Decomposition)
특이값 분해는 임의의 $m \times n$ 차원 행렬 $A$ 에 대해 다음과 같이 행렬을 분해할 수 있다는 행렬 분해 방법 중 하나다. 이 방법은 $(m \times n)$ 행렬의 고유값과 고유벡터를 이용한 고유분해(eigen decomposition)의 일반화 된 방식이다.

$$
    A = U\sum V^T
$$

행렬 $U$와 $V$에 속한 벡터는 특이벡터로 모든 특이벡터는 서로 직교하는 성질을 가진다.<br>$\sum$는 대각행렬으로, 0이 아닌 대각에 위치한 값은 행렬 $A$의 **특이값**이다.<br>크기와 성질은 다음과 같다.

$$
    A=m \times n  , (rectangular)  \\
    U = m \times m  , (orthogonal)  \\
    \sum =m \times n  , (diagonal)  \\
    V=n \times n  , (orthogonal)  
$$

---

## 특이값 분해 활용 

특이값 분해는 분해되는 과정보다 분해된 행렬을 다시조합하는 과정에서 그 응용력이 빛을 발한다.<br>기존의 $U,\sum ,V^T$ 로 분해되어있던 $A$행렬을 특이값 p개 만을 이용해 $A'$라는 행렬로 부분복원을 할 수 있다. <br>특이값의 크기에 따라 $A$의 정보량이 결정되므로 **몇개의 큰 특이값을 가지고도 충분히 유용한 정보를 유지**할 수 있다. [reference](https://angeloyeo.github.io/2019/08/01/SVD.html)


<img src=' https://drive.google.com/uc?export=download&id=1QSlTSj02NesLkcr2WqMmd6nDpafmrQuP' width=500>

---

## Tutorial
numpy의 SVD를 이용해 SVD 연산, 분해가 어떻게 되는지 예제로 살펴보자.

```python
import numpy as np
from numpy.linalg import svd

#랜덤 행렬 A 생성  
np.random.seed(121)
A = np.random.randn(4,4)

# A행렬에 SVD를 적용해 U, sigma, V 도출
U, Sigma,Vt =svd(A)
# Sigma 대각행렬으로 변환 후 U, sigma, Vt 내적
Sigma_mat = np.diag(Sigma)
# A 와 A_가 동일하게 복원됨을 확인
A_ = np.dot(np.dot(U,Sigma_mat),Vt)
```

일부 상위 특이값을 선택해서 SVD를 실행해보자.<br>**일부를 선택해서 진행하므로 A행렬과 동일하게 복원할 수 없다.**

```python
import numpy as np
from scipy.sparse.linalg import svds
from scipy.linalg import svd

# 원본행렬을 추출하고 SVD적용후, U, sigma, V 도출
np.random.seed(121)
A= np.random.randn(6,6)
# Truncated SVD로 특이값 4개로 지정 
U, sigma, Vt = svds(A,4)
sigma_mat = np.diag(sigma)
A_=np.dot(np.dot(U,sigma_mat),Vt)
```

`TruncatedSVD`클래스는 사이파이와 다르게 $U,\sum,V^T$를 반환하지 않는다. 

```python
from sklearn.decomposition import TruncatedSVD
from sklearn.datasets import load_iris
from sklearn.preprocessing import StandardScaler

iris= load_iris()
scaled_data = StandardScaler().fit_transform(iris.data)
tsvd = TruncatedSVD(n_components=2)
tsvd.fit(scaled_data)
iris_tsvd=tsvd.transform(scaled_data)
```

---

##  Practice

- Feature extraction SVD [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/Feature%20extraction.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
- [angeloyeo 님의 특이값분해](https://angeloyeo.github.io/2019/08/01/SVD.html)
