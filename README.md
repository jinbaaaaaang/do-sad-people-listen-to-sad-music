# 🎵 do-sad-people-listen-to-sad-music

Turns out sad people don't listen to sad music.

우울감이 심해지면 Classical이나 Lo-fi처럼 잔잔한 음악으로 도피할 것이라는 가설을 출발점으로,
음악 청취 습관과 우울 수준의 관계를 데이터로 검증한 프로젝트입니다.

## 데이터
- **출처**: Kaggle MxMH (Music & Mental Health) Survey
- **링크**: https://www.kaggle.com/datasets/catherinerasgaitis/mxmh-survey-results
- **수집**: 2022년 Catherine Rasgaitis
- **규모**: 원본 736명 → 전처리 후 726명
- **구성**: 음악 청취 습관(16개 장르 빈도, BPM, 청취 시간) + 정신건강 지표(Anxiety, Depression, Insomnia, OCD, 0~10점)

## 분석 내용
| 단계 | 내용 |
|------|------|
| EDA | 기술통계, 상관관계 히트맵, 우울 그룹별 장르 분포 |
| 가설 검정 | 우울 그룹(Low/Mid/High) 간 음악 변수 차이 검정 (ANOVA) |
| 회귀 분석 | 선형 / 다항(degree 1~4) / Natural Spline 비교 |
| 분류 모델 | Logistic, LDA, QDA, Decision Tree, Random Forest, KNN — 5-Fold CV 비교 |
| 변수 선택 | Lasso 정규화, Random Forest Feature Importance |
| 비지도 학습 | PCA, K-Means(K=2,3,4), 계층적 군집분석 |

## 주요 결과
- 우울 수준이 높아질수록 Rock·Metal 청취가 증가 (F=11.790, p<0.001)
- Classical·Lo-fi는 우울 수준과 무관 (p=0.434) → **도피 가설 기각**
- Lasso와 Random Forest 모두 Rock, Metal, 청취 시간을 핵심 변수로 선별
- BPM이 장르보다 우울 고위험군 예측에 더 중요한 변수 (importance 0.114)
- Random Forest가 가장 안정적 (CV 0.653, Test 0.648)

## 사용 라이브러리
```python
# 주요 라이브러리
import statsmodels.api as sm
from ISLP.models import ModelSpec as MS, summarize, poly, ns
from ISLP import confusion_table
from ISLP.cluster import compute_linkage
import sklearn.linear_model as skl
import sklearn.model_selection as skm
```

## 파일 구성
```
├── music_mental_health.ipynb
└── README.md
```
