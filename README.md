# Recommendation System - Alternating Least Square Implicit Collaborative Filtering

## Contents
### [01. Exploratory Data Analysis](https://github.com/hojisu/recommendation-project/tree/master/01-Exploratory-Data-Analysis)
### [02. Recommend System - ALS](https://github.com/hojisu/recommendation-project/tree/master/02-Recommend-System-ALS)

## 데이터
롯데멤버스, L.pay|L.POINT, 제6회 L.POINT Big Data Competition에서 데이터를 제공받았습니다.
온라인 행동 정보, 거래 정보, 고객 Demographic 정보, 상품분류 정보 데이터가 있습니다.

## Exploratory Daya Analysis
데이터는 implicit 데이터였습니다. 상품에 대한 비선호도가 반영되지 않았습니다. 추천시스템이 많이 사용되는 explicit한 점수(rank)데이터를 포함하고 있지 않기 때문에 고객이 구매한 상품 구매 수량으로 데이터 전처리를 진행하였습니다. 

## Recommend System - ALS
implicit 데이터로 사용자의 비선호도가 반영되지 않았기 때문에 Latent Factor model이 적합하다고 생각하였고 사용자와 아이템을 Latent Factor로 분해하고 이를 각각 학습시키는 Matrix Factorization기법을 사용하였습니다. 평점 행렬을 사용자와 아이템 Latent Factor 행렬로 분해하고 분해된 행렬을 다시 곱하여 예측 평점 행렬을 계산한다. Latent Factor Matrix가 적절하게 학습이 되었다면 예측된 값과 실제 값이 유사한 결과를 낼 것이다. 예측 평점 행렬의 오차가 최소화하도록 Alternating Least Square 알고리즘을 사용하였다. ALS은 사용자와 아이템 둘 중 하나를 고정(상수로 생각하고)시키고 다른 하나를 최적화 시킨다. 이 과정을 계속 반복하면서 최적의 사용자와 아이템 Latent Factor를 찾습니다.

implicit 데이터에는 평점처럼 명확히 사람의 선호도를 나타내는 지표가 없으므로 implicit 데이터에서 선호도와 신뢰도를 정의하였습니다. 선호와 비선호 정의는 상품을 구매했으면 선호한 것으로 정의하고, 구매하지 않았으면 비선호 한 것으로 정의하였습니다. 신뢰도는 구매 이력이 없는 데이터는 신뢰도를 판단할 수 없다고 정의하였습니다. 신뢰도 변수를 도입하여 구매하지 않은 데이터는 낮은 신뢰도 값을 갖게 하여 오차 함수 계산 시 영향력이 작게 조절하였고 구매 수량이 많으면 영향력이 높아지게 하였습니다.

먼저 사용자 혹은 아이템의 Latent Factor 행렬을 아주 작은 랜덤 값으로 초기화 하였습니다. 그 다음 둘 중 하나를 상수처럼 고정시켜 Loss Function을 
Convex Function으로 만들었습니다. 그리고 이를 미분한 다음 미분 값을 0으로 만드는 사용자 혹은 아이템의 Latent Factor 행렬을 계산합니다. 이 과정을 사용자 한번, 아이템 한번 반복하면서 최적의 X, Y를 찾았다.

모델 성능을 평가하기 위해 Traning Set에 20%를 가려서 아이템을 구매하지 않은 것처럼 보이도록 하였습니다. 그 다음 사용자에게 추천된 아이템 중 실제로 구매한 아이템의 수가 얼마나 되는지 확인하였습니다. 사용자에게 추천시스템에 의해 추천받은 아이템이 실제 구매한 상품에 있는지 확인하였습니다.

## References
- Yifan Hu, Yehuda Koren, Chris Volinsky : Collaborative Filtering for Implicit Feedback Datasets
