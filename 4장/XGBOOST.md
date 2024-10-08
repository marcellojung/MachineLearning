# XGBoost
 "Extreme Gradient Boosting"의 약자로, Gradient Boosting Machine(GBM)을 확장한 매우 효율적이고 강력한 부스팅 알고리즘입니다. XGBoost는 성능과 학습 속도를 크게 향상시키기 위해 여러 가지 최적화 기법을 적용한 모델로, 특히 대규모 데이터셋에서 뛰어난 성능을 보입니다.

 python wrapper, 사이킷런 wrapper 두 종류가 있다 

## **XGBoost의 주요 특징**

1. **Regularization (정규화)**
   - L1 및 L2 정규화를 통해 모델 복잡도를 조절하고, 과적합을 방지합니다. 이는 XGBoost의 중요한 장점으로, 다른 부스팅 알고리즘에 비해 과적합에 덜 민감합니다.

2. **Sparsity Awareness (희소성 인식)**
   - 희소한 데이터(결측치가 많은 데이터)를 효율적으로 처리할 수 있도록 설계되었습니다. XGBoost는 희소한 행렬을 내부적으로 효율적으로 처리합니다.

3. **Weighted Quantile Sketch**
   - XGBoost는 매우 큰 데이터셋에서도 정확한 분할 지점을 찾기 위해 가중치가 부여된 분위수 스케치를 사용합니다.

4. **Parallel Computing (병렬 처리)**
   - XGBoost는 다중 스레드를 활용하여 트리 생성을 병렬로 수행합니다. 이를 통해 학습 속도가 크게 향상됩니다.

5. **Handling Missing Data**
   - 결측 데이터를 자동으로 처리하는 기능을 내장하고 있어, 결측치가 있는 데이터셋에서도 안정적으로 동작합니다.

6. **Early Stopping**
   - 성능 개선이 멈추면 학습을 중단하는 기능을 지원하여 불필요한 학습 시간을 절약하고, 과적합을 방지할 수 있습니다.

## **XGBoost의 주요 하이퍼파라미터**

1. **`n_estimators`**
   - **설명**: 부스팅 트리의 개수를 지정합니다. 많은 트리를 사용할수록 성능이 향상될 수 있지만, 과적합의 위험도 증가합니다.
   - **기본값**: 100.
   - **튜닝 팁**: `learning_rate`와 함께 조정하며, 작은 학습률을 사용할 경우 더 많은 트리를 사용합니다.

2. **`learning_rate` (또는 `eta`)**
   - **설명**: 각 트리의 기여도를 조정하는 매개변수입니다. 학습률이 낮을수록 학습 속도는 느려지지만, 일반적으로 더 좋은 성능을 얻을 수 있습니다.
   - **기본값**: 0.3.
   - **튜닝 팁**: 0.01에서 0.2 사이의 값을 자주 사용합니다. 작은 값을 사용할수록 `n_estimators`를 늘려야 합니다.

3. **`max_depth`**
   - **설명**: 각 트리의 최대 깊이를 설정합니다. 트리 깊이가 깊을수록 모델이 더 복잡해지며, 과적합할 위험이 있습니다.
   - **기본값**: 6.
   - **튜닝 팁**: 3에서 10 사이의 값을 사용하며, 데이터셋의 크기와 복잡성에 따라 조정합니다.

4. **`min_child_weight`**
   - **설명**: 자식 노드를 분할하기 위해 필요한 최소 샘플 가중치의 합을 지정합니다. 값이 클수록 과적합을 방지할 수 있습니다.
   - **기본값**: 1.
   - **튜닝 팁**: 값이 클수록 모델이 덜 복잡해지고, 과적합이 줄어듭니다. 데이터가 불균형한 경우 유용합니다.

5. **`subsample`**
   - **설명**: 각 트리를 학습할 때 사용할 데이터 샘플의 비율을 지정합니다. 값이 작을수록 모델의 다양성이 증가하여 과적합을 줄일 수 있습니다.
   - **기본값**: 1.0 (전체 데이터 사용).
   - **튜닝 팁**: 일반적으로 0.5에서 0.9 사이의 값을 사용합니다. 너무 작은 값은 성능을 저하시킬 수 있습니다.

6. **`colsample_bytree`**
   - **설명**: 각 트리를 학습할 때 사용할 특징(feature)의 비율을 지정합니다. 부분 샘플링을 통해 모델의 다양성을 증가시킵니다.
   - **기본값**: 1.0 (모든 특징 사용).
   - **튜닝 팁**: 보통 0.3에서 0.8 사이의 값을 사용합니다.

7. **`gamma` (또는 `min_split_loss`)**
   - **설명**: 노드를 분할하기 위해 필요한 최소 손실 감소를 지정합니다. 값이 클수록 트리가 덜 분할되어 모델이 덜 복잡해집니다.
   - **기본값**: 0.
   - **튜닝 팁**: 모델이 과적합하는 경우 값을 높여 트리 분할을 줄일 수 있습니다.

8. **`lambda` (또는 `reg_lambda`)**
   - **설명**: L2 정규화 항의 가중치를 설정합니다. 과적합을 방지하기 위해 사용됩니다.
   - **기본값**: 1.
   - **튜닝 팁**: 모델이 과적합할 경우 이 값을 증가시켜 규제를 강화할 수 있습니다.

