---
title: ML/Regression 회귀 평가 지표
date: 2022-01-09 00:00:01
categories:

- ML
tags:
- Regression
- Evaluation Metric
---

# [ML/Regression] 회귀 평가 지표
회귀 평가를 위한 지표는 실제값과 회귀 예측값의 차이를 기반으로 한 지표가 중심이다. <Br>대부분 잔차의 절대값 평균과 제곱을 이용한다. <Br> 회귀의 성능을 평가하는 지표는 다음과 같다.

| 평가지표 |  설명  | 수식 |
| -----| -------------| ---------|
| MAE |  mean absolute Error; 실제값과 예측값이 차이의 절대값의 평균 | $MAE = \frac{1}{n}\sum_{i=1}^{n}(\vert Y_i - \widehat{Y_i}\vert)$ |
| MSE |  mean squred Error; 실제값과 예측값의 차이의 제곱해 평균  | $MSE = \frac{1}{n}\sum_{i=1}^{n}(Y_i - \widehat{Y_i})^2$ |
| RMSE|  sqrt(MSE) | $RMSE = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(Y_i - \widehat{Y_i})^2}$ |
| $R^2$ |  분산기바으로 예측성능을 평가함; 실제값의 분산대비 예측값의 분산을 지표로하며 1에 가까울수록 예측 정확도가 높다. | $R^2 = \frac{예측값 Variance}{실제값 Variance}$ |


---

## Reference

- 파이썬 머신러닝 완벽가이드 서적
