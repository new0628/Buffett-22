# Dart API로 부터 불러오는 셀은 시간이 오래걸립니다(30분)

# 📘 워런 버핏 가치투자 기준 기반 국내 반도체 기업 클러스터 분석

이 프로젝트는 국내 중소·중견 반도체 기업을 대상으로 워런 버핏이 강조한 **수익성**, **안정성**, **성장성** 기준에 따라 장기적 투자 매력도를 평가한 분석입니다.  
정량 지표(재무제표)와 함께 **브랜드 평판 지수**, **경영진 평가** 같은 정성 지표를 포함해 클러스터링 기반 투자 유형 분류 모델을 구축하였습니다.

## 🎯 프로젝트 목적

- 재무지표 중심 분석이 간과하는 **질적 경쟁력**까지 반영
- **숨어 있는 가치주**, **지속가능한 성장주** 선별
- 반도체 산업 내 **기업 비교·군집화**를 통해 실질적인 인사이트 제공

## 📂 프로젝트 파일 구성

| 파일명                       | 설명                                                             |
| ---------------------------- | ---------------------------------------------------------------- |
| `BigData_Final.ipynb`        | 전체 분석 노트북 (데이터 수집, 전처리, 클러스터링, 해석 등 포함) |
| `financial_indicators.csv`   | 2022Q1~2025Q1 기준 재무 및 정성 지표 데이터셋                    |
| `management_evaluation.docx` | 2022~2025 경영진 평가 뉴스 스크랩 데이터셋                       |
| `README.md`                  | 프로젝트 설명 문서                                               |

## 📊 데이터 출처 및 지표 구성

### 재무 데이터

- **출처**: 금융감독원 DART 전자공시 Open API
- **기간**: 2021 ~ 2025년
- **수집 항목**: 매출액, 순이익, 자산, 부채, 자본, 유동자산, 유동부채, EPS 등

### 사용된 지표

- **수익성**: ROE, ROA, 영업이익률, 순이익률, EPS
- **안정성**: 부채비율, 유동비율, 자기자본비율
- **성장성**: 매출 성장률, 순이익 성장률
- **정성적 지표**: 브랜드 평판 지수, 경영진 평가 점수

## 🧠 분석 방법론 요약

1. **데이터 수집**

   - DART API 활용
   - EPS 계산을 위한 주식수 보완 처리 포함

2. **버핏식 스코어링**

   - 수익성, 안정성, 성장성 각각에 대한 점수 계산
   - 로그 변환 및 표준화 적용

3. **KMeans 클러스터링 + PCA 시각화**

   - 최적 클러스터 수 결정 (k=3)
   - 클러스터별 기업 유형 해석 (가치주, 성장주, 저성장주)

4. **정성 지표 통합**
   - 브랜드 지수, 경영진 평가 포함 → 해석력 향상

## 📌 클러스터 해석 요약

| Cluster | 투자 성향     | 특징 요약                         |
| ------- | ------------- | --------------------------------- |
| **0**   | 안정적 가치주 | 고ROE, 저부채, 브랜드 신뢰도 우수 |
| **1**   | 저성장·저수익 | 수익성·성장성 낮음, 투자 비추천   |
| **2**   | 고성장·고수익 | 리스크 있지만 성장 기대 큰 성장주 |

## 📈 시각화 및 결과 해석

- **PCA 시각화**: 각 클러스터가 시각적으로 분리됨
- **Silhouette Score**: 평균 ≈ 0.18
- **클러스터별 대표 기업 예시**:
  - Cluster 0: 삼성전자, SK하이닉스, DB하이텍 등
  - Cluster 1: 디아이, 넥스틴, 오킨스전자 등
  - Cluster 2: 신성이엔지, 젬백스, 제우스 등

## ✅ 코드 실행 방법

### 환경 요구사항

- Python 3.9 이상 (Anaconda 권장)
- Jupyter Notebook / Jupyter Lab

### 필수 패키지 설치

```python
pip install pandas numpy scikit-learn matplotlib requests ipywidgets

pip install git+https://github.com/josw123/dart-fss.git
```

### DART API 키 등록

```python
import dart_fss as dart
dart.set_api_key('본인_API_KEY')
```

## 🧭 인사이트 및 한계

### 핵심 인사이트

- 버핏식 가치 기준은 **국내 반도체 기업 분석에도 유효**
- 정성적 지표는 재무지표의 **현실적 보완 수단**
- 투자자 성향에 따라 **전략적 포트폴리오 구성 가능**

### 한계점

- Silhouette 점수가 낮아 **모델 구분력** 개선 필요
- 정성 지표는 **정규화 및 최신성 유지**에 어려움 존재
- **업종 특화 분석**이 아직 미흡 (ex. 장비/소재/팹리스)

## 🔮 향후 개선 방향

1. 정성 지표 정규화 및 가중치 조정
2. 반도체 **세부 업종별 클러스터링**
3. **시계열 기반 클러스터 이동 분석**
4. 현금흐름, 기술력, ESG 등 지표 추가 고려
5. **실제 투자성과 백테스트** 수행

## 🛠 주요 함수

- `run_investment_model_all_quarters_df_no_nan(기업명)`
- `get_investment_recommendation(기업명)`

## 📎 예시 출력

```text
삼성전자 기업은 Cluster 0 에 속합니다.
투자 판단: 안정적 가치주 – 장기 투자 및 배당 전략에 적합합니다.
```

## 👋 참고

- DART API: https://opendart.fss.or.kr/
- BRI 코리아 브랜드 지수: https://brikorea.com/

이러한 개선 방향을 바탕으로, 본 프로젝트는 정성·정량을 아우르는 실질적인 가치투자 모델로 확장될 수 있을 것입니다. 투자자에게는 종목 선별에, 기업에게는 스스로의 위치를 진단하는 데 도움이 되기를 기대합니다
