# BigDataPrograming_A_Team H
## 1형 소아당뇨 환자 혈당 예측 및 음식 추천  

---

## 📊 Data Sources & Descriptions

### 1. [CGM_YoungChildren.csv](https://public.jaeb.org/datasets/diabetes)
**출처**: JAEB Center  
**데이터명**: *A Study to Assess Continuous Glucose Sensor Profiles in Healthy Non-Diabetic Participants Aged <7 Years*
**요약**: 만 1~ 6세 제1형 당뇨 아동의 CGM을 사용하여 수집한 혈당 기록

| 컬럼명 | 설명 | 예시 |
|--------|------|------|
| ID | 아동 고유 식별번호 | 1 |
| Timestamp | 혈당 측정 시각 (5분 간격) | 2000-01-01 12:25 |
| GL | 혈당 수치 (mg/dL) | 144 |
| Weight(kg) | 몸무게 | 22.2 |
| Height(cm) | 키 | 122.5 |
| Age | 나이 (만 나이) | 6 |
| Gender | 성별 (F/M) | F |
| Time of Day | 시간대 구분 (0:새벽, 1:오전, 2:오후, 3:밤) | 1 |

- **특징**: 연속 혈당 센서 데이터 (5분 간격), 신체정보 포함

---

### 2. [actual_pediatric_patient_data.csv](https://github.com/ictinnovaties-zorg/dataset-diabetes-adolescents-time-series-with-heart-rate)
**출처**: ICT Innovaties Zorg  
**요약**: 10~17세 제1형 당뇨 아동의 CGM을 사용하여 수집한 혈당 기록

| 컬럼명 | 설명 | 예시 |
|--------|------|------|
| ID | 아동 환자 고유번호 | 903 |
| Timestamp | 혈당 측정 시각 (15분 간격) | 2019-10-17 00:11 |
| GL | 혈당 수치 | 155 |
| Weight(kg) | 체중 | 42.7 |
| Height(cm) | 키 | 154.5 |
| Age | 나이 | 10 |
| Gender | 성별 (F/M) | F |
| Time of Day | 시간대 구분 (0~3) | 3 |

---

### 3. [Food_Recipe_DB.csv](https://www.foodsafetykorea.go.kr/api/openApiInfo.do?menu_grp=MENU_GRP31&menu_no=661)
**출처**: 식품안전나라 - 공공 레시피 API  
**데이터명**: COOKRCP01 (공공 레시피 영양정보 포함)

| 컬럼명 | 설명 |
|--------|------|
| RCP_NM | 음식명 |
| INFO_ENG | 열량 (kcal) |
| INFO_CAR / PRO / FAT / NA | 탄수화물 / 단백질 / 지방 / 나트륨 |
| RCP_PARTS_DTLS | 주재료 및 분량 |
| MANUAL01 ~ MANUAL20 | 단계별 조리 방법 |
| RCP_NA_TIP | 나트륨 저감 팁 |

- **특징**: 레시피별 영양 정보, 조리과정, 건강 정보 포함 (나트륨 저감 등)

---

## 🧠 Model Summary

- **목표**: 
  - 식사 이벤트 발생 전후 혈당 변화(ΔGL@1h)를 예측
  - 혈당 반응이 낮은 레시피 추천

- **사용 모델**:
  - XGBoost (`xgb_model.joblib, lgb_model.joblib` 앙상블)
  - LightGBM (실험용)
  
- **입력 피처**:
  - 이전 혈당 수치
  - 신체정보: 키, 몸무게, 성별, 나이
  - 시간대 구분
  
- **예측 대상**: ΔGL 1h (식사 후 1시간 혈당 변화량)

---

## 🛠️ Main Files Overview

| 파일명 | 설명 |
|--------|------|
| `CGM__xgboost_lightgbm_model.ipynb` | 식사 이벤트 탐지 → AUC 계산 → ΔGL@1h 회귀 예측 모델 학습 |
| `Demonstration_Code.ipynb` | 사용자 입력 기반 혈당 예측 및 음식 추천 시연 |
| `xgb_model.joblib` | 학습 완료된 XGBoost 회귀 모델 (ΔGL 예측용) |

---

## 📌 Usage

1. `Demonstration_Code.ipynb` 실행
2. 사용자 혈당 정보, 신체 정보 입력
3. 훈련된 모델(`xgb_model.joblib`)로 ΔGL 예측
4. Food DB에서 탄수화물 및 혈당 반응 낮은 레시피 추천

---

## 📅 Roadmap

- [x] 식사 이벤트 탐지 및 AUC 기반 모델 구축
- [x] ΔGL@1h 회귀 모델 학습
- [x] 추천용 음식 DB 정제 및 매핑
- [ ] 실제 사용자 인터페이스 구현 (예: 웹앱)
- [ ] 개인별 식단 맞춤화 고도화 (과거 반응 학습)

---

## 📜 License

본 프로젝트는 학술적 목적 및 연구용으로 활용되며, 상업적 이용은 제한됩니다. 데이터 출처에 따라 사용 전 저작권 정책을 반드시 확인하시기 바랍니다.

---

## 🙋 Contact

문의사항: [프로젝트 담당자 이름 또는 이메일 작성]

