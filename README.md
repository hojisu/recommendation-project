# Recommendation System - Alternating Least Square Implicit Collaborative Filtering

## Contents
### [01. Exploratory Data Analysis](https://github.com/hojisu/recommendation-project/tree/master/01-Exploratory-Data-Analysis)
### [02. Recommend System - ALS](https://github.com/hojisu/recommendation-project/tree/master/02-Recommend-System-ALS)

## 데이터
롯데멤버스, L.pay|L.POINT, 제6회 L.POINT Big Data Competition에서 데이터를 제공
거래 정보, 상품분류 정보 데이터 사용


## Exploratory Daya Analysis
implicit 데이터로 상품에 대한 비선호도가 반영되지 않아 고객이 구매한 상품 수량으로 대체
user, item, 구매수량으로 spare matrix 형태로 변환


## Recommend System - Matrix Factorization
사용자와 아이템을 Latent Factor로 분해하고 이를 각각 학습시키는 Matrix Factorization기법을 사용
최적화를 위해 Alternating Least Square 알고리즘을 사용

implicit 데이터에서 선호도와 신뢰도를 정의하였습니다. 
- 상품을 구매했으면 선호, 구매하지 않았으면 비선호로 정의
- 신뢰도는 구매 이력이 없는 데이터는 신뢰도를 판단할 수 없다고 정의


## Evaluation
Training Set에 20%를 가려서 아이템을 구매하지 않은 것처럼 구현 
사용자에게 추천된 아이템 중 실제로 구매한 아이템의 수 확인 


References
- Yifan Hu, Yehuda Koren, Chris Volinsky : Collaborative Filtering for Implicit Feedback Datasets
