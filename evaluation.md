# Evaluation

At this stage in the project you have built a model \(or models\) that appears to have high quality, from a data analysis perspective. Before proceeding to final deployment of the model, it is important to more thoroughly evaluate the model, and review the steps executed to construct the model, to be certain it properly achieves the business objectives. A key objective is to determine if there is some important business issue that has not been sufficiently considered. At the end of this phase, a decision on the use of the data mining results should be reached.

* 순서를 매기는 상황에서의 평가 척도 : AUC \(ROC 곡선 아래 면적\), 누적향상도 곡선 아래 면적 
* 분류를 목적하는 상황에서의 평가 척도 
  * 정확도 . 정밀도 : 참긍정의 수/\(참긍정의 수 + 거짓긍적의 수\) 
  * 재현율 : 참긍정의 수/\(참긍정의 수 + 거짓부정의 수\) 
  * F점수\(F-score\) : 정밀도와 재현율을 합한값, \(2x정밀도x재현율\)/\(정밀도+재현율\) 
  * 향상도\(lift\) 

## 1. Evaluate Results
여러 모델을 동시 성능 평가
![](/assets/fmtest.png)

classification performance 
* Confusion matrix : http://blog.naver.com/ilustion/220275811793
* lift chart
* gain chart
* ROC Curve (classification 에서만)


### Confusion matrix
```
library("SDMTools")
mat <- confusion.matrix(german$y, german$pred, threadhold=0.5)
mat
omission(mat)
sensitivity(mat)
specificity(mat)
prop.correct(mat)
```
* AUC(area under curve): ROC curve 아래의 면적, 숫자가 높을수록 좋다.
* omission.rate: the ommission rate as a proportion of true occurrences misidentified given the defined threshold value
* sensitivity: 1일 확률, 민감도
* specificity: 0일 확률, 특이도
* prop.correct: 모델의 정확도
* kappa statistic : Fleiss의 판단기준..
  * 신뢰도 낮다: 0.4 미만
  * 신뢰도 있다: 0.4 ~ 0.6
  * 신뢰도 높다: 0.6 ~ 0.75
  * 신뢰도 매우 높다: 0.75 초과
  
![](/assets/coma.png)
* 정확도 : 모델의 정확도
* 민감도 : True 확률
* 특이도 : False 확룰
* 오류율 : 모델의 오류율

http://databaser.net/moniwiki/wiki.php/%EB%A1%9C%EC%A7%80%EC%8A%A4%ED%8B%B1%ED%9A%8C%EA%B7%80%EB%B6%84%EC%84%9D

> 참고: 민감도와 특이도 #

> *특정 질병에 대한 조사결과..민감도 (질병에 실제로 걸렸을 때 걸렸다는 검사 결과)가 99.7%고 특이도 (질병에 실제로 안 걸렸을 때 안 걸렸다는 검사 결과)가 98.5%입니다. 이게 무슨 소리냐면, 1000명을 검사했을 때 병이 있는데도 없다고 오진받는 사람은 3명이고 병이 없는데도 있다고 오진되는 사람은 15명 정도라는 거죠.


## 2. Approved Models







## 3. Determine Next Steps



