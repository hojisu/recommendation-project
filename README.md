# Recommendation System - Alternating Least Square Implicit Collaborative Filtering

## Contents
### [01. Exploratory Data Analysis](https://github.com/hojisu/recommendation-project/tree/master/01-Exploratory-Data-Analysis)
### [02. Recommend System - ALS](https://github.com/hojisu/recommendation-project/tree/master/02-Recommend-System-ALS)

## 데이터
롯데멤버스, L.pay|L.POINT, 제6회 L.POINT Big Data Competition에서 데이터를 제공받았다. 
온라인 행동 정보, 거래 정보, 고객 Demographic 정보, 상품분류 정보 데이터가 있다.

## Exploratory Daya Analysis
데이터를 살펴보니 추천시스템이 많이 사용되는 explicit한 점수(rank)데이터를 포함하고 있지 않았다. 그리하여 고객이 구매한 상품 유무를 rank데이터로 생각하여 
전처리를 진행하였다. 

## Recommend System - ALS
유저의 비선호도가 반영되지 않은 Implicit Dataset은 Latent Factor model 가운데 Matrix Factorization이 적합하다. 
평점 행렬을 사용자와 아이템 Latent Factor 행렬로 분해하고 분해된 행렬을 다시 곱하여 예측 평점 행렬을 계산한다. Latent Factor Matrix가 적절하게 학습이 
되었다면 예측된 값과 실제 값이 유사한 결과를 낼 것이다. 예측 평점 행렬의 오차가 최소화하도록 Alternating Least Square 알고리즘을 사용하였다. 
ALS 알고리즘은 사용자와 아이템 둘 중 하나를 고정(상수로 생각하고)시키고 다른 하나를 최적화 시킨다. 이 과정을 번갈아가며 반복한다. 
먼저 사용자 혹은 아이템의 Latent Factor 행렬을 아주 작은 랜덤 값으로 초기화 합니다. 그 다음 둘 중 하나를 상수처럼 고정시켜 Loss Function을 
Convex Function으로 만듭니다. 그리고 이를 미분한 다음 비분 값을 0으로 만드는 사용자 혹은 아이템의 Latent Factor 행렬을 계산합니다.
이 과정을 사용자 한번, 아이템 한번 반복하면서 최적의 X, Y를 찾아내는 것입니다. 
