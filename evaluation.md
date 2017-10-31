# Evaluation

* 목표
  * 충분한 평가를 통해서 비즈니스 목표를 달성할 것으로 확신되는 모델을 선정
  * 전체 프로세스를 재검토하고 다음 단계를 결정
* Actions
  * Evaluate Results : 결과가 비즈니스 목표에 부합하는지 확인
  * Review Process : 빠트린 사항이 없도록 중요 항목을 도출하고 전체 프로세스를 요약
  * Determine Next Steps : 다음 단계를 결정
* KDD : \(해석/평가\) 지식
* Process 2 : 검증
* 수리적 모델의 검증과 변수/데이터의 확인

At this stage in the project you have built a model \(or models\) that appears to have high quality, from a data analysis perspective. Before proceeding to final deployment of the model, it is important to more thoroughly evaluate the model, and review the steps executed to construct the model, to be certain it properly achieves the business objectives. A key objective is to determine if there is some important business issue that has not been sufficiently considered. At the end of this phase, a decision on the use of the data mining results should be reached.

## 1. Evaluate Results

여러 모델을 동시 성능 평가  
![](/assets/fmtest.png)

- Classification에서의 Metric 
  - Accuracy : 전체 정답률
  - Precision : 양성 항목 **정답률**
  - Recall : 양성 항목 **검출율**

- Regression에서의 Metric : Distance Between True & Predicted Function 
  - 예측값과 결과값 사이의 오차 거리를 계산 
  - (L2 Norm, L2 Norm, L-Infinite Norm. etc)





### 1.1 성능 평가 인자 \(Classification \)

- Classification에서의 Metric 
  - Accuracy : 전체 정답률
  - Precision : 양성 항목 **정답률**
  - Recall : 양성 항목 **검출율**

