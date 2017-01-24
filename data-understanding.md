# Data Understanding
The data understanding phase starts with an initial data collection and proceeds with activities in order to get familiar with the data, to identify data quality problems, to discover first insights into the data, or to detect interesting subsets to form hypotheses for hidden information.


## 1. Collection Initial Data 

### 클래스 불균형(Class Imbalance)
* 구분할 각 분류에 해당하는 데이터의 비율이 반반이 아닌 경우 데이터가 많은쪽으로 결과가 치우침 
* 해결법_1 : 데이터가 적은쪽에 가중치 or 데이터가 적은쪽을 잘못 분류시 Cost/Loss 부과 (모델링 함수의 param, loss, cost파라미터 이용)
* 해결법_2 : 모델을 만드는 훈견 데이터를 직접 조정 (Up sampling, Down Sampling, Hybrid-SMOTE) 
    * Up sampling : 데이터가 적은쪽을 표본으로 더 많이 추출 
    * Down Sampling : 데이터가 많은 쪽을 적게 추출 
        * downSample(설명변수, 예측대상 분류인자) #d <- downSample(r435, r435$lecture)
    * SMOTE : KNN을 이용하여 낮은 분류으 ㅣ데이터 생성  

![](/assets/sampling.png)
http://www.r-bloggers.com/down-sampling-using-random-forests/


## 2. Describe Data



## 3. Explore Data


## 4. Verfy Data Quality 

### 이상치 
이상 관측치(Unusual Observation) 판단하기 
* 정의 : An observation that lies an abnormal distance from other values in a random sample from a population

이상치(Outliner)를 파악 하는 방법 
* 일변량 : 표준점수(즉, z-score)가 2.5~4 이상인 표본(표본수에 따라 기준은 달라짐) - outliers()
* 이변량 : 산포도를 이용하여 독립변수와 종속변수의 관계성 테스트하여 특정 신뢰구간에 포함되지 않은 표본 - mvoutlier() , corr.plot() 사용 
* 다변량 : 마하로노비스 D2 값을 이용, D2/df가 2.5~4이상인 표본(표본수에 따라 기준은 달라짐) - library(chemometrics) - Moulier() 
* 큰지레점(High-leverage observation)
* 영향관측치(Influential observation)


이상 관측치 판단하기 : http://blog.naver.com/ilustion/220285462430

이상치 : http://blog.naver.com/jinwon_hong/140160660331

Outlier : http://www.itl.nist.gov/div898/handbook/prc/section1/prc16.htm
http://blog.naver.com/jinwon_hong/140160660331
https://en.wikibooks.org/wiki/Data_Mining_Algorithms_In_R/Classification/Outliers

https://www.youtube.com/watch?v=ckxEZDN1iok

http://www.dbs.ifi.lmu.de/~zimek/publications/KDD2010/kdd10-outlier-tutorial.pdf

http://www.r-statistics.com/2011/01/how-to-label-all-the-outliers-in-a-boxplot/

http://blog.naver.com/jinwon_hong/140160660331
https://en.wikibooks.org/wiki/Data_Mining_Algorithms_In_R/Classification/Outliers


