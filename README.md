# 🚀 머신러닝 앙상블 모델: 부스팅과 스태킹

이 레포지토리는 머신러닝 앙상블 모델의 부스팅과 스태킹 방법에 대한 설명과 예제 코드를 포함하고 있습니다.

## 앙상블(Ensemble) 모델
- 앙상블 모델이란 여러개의 머신러닝 모델을 이용해 최적의 답을 찾아내는 기법을 사용하는 모델입니다.
- 앙상블의 종류
  1. 보팅
  2. 배깅
  3. 부스팅
  4. 스태킹

***

## 부스팅 (Boosting)

- **부스팅 개념:**
  - 부스팅은 여러개의 약한 학습기(weaklearner)를 결합하여 강한 학습기고(strong learner)를 만드는 앙상블 학습 방법 중 하나입니다. 약한 학습기는 일반적으로 성능이 낮은 모델로, 무작위 추측보다 조금 더 나은 성능을 갖는 모델을 말합니다. 부스팅은 이러한 약한 학습기를 순차적으로 학습시켜서, 이전 모델이 만들어진 오차를 보완하도록 하는 방식으로 작동합니다.

- **부스팅 주요 특징:**
  - 순차적인 학습: 부스팅은 이전 모델이 만든 오차에 초점을 맞추어 순차적으로 학습을 진행합니다.
    각 모델은 이전 모델이 잘못 분류한 샘플에 더 집중하여 학습됩니다.
  - 앙상블 학습: 부스팅은 여러 개의 약한 학습기를 결합하여 하나의 강한 학습기를 만듭니다. 이를 통해 전체적인 성능이 향상됩니다.
  - 가중치 부여: 각 약한 학습기에는 가중치가 할당되어 있으며, 모델이 더 잘 수행한 경우 해당 모델에 높은 가중치를 부여합니다. 최종 예측은 각 모델의 가중 평균이 됩니다.
    가중치 부여방식
      1. 첫번째 모델 학습: 첫 번째 약한 학습기가 전체 데이터에 대해 학습됩니다.
      2. 오차계산: 첫번째 모델의 예측 결과와 실제 값 사이의 오차가 계산됩니다. 오차는 예측이 잘못된 샘플에 대해 더 큰 값을 갖습니다.
      3. 가중치 할당: 오차에 따라 가중치가 할당됩니다. 오차가 큰 샘플에 더 큰 가중치가 부여되어, 다음 모델이 이 샘플에 더 집중하도록 유도됩니다.
      4. 두 번째 모델 학습: 두번째 약한 학습기가 가중치가 적용된 데이터에 대해 학습됩니다. 이때, 이전에 잘못 예측한 샘플에 높은 가중치가 부여되어 이를 보다 정확하게 예측하려고 노력합니다.
      5. 이전 모델과 현재 모델의 예측을 결합: 예측 결과에 가중치를 적용하여 최종 예측을 계산합니다. 이때, 각 모델의 가중 평균이 사용됩니다.
      6. 반복: 위 과정을 원하는 만큼 반복합니다. 각 반복에서 새로운 모델이 이전 모델들이 만든 오차를 보정하려고 노력하며, 전체 모델의 성능이 향상됩니다.
 
- **부스팅의 종류:**
  - Adaboost(Adaptive Boosting)
  - Gradient Boosting    (실제값과 예측값 차이 줄여주는 함수 찾는 것으로 보완)
  - XGBoost    (Gradient Boosting에서 과적합 방지 기능 추가)
  - LightGBM
  - Cat Boost ...
  - 등이 있습니다. 각 알고리즘은 부스팅의 기본 아이디어를 확장하고 세부적으로 조정한 변종입니다.
  
- [Boosting 사용 예제](boosting_stacking_example.ipynb)

***

## 스태킹 (Stacking)

- **스태킹 개념:**
  - 여러 다른 기본 모델들을 조합하여 보다 강력한 모델을 만드는 방법입니다. 스태킹은 개별 모델들의 예측 결과를 결합하여 최종 예측을 수행하며, 이를 통해 모델의 성능을 향상시키고 다양한 패턴을 잘 캡처할 수 있습니다.
    
- **스태킹의 주요 특징:**
  - 다양한 모델의 결합: 서로 다른 알고리즘이나 설정을 가진 여러 기본 모델들을 결합합니다.
  - 앙상블 효과: 각 모델이 부족한 부분을 다른 모델이 보완하며, 앙상블의 효과를 얻을 수 있습니다.
  - 다단계 학습: 다단계 학습을 통해 각 모델은 전체적인 문제에 대한 특정 측면을 학습하게 됩니다.

- **스태킹의 학습단계:**
  1. 첫 번째 단계: 여러 다른 기본 모델들을 학습시킵니다. 이 단계에서는 서로 다른 알고리즘이나 설정을 사용한 여러 모델을 선택하는 것이 좋습니다.
  2. 두 번째 단계: 첫 번째 단계에서 학습한 기본 모델들을 새로운 훈련 데이터로 사용하여 새로운 메타 모델을 학습시킵니다.
  3. 스태킹 모델의 예측: 새로운 데이터에 대해 메타 모델을 사용하여 예측을 수행합니다.
 
- **스태킹의 종류:**
  - 기본 스태킹: 데이터의 다양한 패턴을 더 효과적으로 학습
  - 블렌딩: 간단한 구조로 계산 비용 감소
 
- **스태킹의 장점:**
  - 스태킹을 사용하면 다양한 모델의 강점을 결합하여 성능을 향상시킬 수 있습니다. 각 모델이 서로 다른 패턴을 잘 잡아내는 경우, 스태킹은 이러한 다양성을 활용하여 더 강력한 예측 모델을 생성합니다. 스태킹은 주로 대회와 같은 경쟁적인 상황에서 성능을 극대화하기 위해 사용되며, 주의할 점은 충분한 데이터가 필요하다는 것입니다.

- [스태킹 구현 예제](boosting_stacking_example.ipynb)
