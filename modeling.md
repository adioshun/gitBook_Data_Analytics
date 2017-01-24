# Modeling
In this phase, various modeling techniques are selected and applied, and their parameters are calibrated to optimal values. Typically, there are several techniques for the same data mining problem type. Some techniques have specific requirements on the form of data. Therefore, stepping back to the data preparation phase is often needed.

## 1. Select Modeling Technique

## 2. Generate Test Design 


## 3. Build Model Parameter settings
파라미터 튜닝 : trControl()
![](/assets/tr.png)

파라미터 튜닝 최적화 : 
* preprocess() : principal component analysis 또는 independent component analysis.
    * centering & scaling, imputation, applying the spatial sign transformation, feature extraction
* expand.grid() : 범위 지정, 다양한 조합에 대한 모델 성능평가시 조합의 목록 생성  
    * ex: 나무개수 1~10, 고려할 변수 개수 1~3
    * grid <- expand.grid(ntree=c(10,100,200), mtry=c(3,4))


http://topepo.github.io/caret/training.html
http://machinelearningmastery.com/compare-models-and-select-the-best-using-the-caret-r-package/


## 4. Assess Model 
