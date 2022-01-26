---
title: ML/TA Bag Of Words
date: 2022-01-26 00:00:01
categories:

- ML
tags:
- TA
- BOW
---

# [ML/TA] BOW(Bag Of Words)
Bag Of Words 모델은 문서가 가지는 모든 단어를 문맥이나 순서를 무시하고 일괄적으로 단어에 대해 빈도값을 부여해 피처값을 추출하는 모델이다. <br>BOW의 장점은 **쉽고 빠른 구축**에 있다. 단순히 단어의 발생횟수에 기반하고 있지만, 예상보다 문서의 특징을 잘 나타낼수있는 모델이다.

그에 반해 대표적인 단점은 아래와 같다.
- **문맥의미(Semantic Context) 반영 부족** : BOW는 단어의 순서를 고려하지 않기때문에 문장 내에서 문백적인 의미가 무시되기도 한다. 이를 보완하기 위해 n_gram기법을 활용할 수 있지만 제한적인 부분이므로 문맥의미를 반영하지 못하는 단점이있다.
- **희소행렬(Sparse Matrix) 문제** : BOW로 피처벡터화를 수행하면 희소행렬 형태의 데이터 세트가 만들어지기 쉽다. 많은 문서에서 단어를 추출하면 매우 많은 단어가 열로 생성된다. 즉, 매우 많은 문서에서 단어의 총 개수는 수만-수십만개가 되는데 하나의 문서에 있는 단어는 이 중 극히 일부분이므로 대부분의 데이터는 0값으로 채워지게 된다.<br>이처럼 대규모 컬럼으로 구성된 행렬에서 대부분의 값이 0으로 채워지는 행렬을 희소행렬이라한다.

---
## BOW Feature Vectorization
머신러닝 알고리즘은 일반적으로 숫자형 피쳐를 데이터로 입력받아 동작하기 때문에 텍스트 데이터는 숫자로 변환을 해줘야한다. **BOW는 각 문서의 텍스트를 단어로 추출해 피처로 할당하고, 각 단어의 발생빈도값으로 벡터를 생성한다.** 

BOW 모델에서 피쳐벡터화를 한다는 것은 모든 문서에서 모든 단어를 열 형태로 나열하고 각 문서에서 해당 단어의 횟수나 정규화된 빈도를 값으로 부여하는 데이터 세트 모델로 변경하는 것이다. 예를 들어 M개의 텍스트문서가 있고 이 문서에서 모든 단어를 추출해 나열했을때 N개의 단어가 있다고 가정하면 M X N 개의 단어 피처로 이뤄진 행렬을 구성하게 된다.

일반적으로 BOW의 피처벡터화는 두 가지 방식이 있다.<br>문서마다 텍스트 길이가 길고 문서개수가 많은경우 TF-IDF방식을 사용하는게 더 낫다.

- 카운트 기반의 벡터화 <br>단어 피처에 값을 부여할때 각 문서에서 해당 단어가 나타나는 횟수를 부여하는 경우다.
- TF-IDF(Term Frequency - Inverse Document Frequency) 기반의 벡터화 <br>개별 문서에서 자주 나타나는 단어에 높은 가중치를 주되 모든 문서에서 전반적으로 자주 나타나는 단어에 대해서는 페널티를 주는 방식으로 값을 부여한다.*(전체적으로 자주 나타나는 단어의 경우, 범용적으로 자주 사용되는 단어일 가능성이 높다.)*<br>모든 문서에서 반복적으로 자주 발생하는 단어에 대해 페널티를 부여하는 방식으로 단어에 대한 가중치의 균형을 맞춘다.

    <img src = 'https://drive.google.com/uc?export=download&id=1swfeoGpwDgBEger3SxrzLmzAkvwPIEFU' width=500><br>

    $TF_i$ = 개별 문서에서의 단어 i 빈도 / $DF_i$ = 단어 i를 가지고있는 문서개수 / $N$ = 전체 문서 개수

    $$
    TF-IDF_i = TF_i * log\frac{N}{DF_i} 
    $$

---
## BOW 벡터화를 위한 희소행렬
사이킷런의 `CountVectorizer` `TfidfVectorizer`는 CSR 형태의 희소행렬을 반환한다.<br>희소행렬은 너무 많은 불필요한 0값이 메모리 공간에 할당되어 메모리 공간이 많이 필요하고, 행렬크기가 커서 연산시에도 데이터 액세스를 위한 시간이 많이 소모된다. 따라서 이러한 희소행렬을 물리적으로 적은 메모리 공간을 차지할 수 있도록 변환 해야하는데 대표적인 방봅으로 COO형식과 CSR형식이 있다. 

일반적으로 CSR을 더 많이 사용한다.

### COO(Coordinate; 좌표)
COO형식은 0이 아닌 데이터만 별도의 Array에 저장하고 그 데이터가 가리키는 행과열의 위치를 별도의 배열로 저장하는 방식이다. 아래 이미지의 (row,col)과 같은 형태다.
### CSR(Compressed Sparse Row)
CSR은 COO형식이 행과 열 위치를 나타내기 위해 반복적인 위치데이터를 사용해야하는 문제점을 해결한 방식이다. 아래 이미지와 같이 **indptr은 row를 압축한 것**으로 COO보다 더 효율적인 것을 알 수 있다.

<img src = 'https://drive.google.com/uc?export=download&id=1N2uqjwvYTMbBQ9J5cym8Yzfv2_Mg8gGc' width=500>

```python
from scipy import sparse
import numpy as np

dense = np.array([[0,1,2],
                  [0,3,4],
                  [0,0,0],
                  [0,5,6]])

#0이 아닌 데이터 추출
non_zero_data = np.arange(1,7)
row_pos = [0,0,1,1,3,3]
col_pos = [1,2,1,2,1,2]

#COO형식으로 변환
sparse_coo = sparse.coo_matrix((non_zero_data,(row_pos,col_pos)))
print('COO :\n',sparse_coo.toarray())

#행 위치 배열의 고유한 값의 시작 위치 인덱스를 배열로 생성
row_pos_ind = [0,2,4,4,6]

sparse_csr = sparse.csr_matrix((non_zero_data,col_pos, row_pos_ind))
print('CSR :\n',sparse_csr.toarray())

```
---
##  Tutorial
사이킷럿의 count 및 TF-IDF 벡터화 구현 클래스를 살펴보자.<br>`CountVectorizer` `TfidfVectorizer` 는 단지 피처 벡터화만 수행하지는 않고 데이터 가공-토큰화-텍스트정규화-벡터화 작업을 순차적으로 진행한다.

```python
# 테스트 데이터 피처 벡터화를 할때 fit_transform을 사용하면안된다.
# 만약 train.fit_transform / test.fit_transform을 사용하면 컬럼수가 달라짐.

from sklearn.feature_extraction.text import CountVectorizer
cnt_vect = CountVectorizer()
cnt_vect.fit(X_train,y_train)
X_train_cnt_vect= cnt_vect.transform(X_train)
X_test_cnt_vect = cnt_vect.transform(X_test)

from sklearn.feature_extraction.text import TfidfVectorizer

tfidf_vect = TfidfVectorizer()
tfidf_vect.fit(X_train)
X_train_tfidf_vect = tfidf_vect.transform(X_train)
X_test_tfidf_vect = tfidf_vect.transform(X_test)
```

---

##  Practice

- News Classification [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/News_Classification.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적

