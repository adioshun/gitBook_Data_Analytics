# Data Preparation
The data preparation phase covers all activities to construct the final dataset (data that will be fed into the modeling tool(s)) from the initial raw data. Data preparation tasks are likely to be performed multiple times, and not in any prescribed order. Tasks include table, record, and attribute selection as well as transformation and cleaning of data for modeling tools.

데이터 Preparation단계는 다시 두 단계로 나눌수 있다. 

* 전처리 :수집한 데이터를 저장소에 적재하기 위한 작업으로 데이터 필터링, 유형 변환, 정제 등 기술 활용

* 후처리 : 저장된 데이터를 분석이 용이하도록 가공하는 작업으로 변환, 통합, 축소 등 기술 활용

| 분류                      | 설명                                                                                                                                                               |     |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| 데이터 여과 (Filtering)      | .오류 발견, 보정, 삭제 및 중복성 확인 등의 과정을 통해 데이터 품질을 향상 시키는 기술                                                                                                              ||
| 데이터 변환(Transformation)  | -데이터 유형 변환 등 데이터 분석이 용이한 형태로 변환하는 기술 <br/> -정규화(normalization), 집합화(Aggregation), 요약(summarization), 계층 생성 등의 방법활용. ETL(extraction/transformation/loading) 도구 제공중||
| 데이터 정제(Cleansing)       | . 결측치들을 채워 넣고, 이상치를 식별 또는 제거하고, 잡음 섞인 데이터를 평활화하여 데이터의 불일치성을 교정하는 기술 ※ 일반적으로 데이터는 불완전하고, 잡음이 섞여있고, 일관성이 없기 때문에 데이터 정제가 필요||
| 데이터 통합(Integration)     | . 데이터 분석이 용이하도록 유사 데이터 및 연계가 필요한 데이터(또는 DB)들을 통합하는기술                                                                                                             ||
| 데이터 축소(Reduction)       | . 분석 컴퓨팅 시간을 단축할 수 있도록 데이터 분석에 활용되지 않는 항목 등을 제거하는기술                                                                                                              ||

1. 데이터 여과 : 중복성, 오류 제거, 저품질 제거
2. 데이터 변환 : 다양한 형식에서 일관성 있는 형식으로 변환(분석 용의성 위해)
    * 평활화(Smoothing) : 데이터로부터 잡음을 제거하기 위해 데이터 추세에 벗어나는 값들을 변환 (cf. outliner)
    * 집계(Aggregation) : 다양한 차원의 방법으로 데이터를 요약
    * 일반화(Generalization) : 특정 구간에 분포하는 값으로 스케일을 변화
    * 정규화(Normalization) : 데이터에 대한 최소-최대 정규화, z-스코어 정규화, 소수 스케일링 등 통계적 기법 적용
    * 속성 생성(Attribute/feature construction) : 데이터 통합을 위해 새로운 속성이나 특징을 만드는 방법으로 주어진 여러 데이터 분포를 대표할 수 있는 새로운 속성/특징 활용
3. 데이터 정제 :수집된 데이터의 불일치성을 교정하기 위한 방식으로 결측치(Missing Value) 처리, 잡음(Noise) 처리 기술 활용
![](/assets/missing.png)
![](/assets/noisy.png)
4. 데이터 통합 : 출처가 다른 상호 연관성이 있는 데이터들을 하나로 결합하는 기술로 다음 사항들을 고려
    * 데이터 통합 시 동일한 데이터가 입력 될 수 있으므로 연관관계 분석 등을 통해 중복 데이터를 검출 할 것
    * 데이터 통합 전·후 수치·통계 등 데이터 값들이 일치 할 수 있도록 검증
    * 통합 대상 entity가 통합 이후에 동일한지 여부를 확인하기 위한 동일성 검사 수행
    * 표현 단위(파운드와 kg, inch와 cm, 시간 등) 등 서로 다른 방식에 대해 표현을 일치할 수 있도록 변환

4. 데이터 축소 : 분석에 불필요한 데이터를 축소하여 고유한 특성은 손상되지 않도록 하고 분석에 대한 효율성을 증대
![](/assets/pca_de.png)


## 1. Select Data

## 2. Clean Data


## 3. Construct Data


## 4. Integrate Data

## 5. Format Data 