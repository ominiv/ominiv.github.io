---
title: ML/FeatureExtraction NMF
date: 2022-01-18 00:00:01
categories:

- ML
tags:
- FeatureExtraction
- NMF

---

# [ML/FeatureExtraction] NMF(Non - Negative Matrix Factorization)
NMF는 원본행렬$V$ 내의 모든 원소값이 **모두 양수**라는 것이 보장되면 두 개의 양수 행렬로 분해 할 수 있다.(*non-negative 데이터는 non-negative feature로 설명하는것이 좋다.*)<Br>NMF는 PCA,SVD와 같은 factorization 방법에 비해 데이터 구조를 더 잘 반영한다. [link](https://angeloyeo.github.io/2020/10/15/NMF.html) 

분해된 행렬은 **잠재 요소**를 특성으로 가진다.<Br>분해행렬$W$는 원본 행렬에 대해서 이 잠재요소의 값이 얼마나 되는지에 대응하며 분해행렬$H$는 잠재요소가 원본 열(속성)로 어떻게 구성 됐는지를 나타낸다. 

<img src='https://drive.google.com/uc?export=download&id=1U12dCZvhO9eZg2x7i-3JBBRbm2S41cu9' width=450 >

주로 NMF는 차원축소를 통한 잠재요소 도출로 **이미지 변환 및 압축/ 텍스트의 토픽도출 영역**에서 사용된다. 또한 영화 추천과 같은 **추천영역**에 활발하게 적용된다.<br>사용자-평가 데이터 세트를 행렬분해기법을 통해 분해하면서 사용자가 평가하지 않은 상품에 대한 잠재적인 요소를 추출해 이를 통해 평가순위를 예측하고 높은 순위로 예측된 상품을 추천해주는 방식이다. 이를 잠재요소기반의 추천방식(Latent Factorizing)이라한다.

---

## Tutorial

```python
from sklearn.decomposition import NMF
from sklearn.datasets import load_iris
import matplotlib.pyplot as plt

iris = load_iris()
X_feature = iris.data
y_label = iris.target

nmf = NMF(n_components=2)
iris_nmf = nmf.fit_transform(X_feature)
colors = ['red','blue','green']
for i,color in enumerate(colors):
    plt.scatter(iris_nmf[iris.target==i][:,0],iris_nmf[iris.target==i][:,1],c=color,label=iris.target_names[i])
plt.xlabel('NMF component 1')
plt.ylabel('NMF component 2')
plt.legend()
```


---

##  Practice

- Feature extraction NMF [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/Feature%20extraction.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
- [angeloyeo 님의 NMF](https://angeloyeo.github.io/2019/08/01/SVD.html)
