# Bank Marketing Prediction

은행 마케팅 캠페인 데이터를 활용해 고객의 정기예금 가입 여부를 예측하는 이진분류 프로젝트입니다.  
여러 머신러닝 모델을 비교하고, 최종적으로 Stacking Classifier를 활용해 예측 성능을 개선했습니다.

---

## 1. Project Overview
- **진행 배경:** 학부 수업 기반 프로젝트
- **진행 형태:** 개인 프로젝트
- **목표:** 고객의 정기예금 가입 여부를 예측하고, 예측 결과를 마케팅 타겟팅에 활용할 수 있도록 하는 것
- **평가 지표:** Accuracy, F1 Score, AUC

---

## 2. Data
- **train.csv:** 32,950 rows × 21 columns
- **test.csv:** 8,238 rows × 20 columns
- **Target:** `y` (정기예금 가입 여부)

### 주요 특징
- 숫자형 + 범주형 혼합 데이터
- 범주형 결측이 `unknown`으로 포함됨
- 타깃 클래스가 불균형함 (`0` 비율이 높음)
- `pdays=999`는 “이전에 연락한 적 없음”을 의미

---

## 3. Preprocessing
- `y`를 `yes=1`, `no=0`으로 인코딩
- `id` 컬럼 제거
- 범주형 변수 one-hot encoding
- 숫자형 변수 표준화 (`StandardScaler`)
- `pdays`를 연락 이력 여부 기준으로 재구성
- `train_test_split(test_size=0.2, random_state=42)` 적용

---

## 4. Models
다음 모델들을 비교했습니다.

- Logistic Regression
- Bagging
- Random Forest
- Gradient Boosting
- XGBoost
- LightGBM
- Stacking Classifier

모든 모델은 5-Fold Cross Validation과 GridSearchCV를 사용해 비교했습니다.

---

## 5. Result
- 여러 모델 중 **Stacking Classifier**를 최종 모델로 선정
- 불균형 데이터 환경에서 Accuracy뿐 아니라 F1, AUC를 함께 고려
- threshold tuning을 통해 실무 활용 가능성을 검토
- LightGBM 기반 변수 중요도 분석 수행

### 주요 중요 변수
- euribor3m
- age
- campaign
- cons.price.idx
- cons.conf.idx
- contact
- nr.employed

---

## 6. Business Insight
이 프로젝트는 단순히 고객 가입 여부를 예측하는 데 그치지 않고,  
예측 확률(`y_prob`)을 기반으로 고객을 우선순위화하여 실제 마케팅 타겟팅 전략에 활용할 수 있도록 설계했습니다.

예시:
- 가입 확률이 높은 고객군 우선 접촉
- 이전 접촉 이력이 있는 고객 대상 리마케팅
- 연락 방식과 시점을 조정한 캠페인 전략 수립

---

## 7. Tech Stack
- Python
- pandas
- scikit-learn
- XGBoost
- LightGBM

---

## 8. Files
- `bank_marketing_prediction.ipynb` : 전체 분석 및 모델링 코드

---

## 9. Notes
- 데이터 파일은 업로드하지 않았습니다.
- 본 저장소는 포트폴리오용으로 정리한 프로젝트입니다.
