# Modeling
In this phase, various modeling techniques are selected and applied, and their parameters are calibrated to optimal values. Typically, there are several techniques for the same data mining problem type. Some techniques have specific requirements on the form of data. Therefore, stepping back to the data preparation phase is often needed.

<!-- toc -->

## 1. Select Modeling Technique

## 2. Generate Test Design 

### 2.1 Sampling 
수집된 데이터 중에서 테스트용과 검증용으로 7:3(일반적)으로 나누기

#### A. 단순 임의 추출 
* 각 데이터를 추출할 확률을 동일하게 하여 표본을 추출하는 방법 
    1. 복원 추출
    2. 비복원 추출 
* 가중치 적용이 필요 할 경우 `prob`파라미터 설정 

```
#sample()
```

#### B. 층화 임의 추출
* 데이터가 중첩 없이 분활될수 있는 경우/성격이 명확히 다를 경우 수행 하면 더 정확한 분석 결과를 얻을수 있다. 
* eg: 남성과 여성으로 나누(=층)어서 표본 추출

```{r}
# sampleing::strata()


# 파라미터중 Poisson은 포아송 추출로 각 데이터의 추출 확률을 다르게 설정하고 각 데이터를 독립적으로 추출하는 경우 설정 
```
#### C. 계통 추출 
* 순서/시간의 영향이 있는 데이터의 경우 $$k$$번째 항목을 추출하는 방법 
* eg: 아침부터 밤까지 지나간 차량의 넘버 추출 

```{r}
#doBy 패키지 sampleBy()
```


## 3. Build Model Parameter settings
파라미터 튜닝 : trControl()
![](/assets/tr.png)

파라미터 튜닝 최적화 : 
* preprocess() : principal component analysis 또는 independent component analysis.
    * centering & scaling, imputation, applying the spatial sign transformation, feature extraction
* expand.grid() : 범위 지정, 다양한 조합에 대한 모델 성능평가시 조합의 목록 생성  
    * ex: 나무개수 1~10, 고려할 변수 개수 1~3
    * grid <- expand.grid(ntree=c(10,100,200), mtry=c(3,4))

튜닝(caret 패키지를 이용하여) 

1. 모델 선정 
    * 213개 지원 : http://topepo.github.io/caret/modelList.html
2. 튜닝할 파라미터 선정 : http://topepo.github.io/caret/bytag.html
3. Resampling 방법 정의  trainControl()
    * k-fold cross-validation (once or repeated),
    * leave-one-out cross-validation
    * bootstrap
4. 결과 확인

> http://rpackages.ianhowson.com/cran/caret/man/models.html



http://topepo.github.io/caret/training.html
http://machinelearningmastery.com/compare-models-and-select-the-best-using-the-caret-r-package/


## 4. Assess Model 
### 모델 평가-교차 검증(Cross Validation)
* 훈련데이터와 테스트 데이터를 분리하여 모델을 만드는 방법 중 하나 
* 데이터를 k개의 조각으로 나누어 훈련/테스트 반복 (K-fold Cross Validation)
    1. 데이터를 10등분하여 D1, D2, D3 ~ D10으로 분할한다.
    2. K값을 1로 초기화 한다.
    3. $$D_k$$를 검증 데이터, 그외를 훈련데이터로 하여 모델을 생성 한다. 
    4. 검증 데이터 Dk를 사용해 모델을 평가 한다. 평가된 모델의 성능을 Pk라 한다. 
    5. K가 9이하인 값이면 K=k+1을 하고 3단계로 간다. 만약 K=10이면 종료 한다. 

교차 검증 후 테스트

1. 데이터를 훈련 데이터와 테스트 데이터로 분리한다. 
2. 훈련 데이터에 대해 k겹 교차 검증을 수행하여 어떤 모델링 기법이 가장 우수한지를 결정한다. 
3. 해당 모델링 기법으로 훈련 데이터 전체를 사용해 최종 모델을 만든다. 
4. 테스트 데이터에 최종 모델을 적용해 성능을 평가하고, 그 결과를 최종 모델과 함께 제출한다. 

교차 검증 함수들
* cvTools::cvFolds() : n개의 관찰을 K겹 교차 검증의 R회 반복으로 분할한다. 
* caret::creatDataPartition() : 데이터를 훈련 데이터와 데스트 데이터로 분활한다.
* Caret::creatFolds() : 데이터를 K겹 교차 검증으로 분할한다. 
* Caret::creatMultiFolds() :데이터를 교차 검증의 Times 반복으로 분할한다. 

https://thebook.io/006723/Ch09/03/03/06/

## caret패키지 trainControl() 방법들 
Bootstrap
* 복원 추출 기반 ReSampling 방식 사용 
* train_control <- trainControl(method="boot", number=100)

k-fold Cross Validation
* 데이터를 K개의 subset으로 잘라서 수행
* train_control <- trainControl(method="cv", number=10)

Repeated k-fold Cross Validation (저자 추천 방식)
* 데이터를 K개의 subset으로 잘라서 수행하는 것을 n번만큼 반복
* train_control <- trainControl(method="repeatedcv", number=10, repeats=3)

Leave One Out Cross Validation (LOOCV)
* train_control <- trainControl(method="LOOCV")

http://machinelearningmastery.com/how-to-estimate-model-accuracy-in-r-using-the-caret-package/


> 과적합
> * 특정 데이터를 이용하여 모델 생성 후 해당 데이터에는 잘 동작하지만, 새로운 데이터에는 좋지 않는 성능을 보이는 경우 
> * 평가 방법 : 특정데이터의 일부는 훈련 모델(약 70%), 나머지는 테스트로 사용해 평가 

## caret패키지 이용한 Data Slicing
createDataPartition
* p의 %로 분할, Index값 Return 
* createDataPartition(y=spam$type, p=0.8, list=FALSE)

createFolds
* k-fold방법을 이용한 Cross Validation시 사용 
* folds <- createFolds(y=spam$type, k=10, list=TRUE, returnTrain = FALSE)
* 테스트 케이스 생성 : sapply(folds, length)

createResample
* Resampling(Bootstrapping)방법을 이용한 Cross Validation시 사용 
* K-fold와 다르게 샘플에 중복값 존재 
* folds <- createResample(y=spam$type, times=10, list=TRUE)

createTimeSlice
* 시계열 데이터 Slicing 시 사용 
* folds <- createTimeSlices(y=time, initialWindow = 20, horizon = 10)
* 트레이닝 20개, 테스트 10가 반복 수행 

참고 : http://goodtogreate.tistory.com/m/post/entry/Week-02-Caret-Package-dataSlicing
