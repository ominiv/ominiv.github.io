---
title: ML/Ensemble Stacking 
date: 2022-01-06 00:00:01
categories:

- ML
tags:
- Stacking
- Ensemble
---

# [ML/Ensemble] Stacking

<img src = "https://drive.google.com/uc?export=download&id=1nkQz3WuMyRURP8hbftgXKVjv3nM-M0EF" width="600px">

- 개별 알고리즘으로 **예측한 데이터를 기반으로 다시 예측**을 수행함<br>즉, 개별 알고리즘의 예측 결과 데이터 세트를 최종적인 **메타 데이터 세트로 만들어 별도의 ML알고리즘으로 최종학습을 수행**하고 테스트 데이터를 기반으로 다시 최종 예측을 수행하는 방식이다. *(개별 모델의 예측된 데이터 세트를 기바능로 학습하고 예측하는 방식을 메타 모델이라한다.)*
- 스태킹 모델은 두 종류의 모델이 필요함
  - 개별적인 기반 모델
  - 개별 기반 모델의 예측 데이터를 학습데이터로 만들어서 학습하는 최종 메타 모델
- 스태킹을 적용할 때는 많은 개별 모델이 필요하다. 2-3개의 개별모델만을 결합해서는 쉽게 예측 성능을 향상 시킬 수 없다.
- 스태킹 모델의 핵심은 여러 개별 모델의 예측 데이터를 각각 스태킹 형태로 결합하여 <br>최종 메타 모델의 학습용 피처 데이터 세트와 테스트용 피처 데이터 세트를 만드는 것이다. 
- <img src = "https://drive.google.com/uc?export=download&id=1n-W_LkryzSmMYWqdZxMkD32VJUZfUDIG" width="700px" align=left >
  <br><br><br><br><br><br><br><br>

  

---

## Stacking Tutorial

본 예제에서는  메타모델인 로지스틱 회귀모델 에서 최종 학습을 할때 <Br>레이블 데이터로 학습데이터가 아닌 테스트용  레이블 데이터 세트를 기반으로 학습했기에 **과적합 문제**가 발생할 수있다.

예시에서는 각 개별모델별 hyper parameter turning을 진행하지 않았는데, 일반적으로 최적으로 튜닝하여 진행한다.

```python
## 개별 모델 생성 / 학습 / 예측
# 개별 모델 생성
knn_clf = KNeighborsClassifier(n_neighbors=4)
rf_clf = RandomForestClassifier(n_estimators=100)
ada_clf = AdaBoostClassifier(n_estimators=100)
dt_clf = DecisionTreeClassifier()
# 개별 모델을 학습
knn_clf.fit(X_train, y_train)
rf_clf.fit(X_train, y_train)
ada_clf.fit(X_train, y_train)
dt_clf.fit(X_train, y_train)
# 개별 모델을 예측 
knn_pred = knn_clf.predict(X_test)
rf_pred = rf_clf.predict(X_test)
ada_pred = ada_clf.predict(X_test)
dt_pred = dt_clf.predict(X_test)

## 예측한 값을 쌓은 후 최종 모델을 활용해 학습/예측
pred =np.array([knn_pred, rf_pred, ada_pred, dt_pred])
print(pred.shape)
# transpose를 이용해 각 알고리즘의 예측결과를 피처로 만듦
pred = np.transpose(pred)
print(pred.shape);print('='*50)

# 스태킹으로 만들어진 데이터세트를 학습, 예측할 최종모델 생성
lr_clf = LogisticRegression(solver='liblinear')
lr_clf.fit(pred, y_test) # overfitting
lr_pred = lr_clf.predict(pred)
print('최종 메타모델의 예측 정확도:')
get_clf_eval(y_test,lr_pred)
```

---

##  CV 세트 기반 스태킹

**과적합을 개선하기위해** 최종 메타모델을 위한 데이터 세트를 만들때 **교차 검증 기반으로 예측된 결과** 데이터 세트를 이용합니다.

CV 세트 기반 스태킹은 개별 모델들이 각각 교차검증으로 메타 모델을 위한 학습용 스태킹 데이터생성과 예측을 위한 테스트용 스태킹 데이터를 생성한 후 이를 기반으로 메타모델이 학습과 예측을 수행한다. 다음과 같이 2단계 스텝으로 구분 될 수 있다.

- Step1 : 각 모델별로 원본 학습/테스트 데이터를 예측한 결과 값을 기반으로 메타모델을 위한 **학습용/테스트용 데이터를 생성**함
- Step2 : `Step1`에서 개별 모델들이 생성한 학습용 데이터를 모두 쌓아서 메타 모델이 학습할 `최종 학습용 데이터 세트`를 생성한다. <br>마찬가지로 각 모델들이 생성한 테스트용 데이터를 모두 쌓아서  메타모델이 예측할 `최종 테스트용 데이터세트`를 생성한다.<br>**메타모델은 최종적으로 생성된 학습데이터와 원본 학습 데이터의 레이블을 기반으로 학습한 뒤, <Br>최종적으로 생성된 테스트 데이터세트를 예측하고, 원본 테스트 데이터의 레이블 데이터를 기반으로 평가한다.**

✔ 핵심은 개별 모델에서 *메타모델인 2차 모델에서 사용될 학습용 데이터와 테스트용 데이터* 를 교차검증을 통해 생성하는것이다. <br>`Step1`은  개별 모델 레벨에서 수행하는 것으로 이러한 로직을 각 모델에 동일하게 수행함.

<img src = "https://drive.google.com/uc?export=download&id=1UnJp5YrV2RYoyTWGtR4VV-icIcff7cL_" width="600px">

### Process

3 Fold라고 가정해보자.

1. **학습용 데이터**를 3개의 폴드로 나누고 `2개의 폴드는 학습을 위한 데이터`, 나머지 `1개 폴드는 검증을 위한 것`으로 지정한다.
   1. 두개의 폴드로 나뉜 학습데이터를 기반으로 개별 모델을 학습시킨다. 
   2. 학습된 개별 모델은 폴드 1개의 검증데이터로 예측하고 그 결과를 저장한다.
2. 2 단계를 3번 반복하며 학습데이터와 검증데이터 세트를 변경해가면서 학습 후 예측결과를 별도로 저장한다. 
3. 3 단계에서 만들어진 예측결과는 메타모델을 학습시키는 학습데이터로 사용된다.

<br>

1. **테스트용 데이터**를 3개의 폴드로 나눠 `2개의 폴드는 학습을 위한 데이터`, 나머지 `1개 폴드는 검증을 위한 것`으로 지정한다.
   1. 두개의 폴드로 나뉜 학습데이터를 기반으로 개별 모델을 학습시킨다. 
   2. 학습된 개별 모델은 폴드 1개의 검증데이터로 예측하고 그 결과를 저장한다.
2. 1단계를 3번 반복하면서 이 예측값의 평균으로 최종 결과값을 생성하고 이를 메타 모델을 위한 테스트 데이터로 사용한다.

---

##  Practice

- Practice stacking [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/breast cancer dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
