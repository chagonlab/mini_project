# 머신러닝을 활용한 로이터 뉴스 카테고리 분류

## 1. 프로젝트 개요

본 프로젝트는 뉴스 텍스트 데이터(46개 카테고리)를 대상으로  
TF-IDF 기반 피처 표현에서 **Vocabulary Size 변화에 따른 분류 모델 성능 비교**를 목적으로 진행되었습니다.

- **문제 유형**: Multi-class Text Classification (46 classes)
- **입력 표현**: TF-IDF
- **평가 지표**
  - Accuracy
  - **Macro F1-score** (클래스 불균형 고려)

Vocabulary Size를  
**20,000 / 10,000 / 5,000 / All words** 로 나누어 실험을 분담하여 진행하였으며,  
각 사이즈별로 동일한 모델 세트를 사용해 성능을 비교했습니다.

---

## 2. 실험 설정

### 공통 설정
- **TF-IDF Vectorizer**
- **분류 모델**
  - Logistic Regression
  - SVM
  - Linear SVC
  - Random Forest
  - Complement Naive Bayes
  - XGBoost
  - LightGBM
  - Dense (MLP)
  - Voting (Soft Voting)
- **평가 방식**
  - Test set 기준 Accuracy / Macro F1-score

---

## 3. 담당한 실험 (Vocabulary Size = 20,000)

본 저장소에 업로드된 Jupyter Notebook에서는  
**Vocabulary Size = 20,000** 설정에 대한 모든 모델 실험을 직접 수행했습니다.

### 3.1 실험 방식

- TF-IDF vocab_size를 **20,000으로 고정**
- 모든 모델에 대해 동일한 train / test split 사용
- Multi-class(46 classes) 환경을 고려하여 **Macro F1-score를 주요 지표로 사용**
- Voting의 경우
  - Soft Voting 사용
  - 확률 기반 예측이 가능한 모델만 포함
- Dense 모델
  - TF-IDF 벡터를 입력으로 사용하는 **MLP(Dense) 구조**
  - Embedding 미사용 (전통 ML 모델과의 공정 비교 목적)

---

### 3.2 Vocabulary Size = 20,000 결과

| Vocabulary Size | Model | Accuracy | F1-Score | Best F1 |
| --- | --- | --- | --- | --- |
| **20,000** | LogisticRegression | 0.7956 | 0.4721 |  |
|  | SVM | 0.8219 | 0.6355 |  |
|  | **Linear SVC** | **0.8299** | **0.6808** | ⭐ |
|  | RandomForest | 0.7600 | 0.4445 |  |
|  | ComplementNB | 0.7707 | 0.4784 |  |
|  | XGBoost | 0.8090 | 0.6574 |  |
|  | LightGBM | 0.3998 | 0.0244 |  |
|  | Dense | 0.7992 | 0.5824 |  |
|  | Voting | 0.8286 | 0.6557 |  |

---

### 3.3 분석 및 해석 (20,000 기준)

- **Linear SVC**가 Accuracy와 Macro F1-score 모두에서 최고 성능을 기록
- 고차원 희소 벡터(TF-IDF) 환경에서는  
  **선형 마진 기반 모델(Linear SVC, SVM)** 이 가장 안정적인 성능을 보임
- Tree / Boosting 계열 모델
  - XGBoost는 비교적 준수한 성능
  - LightGBM은 sparse + multi-class 환경에서 성능 저하가 뚜렷
- Dense(MLP)
  - 비선형 모델임에도 TF-IDF 입력에서는 선형 모델 대비 뚜렷한 우위는 없음
- Voting
  - 단일 최고 모델을 넘지는 못했으나
  - 비교적 안정적인 성능을 통해 앙상블 효과 확인

---

## 4. 전체 Vocabulary Size별 모델 성능 비교 결과

아래 표는 Vocabulary Size별로 다양한 모델을 적용했을 때의  
Accuracy와 Macro F1-score를 정리한 결과입니다.  
각 Vocabulary Size 기준으로 **가장 높은 Macro F1-score**를 기록한 모델을 ⭐로 표시했습니다.

| **Vocabulary Size** | **Model** | **Accuracy** | **F1-Score** | Best F1 |
| --- | --- | --- | --- | --- |
| **20,000** | LogisticRegression | 0.7956 | 0.4721 |  |
|  | SVM | 0.8219 | 0.6355 |  |
|  | **Linear SVC** | **0.8299** | **0.6808** | ⭐ |
|  | RandomForest | 0.7600 | 0.4445 |  |
|  | ComplementNB | 0.7707 | 0.4784 |  |
|  | XGBoost | 0.8090 | 0.6574 |  |
|  | LightGBM | 0.3998 | 0.0244 |  |
|  | Dense | 0.7992 | 0.5824 |  |
|  | Voting | 0.8286 | 0.6557 |  |
| **10,000** | LogisticRegression | 0.7876 | 0.7613 |  |
|  | SVM | 0.8219 | 0.8121 |  |
|  | **Linear SVC** | **0.8299** | **0.8237** | ⭐ |
|  | RandomForest | 0.7542 | 0.7295 |  |
|  | ComplementNB | 0.7707 | 0.7457 |  |
|  | XGBoost | 0.7961 | 0.7895 |  |
|  | LightGBM | 0.0583 | 0.0350 |  |
|  | Dense | 0.7854 | 0.7712 |  |
|  | Voting | 0.7960 | 0.7894 |  |
| **5,000** | LogisticRegression | 0.8250 | 0.8274 |  |
|  | SVM | 0.8050 | 0.7965 |  |
|  | **Linear SVC** | **0.8388** | **0.8322** | ⭐ |
|  | RandomForest | 0.7863 | 0.7787 |  |
|  | ComplementNB | 0.7707 | 0.7459 |  |
|  | XGBoost | 0.8241 | 0.8171 |  |
|  | LightGBM | 0.8072 | 0.7979 |  |
|  | Dense | 0.8045 | 0.7949 |  |
|  | Voting |  |  |  |
| **NaN (All words)** | LogisticRegression | 0.8130 | 0.8064 |  |
|  | SVM | 0.8227 | 0.8122 |  |
|  | **Linear SVC** | **0.8294** | **0.8236** | ⭐ |
|  | RandomForest | 0.7448 | 0.7180 |  |
|  | ComplementNB | 0.7649 | 0.7346 |  |
|  | XGBoost | 0.8130 | 0.8061 |  |
|  | LightGBM | 0.1923 | 0.1781 |  |
|  | Dense | 0.8103 | 0.8016 |  |
|  | Voting | 0.8294 | 0.8234 |  |

---

## 5. 결론

- TF-IDF 기반 텍스트 분류 문제에서는  
  **모델 복잡도보다 입력 표현 방식과 차원 수 조절이 더 중요**
- 46개 클래스의 다중 분류 환경에서  
  **Linear SVC는 가장 일관되고 강력한 베이스라인 모델**
- Dense 및 Boosting 모델의 강점은  
  Embedding 기반 입력으로 확장할 때 더 명확해질 것으로 예상됨

---

## 6. 향후 실험 방향

- Embedding 기반 입력(Dense / CNN / RNN)
- Vocabulary Size와 Embedding Dimension 간 trade-off 분석
- Class imbalance를 고려한 loss / sampling 전략 실험
