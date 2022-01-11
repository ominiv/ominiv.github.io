---
title: ML/Regression Logistic Regression
date: 2022-01-11 00:00:01
categories:

- ML
tags:
- Regression
- Logistic
---

# [ML/Regression] Logistic Regression
로지스틱 회귀는 선형회귀 방식을 분류에 적용한 알고리즘이다.<br>다만 다른 회귀와 다른점은 학습을 통해 선형함수의 회귀 최적선을 찾는 것이 아니라 **시그모이드(sigmoid) 함수의 최적선을 찾고 이 시그모이드 함수의 반환값을 확률로 간주해 확률에 따라 분류를 결정한다.**

---

## Tutorial

```python
# 학습 / 예측 / 평가
model = LogisticRegression(solver='liblinear')
model.fit(X_train,y_train)
y_pred = model.predict(X_test)
get_clf_eval(y_pred, y_test)
```

---

## Hyperparameter turning

Logistic Regression의 주요 하이퍼파라미터는 penalty와 C가 존재한다.  [link](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)<br>penalty는 규제유형을 의미하고, C는 $\frac{1}{alpha}$를 의미한다. alpha가 커질수록 회귀계수는 작아진다.<br>`penalty{‘l1’, ‘l2’, ‘elasticnet’, ‘none’}, default=’l2’`
```python
params = {
          'penalty' : ['l1','l2'],
          'C' : [0.01,0.1,1,5,10]
}
grid_clf = GridSearchCV(model,param_grid=params,cv=5,scoring='accuracy')
grid_clf.fit(X_train,y_train)
print('최적 파라미터:\n', grid_clf.best_params_)
print('최적 정확도:\n', grid_clf.best_score_)
```

---

##  Practice

- Logistic Regression [link](https://github.com/ominiv/Practice_ML/blob/master/Practice/breast%20cancer%20dataset.ipynb)

-----

## Reference

- 파이썬 머신러닝 완벽가이드 서적
