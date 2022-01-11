---
title: ML Undersampling- Oversampling 
date: 2022-01-05 00:00:01
categories:
- ML
tags:
- imbalance
- 오버샘플링
---

# [ML] Undersampling- Oversampling 
레이블이 불규형한 분포를 가진 데이터 세트를 학습 시킬때 예측 성능의 문제가 발생할수 있다. <br>이는 정상 레이블 데이터 건수에 비해 이상 레이블 데이터가 너무 적기 때문이다.  

지도학습에서 극도로 불균형한 레이블 값 분포로 인해 문제점을 해결하기 위해 적절한 학습데이터를 확보하는 방안이 필요하다. <br>이런 경우, 대표적으로 오버샘플링(Oversampling)과 언더샘플링(Undersampling)을 이용한다.

✔ **오버샘플링 방식이 예측 성능상 더 유리한 경우가 많으며 주로 사용한다.**

- **오버샘플링**
  - 적은 레이블을 가진 데이터세트를 많은 레이블을 가진 데이터 세트수준으로 증식
  - 이상 데이터와 같이 적은 데이터 세트를 증식하여 학습을 위한 충분한 데이터를 확보하는 방법
  - 동일한 데이터를 단순히 증식하는 방법은 과적합이 되기 때문에 원본 데이터의 피처 값들을 아주 약간만 변경하여 증식시킨다. <br>대표적으로 **SMOTE(Synthetic Minority Oversampling Technique)** 방법 존재함 <br>*(SMOTE는 적은 데이터 세트에 있는 개별 데이터들의 KNN을 찾아서 이 데이터와 K개 이웃들의 차이를 일정값으로 만들어서 기존 데이터와 약간 차이나는 새로운 데이터들을 생산함)*
  - <img src = "https://drive.google.com/uc?export=download&id=1HyYI8_A7ycxpxfHBdQw-ng79htZriP5J" width="300px" align=left>
  <br><br><br><br><br><br>

- **언더샘플링**
  - 많은 레이블을 가진 데이터 세트를 적은 레이블을 가진 데이터 수준으로 감소시키는 방법입니다. <br>즉, 정상레이블을 가진 데이터가 10,000건 이상 레이블을 가진 데이터가 100건이 있다면 정상레이블 데이터를 100건으로 줄여버리는 방식입니다.
  - 대체로 너무 많은 정상레이블 데이터를 감소시키기 때문에 정상레이블의 경우 **제대로 된 학습을 수행할수없다는 단점**이 있어서 잘 사용하지 않음
  - <img src = "https://drive.google.com/uc?export=download&id=1i_DWea6xE4DQNQ7X55jPnrYbwfTzAAl1" width="300px" align=left>
  <br><br><br><br><br><br>

---

## SMOTE

- 데이터를 증식하는 방법 중 하나다.
- SMOTE는 적은 데이터 세트에 있는 개별 데이터들의 KNN을 찾은 후<br>이 데이터와 K개 이웃들의 차이를 일정값으로 만들어서 기존 데이터와 약간 차이나는 새로운 데이터들을 생산한다. (증식)
- **SMOTE는 반드시 학습 데이터 세트에만 적용해야한다**. 테스트 데이터에 적용할 경우 믿을수 없는 결과가 도출된다.
- `imbalanced - learn` 패키지의 SMOTE 클래스를 활용하면 쉽게 구현 할 수 있다.
- SMOTE를 적용하면 재현률이 높아지거나, 정밀도는 낮아지는것이 일반적이다. 

### tutorial

target 내의 0과 1의 개수가 동일해진 것을 확인 할 수 있다.

```python
from imblearn.over_sampling import SMOTE

smote = SMOTE()
X_train_over, y_train_over = smote.fit_resample(X_train,y_train)
print('smote 적용 전 train dataset shape',X_train.shape, y_train.shape)
print('smote 적용 후 train dataset shape',X_train_over.shape, y_train_over.shape)
print('smote 적용 후 target 분포 :\n', y_train_over.value_counts()); print('='*50)

#smote 적용 전 train dataset shape (199362, 29) (199362,)
#smote 적용 후 train dataset shape (398040, 29) (398040,)
#smote 적용 후 target 분포 :
#0    199020
#1    199020
```

---
## Reference

- 파이썬 머신러닝 완벽가이드 서적
