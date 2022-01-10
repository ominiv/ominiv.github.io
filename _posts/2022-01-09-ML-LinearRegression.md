---
title: ML/Regression LinearRegression
date: 2022-01-09 00:00:01
categories:

- ML
tags:
- Regression
- LinearRegression
---

# [ML/Regression] LinearRegression

- sklearn의 linear_models 모듈은 다양한 선형기반 회귀를 클래스로 구현해 제공한다. [link](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.linear_model)
- 오늘은 다양한 선형기반 회귀들 중 **규제가 적용되지 않는 Linear Regression**에 대해 알아보자

---
## LinearRegression Class - Ordinary Least Squres

LinearRegression 클래스는 예측값과 실제값의 RSS를 최소화해 OLS추정방식으로 구현한 클래스이다.<br>`class sklearn.linear_model.LinearRegression(*, fit_intercept=True, normalize='deprecated', copy_X=True, n_jobs=None, positive=False)`<br> LinearRegression 클래스는 fit() 메서드로 X,y 배열을 입력받으면 회귀계수를 `coef_`속성에 저장한다.

ordinary least squres기반의 회귀계수 계산은 입력 피처의 독립성에 많은 영향을 받는다.<br>피처간의 상관관계가 매우 놓은 경우 분산이 매우 커져서 오류에 매우 민감해진다. <br>위와 같은 현상을 다중공선성(multi - collinearity)라고 하며 일반적으로 매우 많은 피처가 다중 공선성 문제를 가지고 있다면 PCA를 통해 차원축소를 고려한다.

### tutorial
사이킷런의 평가지표 기준은 높은 값일 수록 좋은 모델인 반해 일반적으로 회귀는 **MSE값이 낮을수록** 좋은 회귀모델이다.사이킷런의 metric 평가기준에 MSE를 부합시키기 위해 `scoring='neg_mean_squared_error'` 로 사이킷런의 Scoring 함수를 호출하면 모델에서 계산된 MSE값에 -1를 곱해서 반환한다.<br>즉, `cross_val_score()`의 반환값에 -1을 곱해주어야 MSE를 도출해낼수있다.
```python
X_train, X_test, y_train, y_test = train_test_split(X_feature.iloc[:,:-1], y_label, test_size = 0.3)
# 모델생성 / 학습 / 예측
lr = LinearRegression()
lr.fit(X_train,y_train)
lr_pred =lr.predict(X_test)

mse = mean_squared_error(y_test,lr_pred)
print('MSE : {0:.4f} / RMSE : {1:.4f} / R^2 : {2:.4f}'.format(mse,np.sqrt(mse),r2_score(y_test,lr_pred)))
print('절편값 : ',np.round(lr.intercept_,1))
print('회귀계수값 : ',np.round(lr.coef_,1))

# cross_val_score으로 5폴드 세트로 MSE를 구한 뒤 이를 기반으로 RMSE를 구함
neg_mse_scores = cross_val_score(lr, X_train,y_train,scoring='neg_mean_squared_error', cv=5)
rmse_score = np.sqrt(-1*neg_mse_scores)
avg_rmse = np.average(rmse_score)

# cross_val_score(scoring='neg_maen_squared_error')으로 반환된 값은 모두 음수
print('5 folds의 개별 Negative MSE scores :',np.round(neg_mse_scores,2))
print('5 folds의 개별 RMSE scores :',np.round(rmse_score,2))
print('5 folds의 개별 RMSE 평균 :',avg_rmse)
```
---

##  Practice

- LinearRegression [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/boston%20dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