* Confusion matrix : [http://blog.naver.com/ilustion/220275811793](http://blog.naver.com/ilustion/220275811793)
* lift chart
* gain chart
* ROC Curve \(classification 에서만\)

#### A. Accuracy

* the percentage of correctly classifies instances out of all instances. 
* It is more useful on a binary classification &gt; multi-class classification problems 
  * because it can be less clear exactly how the accuracy breaks down across those classes

#### B. Confusion matrix : 각 항목 별로 Accuracy 확인시 사용

```
library("SDMTools")
mat <- confusion.matrix(german$y, german$pred, threadhold=0.5)
mat
omission(mat)
sensitivity(mat)
specificity(mat)
prop.correct(mat)
```

* omission.rate: the ommission rate as a proportion of true occurrences misidentified given the defined threshold value
* sensitivity: 1일 확률, 민감도
* specificity: 0일 확률, 특이도
* prop.correct: 모델의 정확도
* kappa statistic : Fleiss의 판단기준..
  * 신뢰도 낮다: 0.4 미만
  * 신뢰도 있다: 0.4 ~ 0.6
  * 신뢰도 높다: 0.6 ~ 0.75
  * 신뢰도 매우 높다: 0.75 초과

###### \[참고\] 분류를 목적하는 상황에서의 평가 척도

* 정확도 . 정밀도 : 참긍정의 수/\(참긍정의 수 + 거짓긍적의 수\) 
* 재현율 : 참긍정의 수/\(참긍정의 수 + 거짓부정의 수\) 
* F점수\(F-score\) : 정밀도와 재현율을 합한값, \(2x정밀도x재현율\)/\(정밀도+재현율\) 
* 향상도\(lift\) 

###### \[참고\] 순서를 매기는 상황에서의 평가 척도

* AUC \(ROC 곡선 아래 면적\), 누적향상도 곡선 아래 면적 
  * 숫자가 높을수록 좋다.
  * ROC커브는 점수 기준을 달리 할때 TP Rate와 FP Rate가 어떻게 달라 지는지 그래프로 표시한 것 

###### \[참고\] 혼돈행렬

![](/assets/cmat.jpg)  
혼돈행렬을 이용하여 구할수 있는 메트릭

| 메트릭 | 계산식 | 의미 |
| --- | --- | --- |
| Precision | $$\frac {TP}{Tp+FP}$$ | Y로 예측된것 중 실제로도 Y인 경우의 비율 |
| Accuracy | $$\frac {TP+TN}{TP+FP+FN+TN}$$ | 전체 예측에서 옳은 예측의 비율 |
| Recall / sesitivity / TP Rate | $$\frac {TP}{TP+FN}$$ | 실제로 Y인 것들 중 예측이 Y로 된 경우의 비율 |
| Specificity | $$\frac {TN}{FP+TN}$$ | 실제로 N인 것들 중 예측이 N로 된 경우의 비율 |
| FP Rate / False alarm | $$\frac {FP}{FP+TN}$$ | Y가 아닌데 Y로 예측된 비율 |
| F1 |  | Precision 과 Recal의 조화 평균 |
| Kappa\(코헨의 카파\) |  | 두 평가자의 평가가 얼마나 일지 하는지 평가 |

* 정확도 : 모델의 정확도
* 민감도 : True 확률
* 특이도 : False 확룰
* 오류율 : 모델의 오류율

###### \[문제 풀이\]

![](/assets/coma.png)

[http://databaser.net/moniwiki/wiki.php/로지스틱회귀분석](http://databaser.net/moniwiki/wiki.php/로지스틱회귀분석)

> 참고: 민감도와 특이도 \#
>
> \*특정 질병에 대한 조사결과..민감도 \(질병에 실제로 걸렸을 때 걸렸다는 검사 결과\)가 99.7%고 특이도 \(질병에 실제로 안 걸렸을 때 안 걸렸다는 검사 결과\)가 98.5%입니다. 이게 무슨 소리냐면, 1000명을 검사했을 때 병이 있는데도 없다고 오진받는 사람은 3명이고 병이 없는데도 있다고 오진되는 사람은 15명 정도라는 거죠.

#### C. Kappa

* classification accuracy, except that it is normalized at the baseline of random chance on your dataset. 
* It is a more useful measure to use on problems that have an imbalance in the classes
  * \(e.g. 70-30 split for classes 0 and 1 and you can achieve 70% accuracy by predicting all instances are for class 0\).

#### D. ROC \(Area Under ROC Curve: AUROC\) also called \(Area Under curve:AUC\)

* ROC is actually the area under the ROC curve or AUC.
  * only suitable for binary classification problems\(e.g. two classes\).
  * The AUC represents a models ability to discriminate between positive and negative classes 
* ROC can be broken down into sensitivity and specificity.  \(Trade-off 관계\)
  * Sensitivity = the true positive rate = recall : It is the number instances from the positive \(first\) class that actually predicted correctly.
  * Specificity = true negative rate : Is the number of instances from the negative class \(second\) class that were actually predicted correctly

#### E. Gini : ROC 확장 버전, 일반적으로 60%이상이면 좋은 모델임

#### F. Logarithmic Loss \(LogLoss\)

* it evaluates the probabilities estimated by the algorithms
* multi-class/ binary classification algorithms. 

### 1.2 성능 평가 인자 \(Classification \)

#### A. RMSE

* the average deviation of the predictions from the observations. 
* It is useful to get a gross idea of how well \(or not\) an algorithm is doing, in the units of the output variable
* RMSE is highly affected by outlier values.  outliers 제거 필수

#### B. R^2 \(= R Squared , coefficient of determination\)

* a “goodness of fit” measure for the predictions to the observations. 
* This is a value between 0 and 1 for no-fit and perfect fit respectively

### 1.3 성능 평가 인자 \(Correlation\)

* 두 확률 변수 사이의 관련성 파악
* 일반적으로 상관 계수는 `피어슨 상관 계수`의미 
* R의 cor\(\)사용 
  * method=c\("pearson","spearman","kendall"\)
* R에서 상관 계수 검정 cor.test\(\)사용 

#### A. 피어슨 상관 계수\(Pearson Correlation Coefficient\)

* 두 변수 간의 `선형적` 상관 관계 측정
* 연속형 데이터에 적합
  * eg. 국어 & 영어 점수 간의 상관 관계 
* \[-1,1\]사이의 값을 가짐, 0은 상관 관계 없음 의미 
* 정의 

  $$
  \rho(X,Y) = \frac{cov(X,Y)}{\sigma_X\sigma_Y}
  $$

> $$\rho(X,Y)$$는 공분산, 두 확률 변수가 얼마나 함께 변하는가 측정

#### B. 스피어만 상관 계수\(Spearman's Rank Correlation Cofficient\)

* 두 데이터의 실제 데이터 대신 두 값의 `순위(rank)`를 사용
* 두 변수 간의 `비선형` 연관성 파악 가능
* 이산형, 순서형 데이터에 적용 가능 
  * eg. 국어 & 영어 석차의 상관 관계
* \[-1,1\]사이의 값을 가짐, 0은 상관 관계 없음 의미 
* 정의 


$$
\rho = \frac{\sum_i(x_i-\overline x)(y_i-\overline y)}{\sqrt{\sum_i(x_i-\overline x)^2}\sqrt{\sum_i(y_i-\overline y)^2}}
$$


#### C. 켄달의 순위 상관 계수\(Kendal's Rank Correlation Cofficient\)

* \(X,Y\)순서쌍으로 데이터가 있을때
  * x가 커질때 y도 커지면 부합
  * x가 커질때 y가 작아지면 비부합
* \[-1,1\]사이의 값을 가짐, 1은 부합 데이터쌍의 비율이 100%, -1은 비부합 데이터쌍의 비율이 100%, 0은 상관 관계 없음 의미
* 정의 

  $$
  \tau = \frac{(부합 테이터쌍의 수)-(비부합 데이터쌍의 수)}{\frac{1}{2}n(n-1)}
  $$

### 1.4 성능 평가 인자 \(Regression\)

> 선형회귀 결과에 한정일수 있음

- Regression에서의 Metric : Distance Between True & Predicted Function 
  - 예측값과 결과값 사이의 오차 거리를 계산 
  - (L2 Norm, L2 Norm, L-Infinite Norm. etc)

![](https://i.imgur.com/uXq90EF.png)

#### A. 결정계수\($$R^2$$\)

* 모델이 데이터의 분산을 얼마나 설명 하는지 표현

#### B. 조정 결정 계수 \($$Adjusted R^2$$\)

* 모델이 데이터의 분산을 얼마나 설명 하는지 표현

#### C. 설명 변수 평가

* `*`기호를 사용하여 $$p-value$$ 표현 

#### D. F 통계량

* 모델이 통계적으로 얼마나 의미가 있는지 표현 
* MSR/MSE의 비율을 F 분포를 사용해 검정한 것

###### \# \[참고\] 모델 진단 그래프

![](/assets/plot_m.PNG)

## 2. Approved Models

## 3. Determine Next Steps


---
> 추천 읽을꺼리 : [Classification 모델 평가 기준 1편- Precision과 Recall](https://brunch.co.kr/@chris-song/54)
