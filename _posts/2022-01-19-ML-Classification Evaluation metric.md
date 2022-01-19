---
title: ML/Classification Evaluation
date: 2022-01-19 00:00:01
categories:
- ML
tags:
- Classification
- Evaluation Metric
---

# [ML/Classification] Evaluation
ML은 데이터가공/변환 , 모델 학습/예측, 그리고 평가의 프로세스로 구성됩니다.<br>일반적으로 모델의 종류에 따라 Evaluation metric이 달라집니다.

분류 성능평가 지표부터 살펴보자.<br>분류는 결정클래스 값 종류의 유형에 따라 **이진분류**와 여러개의 결정클래스 값을 가지는 **멀티분류**로 나뉩니다. 

---

## Confusion Matrix

이진분류에서 성능지표로 잘 활용됨<Br>학습된 분류모델이 예측을 수행하면서 얼마나 헷갈리고 있는지 쉽게 보여줌

| Actual \ Prediction | Negative      | Positive      |
| ------------------- | ------------- | ------------- |
| Negative            | TN (TRUE)     | FP (1종 에러) |
| Positive            | FN (2종 에러) | TP (TRUE)     |

*2종 에러가 더 심각한 결과를 초래함.*

---

## Accuracy

: 예측결과와 실제값이 동일한 건수 / 전체 데이터수<br>: (TN + TP) / (TN + TP + FN + FP)

---

## Precision / Recall

- 불균형한 데이터의 경우, Accuracy 보다 Precision, Recall 지표가 더 선호됩니다. <br>Positive 데이터세트의 예측 성능에 초점을 맞춤 평가지표
- 가장 좋은 성능평가는 Precision, Recall 모두 높은 수치를 얻는 것임
-  분류하려는 업무 특성항 정밀도와 재현율를 특히 강조해야 할 경우,  
	분류의 threshold를 조정해 precision, Recall 값을 높일 수있음.  이를 Trade - off라 칭함
	분류 임계값을 낮출수록 Recall 증가 
- **precision  = 정밀도, 양성 예측도**<br>  : TP / (TP+FP) <br>  : 예측을 Positive로 한  것 중에 실제값과 동일한 비율
  즉, FP(type1 error)를 낮추는데 초점을 둠 (*활용 예시 , 스팸메일 분류* )

- **recall  = 재현율, Sensitivity , TPR**<br>  : TP / (TP+FN) <br>  : 실제값이 Positive인 것 중에 예측값과 동일한 비율<br>  즉, FN(type2 error)을 낮추는데 초점을 둠(*활용 예시, 암판단*)<Br>    : 암 양성예측모델

---

## F1 score
: 2/(1/recall + 1/precision)<br>: 2 x ( (precision x recall) / (precision + recall) )<br>Precision, recall 값을 결합한 지표. <br>정밀도와 재현율이 어느 한쪽으로 치우치지 않는 수치를 나타낼때 상대적으로 높은 값을 가짐

---

## ROC curve &  AUC score

이진분류에서 중요하게 사용됨.

- **ROC Curve**<br>  : Receiver Operation Characteristic Curve<br>  : FPR이 변할때 TPR이  어떻게 변하는지 나타내는 곡선 (x축 FPR , y축 TPR)
- **AUC score**<Br>  : Area under curve<br>  : 곡선 아래 면적을 나타내는 수치 <Br>  : 1에 가까울 수록 좋은 성능을 의미함


