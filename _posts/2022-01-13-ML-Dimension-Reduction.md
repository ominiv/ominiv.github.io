---
title: ML Dimension-Reduction
date: 2022-01-13 00:00:01
categories:

- ML
tags:
- Dimension Reduction
- FeatureExtraction
- FeatureSelection

---

# [ML] Dimension Reduction

<img src='https://drive.google.com/uc?export=download&id=1MpQrTnyXgKrxtR1la8D4n3qrWv1fXmED' width=550>

우선 차원축소는 매우 많은 피처로 구성된 다차원 데이터 세트의 차원을 축소해 새로운 차원의 데이터 세트를 생성한다. <br>**일반적으로 차원이 증가할수록 데이터 포인트 간의 거리가 기하급수적으로 멀어지고 sparse한 구조를 가지게 된다.** <br>수백개 이상의 피처로 구성된 데이터 세트의 경우 상대적으로 적은 차원에서 학습된 모델보다 예측 신뢰도가 떨어진다. 또한 피처가 많을 경우 개별 피처간의 상관관계가 높을 가능성이 크다. *(선형모델에서는 입력변수간의 상관관계가 높을경우 다중공선성 문제가 발생하여 예측성능 저하.)*

✔ **차원축소를 진행할경우, 더 직관적으로 데이터를 해석할수 있고 데이터의 크기가 줄어서 학습에 필요한 처리 능력도 줄일 수 있는 장점이 있다.**

일반적으로 차원 축소는 Feature selection 과 Feature extraction으로 나뉜다. 
- Feature selection 
    - 말그대로 특정 피처에 종속성이 강한 불필요한 피처는 제거하고 특징을 잘 나타내는 주요 피처만 선택
- Feature extraction
    - 기존 피처를 저차원의 중요피처로 압축해서 추출한다.<br>단순히 데이터의 압축을 의미하는것이 아니라 차원축소를 통해 더 데이터를 잘 설명할 수 있는 잠재적인 요소를 추출
    - 추출된 기존 피처가 압축된것으로 기존의 피처와는 완전히 다른값임
    - PCA, SVD, NMF는 잠재적인 요소를 찾는 대표적인 차원축소 알고리즘 *주로 이미지나 텍스트 차원축소에 사용된다.*

---

## Reference
- 파이썬 머신러닝 완벽가이드 서적