9. **`alpha` (또는 `reg_alpha`)**
   - **설명**: L1 정규화 항의 가중치를 설정합니다. L1 정규화는 일부 가중치를 0으로 만들어, 특징 선택의 역할을 할 수 있습니다.
   - **기본값**: 0.
   - **튜닝 팁**: 모델에 불필요한 특징이 많거나, 과적합이 의심될 경우 값을 높입니다.

10. **`scale_pos_weight`**
    - **설명**: 클래스 불균형 문제를 해결하기 위해 양성 클래스의 가중치를 조정하는 파라미터입니다.
    - **튜닝 팁**: 데이터셋의 클래스 불균형이 심할 경우 (e.g., 1:10 이상), 이를 조정하여 모델이 균형 잡힌 예측을 할 수 있도록 합니다.

11. **`early_stopping_rounds`**
    - **설명**: 검증 데이터의 성능이 향상되지 않으면 학습을 조기에 중단할 수 있습니다.
    - **튜닝 팁**: 일반적으로 10에서 100 사이의 값을 사용합니다. 이는 모델의 과적합을 방지하고, 학습 시간을 단축할 수 있습니다.

## **XGBoost 하이퍼파라미터 튜닝 전략**

- **Grid Search 및 Random Search**: 하이퍼파라미터 공간을 탐색하여 최적의 값을 찾는 방법입니다. 특히 `learning_rate`, `max_depth`, `min_child_weight`, `gamma` 등의 파라미터를 함께 조정하는 것이 중요합니다.

- **Bayesian Optimization**: 하이퍼파라미터의 조합이 많을 경우, Bayesian Optimization과 같은 기법을 통해 효율적으로 최적의 하이퍼파라미터를 찾을 수 있습니다.

- **Cross-Validation**: 교차 검증을 통해 각 하이퍼파라미터 조합의 성능을 평가하여 과적합을 방지합니다.

## **XGBoost의 사용 사례**

- XGBoost는 Kaggle 및 기타 데이터 과학 대회에서 자주 사용되는 모델로, 다양한 회귀 및 분류 문제에서 우수한 성능을 보입니다.
- 특히, 대규모 데이터셋, 높은 차원의 데이터, 그리고 결측치가 많은 데이터에서 뛰어난 성능을 발휘합니다.
- XGBoost는 강력하고 유연한 모델이지만, 하이퍼파라미터 튜닝이 필수적입니다. 적절한 튜닝을 통해 XGBoost의 성능을 극대화할 수 있으며, 특히 대규모 데이터셋에서 탁월한 성능을 발휘합니다. 


XGBoost를 Python에서 사용할 때, 두 가지 주요 인터페이스가 있습니다: 

1. **XGBoost의 자체 Python API (`xgboost.XGBClassifier`, `xgboost.XGBRegressor` 등)**
2. **사이킷런 래퍼 (`xgboost.sklearn.XGBClassifier`, `xgboost.sklearn.XGBRegressor`)**

이 두 가지 모두 비슷한 기능을 제공하지만, 사용하는 방식이나 환경에 따라 선택이 달라질 수 있습니다.

### 1. **XGBoost 자체 Python API**
이 방법은 XGBoost의 공식 API를 사용하여 모델을 직접 구현하는 방법입니다. 

```python
import xgboost as xgb

# XGBClassifier 또는 XGBRegressor 사용
model = xgb.XGBClassifier()
model.fit(X_train, y_train)
```

### 2. **사이킷런 래퍼 (`xgboost.sklearn.XGBClassifier`)**
이 방법은 XGBoost 모델을 사이킷런의 `Pipeline`, `GridSearchCV`, `cross_val_score` 등과 같은 도구들과 쉽게 연동할 수 있도록 래핑한 것입니다.

```python
from xgboost import XGBClassifier

model = XGBClassifier()
model.fit(X_train, y_train)
```

### **어느 방식이 더 많이 사용되나요?**

일반적으로 **사이킷런 래퍼** (`xgboost.sklearn.XGBClassifier`, `xgboost.sklearn.XGBRegressor`)가 더 많이 사용됩니다. 그 이유는 다음과 같습니다:

1. **사이킷런과의 통합 용이성**: 
   - `GridSearchCV`, `Pipeline`, `cross_val_score` 등 사이킷런의 다양한 유틸리티와 자연스럽게 통합됩니다.
   - 사이킷런 기반의 작업 흐름을 유지하면서 XGBoost의 성능을 활용할 수 있습니다.

2. **사이킷런 사용자의 친숙함**: 
   - 사이킷런 사용자라면 이미 익숙한 API 패턴을 그대로 사용할 수 있기 때문에 학습 곡선이 짧습니다.

3. **일관된 인터페이스**: 
   - 사이킷런에서 제공하는 다른 모델들과 함께 XGBoost를 동일한 방식으로 사용할 수 있습니다. 이는 코드의 일관성을 유지하는 데 도움이 됩니다.

### 결론

대부분의 경우, 특히 사이킷런과 함께 작업하는 경우에는 **사이킷런 래퍼** (`xgboost.sklearn.XGBClassifier`, `xgboost.sklearn.XGBRegressor`)가 더 널리 사용됩니다. XGBoost의 고급 기능을 활용하고, 사이킷런의 편리한 기능들을 함께 사용하려는 경우 이 방식을 사용하는 것이 좋습니다. 

하지만, 사이킷런과의 통합이 필요 없거나, XGBoost의 특정 기능을 직접적으로 제어하고 싶을 때는 XGBoost의 자체 Python API를 사용할 수도 있습니다.