# OSS 기반 Smart Factory 설비 상태 모니터링 및 AI 고장징후 예측·대응 시스템

## Project Plan

| 항목 | 내용 |
|---|---|
| 문서 ID | `SF-PHM-PP-001` |
| 연결 Issue | `#1 Project Plan 수립` |
| 버전 | `v1.0` |
| 개발 방식 | Agile/Scrum 기반 반복·점진 개발 |
| 개발 기간 | 4주차 착수 ~ 9주차 개선 Increment 완료 |
| 기준 Branch | `develop` |
| 승인 후 배포 Branch | `main` |
| 문서 책임자 | Team Leader / Scrum Master |
| 승인자 | Product Owner 역할의 교수자 또는 팀 지정 검토자 |

---

## 1. 프로젝트 개요

### 1.1 배경

Smart Factory의 설비는 진동, 온도, 전류, 압력 등 다양한 센서 데이터를 지속해서 발생시킨다. 단순 임계치 감시는 이미 발생한 이상을 확인하는 데에는 유용하지만, 고장 이전에 나타나는 복합적인 변화 패턴을 탐지하는 데에는 한계가 있다.

본 프로젝트는 오픈소스 소프트웨어를 조합하여 설비 데이터를 수집·저장·시각화하고, 팀이 직접 개발한 AI 모델을 적용하여 고장징후를 예측하며, 예측 결과에 따라 경보와 대응 권고를 제공하는 실행 가능한 Prototype을 개발한다.

### 1.2 프로젝트 목표

1. 설비 센서 데이터를 실시간 또는 준실시간으로 수집·저장한다.
2. 현재 상태와 시간대별 변화 추이를 대시보드에서 확인한다.
3. 학습용 데이터를 이용해 고장징후 예측 AI 모델을 직접 개발·평가한다.
4. 예측 모델을 시스템에 탑재하여 신규 센서 데이터에 대한 추론을 수행한다.
5. 위험 수준을 `Normal`, `Warning`, `Critical`로 구분하고 대응 권고를 제공한다.
6. OSS 선정 근거, 라이선스, 요구사항, API, 시험 결과를 GitHub에서 추적 가능하게 관리한다.

### 1.3 Product Vision

> 설비 운영자가 전문적인 데이터 분석 지식 없이도 설비 상태와 고장 가능성을 한 화면에서 확인하고, 고장 전에 점검 조치를 시작할 수 있도록 하는 오픈소스 기반 예지보전 Prototype을 제공한다.

### 1.4 주요 사용자

| 사용자 | 주요 요구 |
|---|---|
| 설비 운영자 | 현재 설비 상태, 이상 경보, 즉시 수행할 조치 확인 |
| 정비 담당자 | 고장 가능성, 관련 센서 추이, 점검 우선순위 확인 |
| 생산 관리자 | 설비별 위험 현황과 가동 영향 확인 |
| 시스템 관리자 | 데이터 수집 상태, 서비스 상태, 장애 로그 확인 |
| AI 개발자 | 데이터 버전, 모델 성능, 모델 버전 및 추론 결과 확인 |

---

## 2. 프로젝트 범위

### 2.1 포함 범위

- 실제 센서 또는 시뮬레이터/공개 데이터셋을 이용한 설비 데이터 입력
- MQTT, REST API 또는 CSV 업로드 방식의 데이터 수집
- 결측치·이상치 처리, 특징 추출 및 학습/검증 데이터 구성
- 시계열 센서 데이터 저장 및 조회
- 설비 상태·센서 추이·경보 이력 대시보드
- 기준 모델과 개선 모델을 포함한 AI 고장징후 예측 모델 개발
- 모델 학습, 평가, 저장, 버전 식별 및 서비스 탑재
- 예측 API 또는 내부 추론 모듈 구현
- `Normal`, `Warning`, `Critical` 위험 등급 판정
- 경보 생성, 경보 이력 저장 및 점검/대응 권고 표시
- 기능시험, API 시험, 성능시험 및 AI 성능 검증
- OSS 라이선스와 출처 기록, 설치·실행·시연 문서 작성

### 2.2 제외 범위

- 실제 생산 설비의 안전 관련 자동 정지 또는 직접 제어
- 상용 수준의 24시간 무중단 운영과 대규모 다공장 배포
- 유료 클라우드 서비스에 종속된 필수 기능
- 안전인증·보안인증·법정인증의 획득
- 대규모 신규 센서 하드웨어 설계 및 제작

### 2.3 핵심 제약조건

- 핵심 실행 기능은 OSS로 구현하고 사용 OSS의 이름·버전·라이선스·URL을 기록한다.
- AI 모델은 외부 예측 결과를 단순 호출하는 방식이 아니라, 팀이 데이터를 전처리하고 학습·평가한 모델이어야 한다.
- 비밀키, 비밀번호, 실제 개인정보는 Repository에 Commit하지 않는다.
- 모든 구현 변경은 Issue, 작업 Branch, Commit, Pull Request, Review를 통해 추적한다.
- 팀원은 자신의 작업 Branch에서 수정하고, `main`에는 직접 Commit하지 않는다.

---

## 3. 성공 기준 및 정량 목표

아래 값은 교육용 Prototype의 기준선이다. 데이터 특성 때문에 AI 목표 달성이 어려운 경우, 임의로 기준을 낮추지 않고 원인·실험 결과·개선안을 시험보고서에 기록한다.

### 3.1 기능 성공 기준

| ID | 성공 기준 | 검증 방법 |
|---|---|---|
| SC-F01 | 최소 1개 설비와 5개 센서 항목의 데이터를 수집한다. | 수집 로그와 DB 조회 |
| SC-F02 | 센서 현재값과 최근 1시간 추이를 대시보드에 표시한다. | 화면 시연 및 기능시험 |
| SC-F03 | 팀이 학습한 AI 모델이 신규 입력에 대해 고장징후 확률 또는 이상 점수를 출력한다. | 모델·API 시험 |
| SC-F04 | 위험 등급별 경보와 대응 권고를 생성하고 이력을 조회한다. | 시나리오 시험 |
| SC-F05 | 정상→이상징후→경보→대응확인 End-to-End 시나리오를 시연한다. | Sprint Review 시연 |

### 3.2 비기능 및 AI 성능 기준

| ID | 항목 | 정량 기준 | 측정 조건 |
|---|---|---|---|
| SC-NF01 | 데이터 수집 처리량 | 분당 1,000건 이상 | 개발 PC, 10분 연속 입력 |
| SC-NF02 | 화면 반영 지연 | 데이터 수신 후 5초 이내, 성공률 95% 이상 | 100건 표본 |
| SC-NF03 | 조회 응답시간 | 최근 1시간 데이터 조회 `p95 ≤ 2초` | 30회 반복 |
| SC-NF04 | AI 추론 응답시간 | 단일 요청 `p95 ≤ 1초` | 모델 로딩 완료 후 100회 |
| SC-NF05 | AI 재현율 | 고장/이상 클래스 Recall `≥ 0.85` | 분리된 Test Set |
| SC-NF06 | AI 정밀도 | 고장/이상 클래스 Precision `≥ 0.80` | 분리된 Test Set |
| SC-NF07 | AI 종합성능 | F1-score `≥ 0.82` | 분리된 Test Set |
| SC-NF08 | 오경보율 | False Positive Rate `≤ 10%` | 분리된 Test Set |
| SC-NF09 | 자동시험 | 핵심 모듈 Test 통과율 100%, 코드 커버리지 70% 이상 | CI 결과 |
| SC-NF10 | 복구성 | 서비스 재시작 후 5분 이내 정상 수집·조회 | 장애복구 시험 |
| SC-NF11 | 보안 | Repository 내 평문 비밀정보 0건 | Secret Scan 및 Review |
| SC-NF12 | OSS 준수 | 사용 OSS의 출처·버전·라이선스 식별률 100% | OSS 목록 검토 |

---

## 4. 개발 전략

### 4.1 개발 원칙

- 작은 기능 단위로 설계·구현·시험하여 매 Sprint마다 실행 가능한 Increment를 만든다.
- API Design First 원칙에 따라 주요 API는 구현 전에 요청·응답·오류 형식을 정의한다.
- AI 개발은 `문제정의 → 데이터 이해 → 전처리 → 기준 모델 → 개선 모델 → 평가 → 탑재 → 모니터링` 순으로 수행한다.
- 복잡한 모델보다 재현 가능하고 설명 가능한 기준 모델을 먼저 완성한다.
- 오픈소스는 기능 적합성뿐 아니라 라이선스, 유지보수성, 문서성, 통합 난이도를 함께 평가한다.

### 4.2 잠정 기술 구성

아래 구성은 계획 기준이며, 최종 채택은 OSS 평가 Issue의 결과로 확정한다.

| 영역 | 우선 검토 OSS | 용도 |
|---|---|---|
| 메시지 수집 | Eclipse Mosquitto | MQTT 센서 메시지 수신 |
| 데이터 흐름 | Node-RED 또는 Python | 데이터 변환·전달 |
| Backend/API | FastAPI | REST API와 AI 추론 서비스 |
| 데이터 저장 | InfluxDB 또는 PostgreSQL | 센서 시계열·경보 이력 저장 |
| Dashboard | Grafana 또는 Web UI | 상태·추이·경보 시각화 |
| AI 개발 | Python, pandas, scikit-learn, XGBoost | 전처리·학습·평가·추론 |
| 시험 | pytest, Postman/Newman | 단위·API 자동시험 |
| 협업/CI | GitHub Issues, Projects, Actions | Agile 관리·형상관리·자동시험 |
| 실행환경 | Docker Compose | 서비스 통합 실행 |

### 4.3 AI 개발 방안

1. 고장 여부가 Label로 제공되는 데이터는 분류 문제로 정의한다.
2. Label이 부족한 경우 이상탐지 모델을 사용하되, 평가용 정상/이상 구간을 별도로 정의한다.
3. Dummy 또는 단순 임계치 방식을 Baseline으로 만들고, Random Forest/XGBoost/Isolation Forest 중 데이터에 맞는 모델을 비교한다.
4. 데이터 누수를 방지하기 위해 Train/Validation/Test Set을 설비 또는 시간 기준으로 분리한다.
5. Accuracy만 사용하지 않고 Precision, Recall, F1-score, Confusion Matrix와 오경보율을 함께 평가한다.
6. 채택 모델, 데이터 버전, 특징 목록, 임계값, 평가 결과를 모델 카드에 기록한다.
7. 학습된 모델 파일은 버전으로 식별하고 추론 서비스에서 동일한 전처리 절차를 사용한다.

---

## 5. Agile 수행 일정

### 5.1 전체 일정

| 기간 | 단계 | 주요 활동 | 완료 산출물/Exit Criteria |
|---|---|---|---|
| 4주차 | Project Initiation | Vision, 범위, 역할, 일정, GitHub 운영기준 수립 | Project Plan 승인, Issue #1 완료 |
| 5주차 | Sprint Planning / Design | 요구사항, User Story, DoR, OSS 평가, 아키텍처, 데이터·API 설계 | Sprint Backlog와 설계 기준선 |
| 6주차 | Sprint 1-A | 데이터 수집·저장·조회, AI 데이터 전처리와 Baseline 개발 | 수집 Pipeline과 Baseline 실행 |
| 7주차 | Sprint 1-B | Dashboard, AI 개선·탑재, 경보·대응 기능 통합, 시험 | End-to-End Increment |
| 8주차 | Sprint Review | 정량시험, 시연, 발표, 사용자 피드백 수집 | Sprint 1 Review 결과와 개선 Backlog |
| 9주차 | Sprint 2 | 요구사항 변경, 미비사항 보완, 회귀시험, 회고 | 개선 Increment, 회고록, 최종 Release |

### 5.2 Issue #1 세부 수행 일정

| 작업일 | 해야 할 일 | 담당 | 완료 기준 |
|---|---|---|---|
| Day 1 | Kick-off, 문제·사용자·Product Vision 합의 | 전원 | Vision 문장과 핵심 사용자 승인 |
| Day 2 | 포함/제외 범위, 제약, 정량 성공기준 정의 | Team Leader + QA | 범위와 SC-F/SC-NF 항목 Review 완료 |
| Day 3 | 9개 Issue, 의존관계, Sprint 배치와 담당 역할 정의 | Scrum Master | 모든 Issue에 Owner·일정·완료기준 존재 |
| Day 4 | GitHub Workflow, 품질관리, OSS 관리, 위험관리 방안 정의 | DevOps/QA | Branch·PR·시험·License 기준 문서화 |
| Day 5 | 팀 Review, 수정, 승인, PR Merge | Team Leader | 아래 DoD 충족 및 `develop` 반영 |

### 5.3 Issue Backlog 및 의존관계

| Issue | 작업 패키지 | 선행 작업 | 계획 완료 |
|---|---|---|---|
| #1 | Project Plan 및 Agile 운영 기준 수립 | 없음 | 4주차 |
| #2 | 이해관계자·요구사항·Use Case·정량 NFR 정의 | #1 | 5주차 |
| #3 | OSS 후보 조사·평가·라이선스 검토 및 선정 | #1, #2 | 5주차 |
| #4 | 시스템 아키텍처·데이터 모델·OpenAPI 설계 | #2, #3 | 5주차 |
| #5 | 설비 데이터 수집·전처리·저장 Pipeline 구현 | #4 | 6주차 |
| #6 | 실시간 모니터링 Dashboard 구현 | #4, #5 | 7주차 |
| #7 | AI 고장징후 예측 모델 개발·평가 | #2, #5 | 7주차 |
| #8 | AI 추론·경보·대응 권고 기능 통합 | #6, #7 | 7주차 |
| #9 | 통합시험·성능검증·문서화·시연·회고 | #5~#8 | 8~9주차 |

---

## 6. 팀 구성과 책임

한 사람이 여러 역할을 겸할 수 있지만, 작성자와 검토자는 가능한 한 분리한다.

| 역할 | 주요 책임 | 핵심 산출물 |
|---|---|---|
| Product Owner | 목표·우선순위·Acceptance Criteria 승인 | 우선순위와 Review 피드백 |
| Team Leader / Scrum Master | 일정, Issue, 회의, 장애요인, Merge 관리 | Project Plan, Sprint 현황, 회고록 |
| Data/AI 담당 | 데이터 분석·전처리·모델 학습·평가·탑재 지원 | Dataset 문서, Model, Model Card |
| Backend/Integration 담당 | 수집·저장·API·서비스 통합 | Backend Code, OpenAPI, DB Schema |
| Frontend/Dashboard 담당 | 상태·추이·경보·대응 화면 | Dashboard와 UI 시험 결과 |
| QA/DevOps 담당 | Test Plan, CI, 성능·보안·OSS 확인 | Test Report, CI, OSS 목록 |

### 6.1 협업 규칙

- 팀장은 Repository를 생성하고 팀원은 이를 Clone하여 작업한다.
- Branch 구조는 `main` → `develop` → `<작업유형>/<작업대상>`을 사용한다.
- Issue #1 Project Plan Branch는 `planning/project-plan`을 사용한다.
- 기존 명명 예: `requirement/system-requirements`, `research/thingsboard`, `evaluation/weighted-matrix`, `architecture/proposed`, `report/final-selection`
- `main`과 `develop`에 직접 Commit하지 않는다.
- Pull Request는 원칙적으로 `작업 Branch → develop`으로 생성한다.
- 최소 1명의 Review 승인과 CI 성공 후 Team Leader가 Merge한다.
- Sprint Review를 통과한 Increment만 `develop → main`으로 Merge하고 Tag를 부여한다.
- PR 본문에 관련 Issue를 `Closes #번호` 형식으로 연결한다.

---

## 7. 요구사항·작업·산출물 추적 방법

다음 연결을 유지하여 계획부터 시험 결과까지 추적 가능하게 한다.

`Project Goal → Requirement/User Story → GitHub Issue → Feature Branch → Commit → Pull Request → Test Case → Release`

| 관리 대상 | 식별 규칙 | 예시 |
|---|---|---|
| 기능 요구사항 | `FR-###` | `FR-007 AI 고장징후 추론` |
| 비기능 요구사항 | `NFR-###` | `NFR-004 추론 p95 ≤ 1초` |
| User Story | `US-###` | `US-005 정비담당자 위험설비 확인` |
| 시험 항목 | `TC-###` | `TC-021 Critical 경보 생성` |
| 모델 버전 | `model-name_vX.Y` | `rf_failure_v1.0` |
| Release Tag | `vX.Y.Z` | `v0.1.0-sprint1` |

---

## 8. 품질관리 계획

### 8.1 Definition of Ready: 개발 착수 조건

Issue는 다음 조건을 모두 충족해야 Sprint에 투입할 수 있다.

- [ ] 목적과 사용자 가치가 설명되어 있다.
- [ ] 작업 범위와 제외 범위가 명확하다.
- [ ] Acceptance Criteria가 측정 가능한 문장으로 작성되어 있다.
- [ ] 선행 Issue와 필요한 입력자료가 준비되어 있다.
- [ ] 담당자, Story Point, 목표 Sprint가 지정되어 있다.
- [ ] UI/API/Data 변경이 있으면 초안이 첨부되어 있다.
- [ ] 시험 방법과 완료 증거가 정의되어 있다.

### 8.2 공통 Definition of Done

- [ ] Acceptance Criteria를 모두 충족했다.
- [ ] 코드·설정·문서가 Feature Branch에 Commit되었다.
- [ ] 단위시험과 관련 API/통합시험이 통과했다.
- [ ] 정량 성능이 해당 요구사항 기준을 충족하거나 미달 원인이 기록되었다.
- [ ] 비밀정보와 불필요한 대용량 파일이 포함되지 않았다.
- [ ] 새로 사용한 OSS의 출처·버전·라이선스가 갱신되었다.
- [ ] 실행 또는 재현 방법이 README에 반영되었다.
- [ ] Pull Request Review와 CI가 완료되었다.
- [ ] 결과 증거인 로그, 화면, 표 또는 시험보고서가 PR에 연결되었다.
- [ ] Product Owner 또는 지정 검토자가 결과를 수용했다.

### 8.3 AI 산출물 추가 완료 기준

- [ ] Dataset의 출처, Label 정의, 크기와 분할 방법이 기록되었다.
- [ ] 동일 Test Set에서 Baseline과 후보 모델을 비교했다.
- [ ] Precision, Recall, F1-score, Confusion Matrix, FPR을 제시했다.
- [ ] 데이터 누수 여부와 클래스 불균형 처리 방법을 검토했다.
- [ ] 고정 Random Seed와 실행 명령으로 재현 가능하다.
- [ ] 채택 모델과 임계값의 선정 근거가 Model Card에 기록되었다.
- [ ] 학습 전처리와 운영 추론 전처리의 일치 여부를 시험했다.

---

## 9. 위험관리 계획

확률과 영향은 각각 1(낮음)~5(높음)이며, 위험도는 `확률 × 영향`으로 계산한다. 위험도 15 이상은 즉시 대응하고 매 Daily Scrum에서 확인한다.

| ID | 위험 | 확률 | 영향 | 위험도 | 예방·대응 방안 | 담당 |
|---|---|---:|---:|---:|---|---|
| R-01 | 고장 Label 데이터 부족 | 4 | 5 | 20 | 공개 데이터 확보, 이상탐지 대안 준비, 평가 구간 수동 검증 | Data/AI |
| R-02 | 클래스 불균형으로 고장 Recall 저하 | 4 | 4 | 16 | Class Weight, Sampling, 임계값 조정, F1/Recall 중심 평가 | Data/AI |
| R-03 | 여러 OSS 간 통합 지연 | 3 | 5 | 15 | 5주차 API/데이터 계약 확정, Docker Compose 최소 통합 조기 수행 | Integration |
| R-04 | 실제 센서 미확보 | 3 | 3 | 9 | 데이터 시뮬레이터와 CSV/MQTT Replay 준비 | Backend |
| R-05 | OSS 라이선스 충돌 또는 출처 누락 | 2 | 4 | 8 | 선정 전에 라이선스 검토, `THIRD_PARTY_NOTICES.md` 유지 | QA |
| R-06 | 팀원별 환경 차이 | 3 | 3 | 9 | `.env.example`, 고정 Version, Docker 기반 실행 절차 제공 | DevOps |
| R-07 | 무리한 기능 확장 | 4 | 4 | 16 | Must/Should/Could 우선순위, Sprint 1은 End-to-End 최소기능 우선 | Team Leader |
| R-08 | 비밀키 또는 민감정보 Commit | 2 | 5 | 10 | `.gitignore`, 환경변수, Secret Scan, 즉시 키 폐기·재발급 | DevOps |

---

## 10. 형상·변경·의사소통 관리

### 10.1 형상관리 대상

- Source Code, AI 학습·추론 Code, 설정 파일
- OpenAPI, DB Schema, Architecture Diagram
- Requirements, OSS 평가표, Project/Sprint 문서
- Test Code와 Test Report
- 모델 메타데이터와 Model Card
- 작은 Sample Data와 데이터 생성 Script

원본 대용량 Dataset과 대용량 Model 파일은 일반 Git에 직접 저장하지 않고, 위치·Version·Hash·획득 방법을 문서화한다.

### 10.2 변경관리

1. 변경 요청을 새 Issue로 등록한다.
2. 변경 사유, 영향 받는 요구사항·API·데이터·일정·시험을 분석한다.
3. Product Owner와 팀이 우선순위 및 Sprint 반영 여부를 결정한다.
4. 승인된 변경만 Backlog와 관련 문서에 반영한다.
5. 구현 후 회귀시험을 수행하고 PR에서 변경 전후를 설명한다.

### 10.3 회의와 보고

| 활동 | 주기 | 핵심 내용 | 기록 위치 |
|---|---|---|---|
| Sprint Planning | Sprint 시작 | 목표, Backlog, Story Point, 담당 | GitHub Project/회의록 |
| Daily Scrum | 개발일마다 10~15분 | 완료, 오늘 계획, Blocker | Project Comment 또는 회의록 |
| Backlog Refinement | 주 1회 | 요구 명확화, 분할, 우선순위 | GitHub Issues |
| Sprint Review | Sprint 종료 | Increment 시연, 정량 결과, 수용 여부 | Review Report |
| Retrospective | Review 후 | Keep, Problem, Try, Action Owner | Retrospective 문서 |

---

## 11. 계획 산출물과 Repository 위치

| 산출물 | 권장 경로 | 생성 Issue |
|---|---|---|
| Project Plan | `docs/project-management/project-plan.md` | #1 |
| 요구사항 및 User Story | `docs/requirements.md` | #2 |
| OSS 평가 및 라이선스 | `docs/oss-evaluation.md` | #3 |
| Architecture 문서 | `docs/architecture.md` | #4 |
| OpenAPI 명세 | `openapi/openapi.yaml` | #4 |
| 데이터 설명 | `data/README.md` | #5, #7 |
| Model Card | `models/model-card.md` | #7 |
| Test Plan/Report | `tests/test-plan.md`, `docs/test-report.md` | #9 |
| OSS 고지 | `THIRD_PARTY_NOTICES.md` | #3, #9 |
| 설치·실행·시연 방법 | `README.md` | #9 |
| Sprint 회고 | `docs/retrospective.md` | #9 |

---

## 12. Issue #1 Acceptance Criteria

- [x] 프로젝트 배경, 목표와 Product Vision이 정의되어 있다.
- [x] 주요 사용자와 사용자별 요구가 정의되어 있다.
- [x] 포함 범위, 제외 범위와 제약조건이 정의되어 있다.
- [x] 기능 및 비기능 성공 기준이 실제 수치로 정의되어 있다.
- [x] AI 모델을 직접 개발·평가·적용하는 방안이 포함되어 있다.
- [x] 4~9주차 Agile 일정과 9개 Issue의 의존관계가 정의되어 있다.
- [x] 팀 역할, GitHub Branch/PR/Review 규칙이 정의되어 있다.
- [x] DoR, 공통 DoD와 AI 추가 DoD가 정의되어 있다.
- [x] 주요 위험, 대응방안, 형상·변경·의사소통 관리가 정의되어 있다.
- [ ] 팀 Review 후 승인 의견이 기록되어 있다.
- [ ] PR의 자동시험/문서검사가 통과하고 `develop`에 Merge되었다.

## 13. 승인 기록

| 구분 | 이름 | 검토 결과 | 날짜 | 의견 |
|---|---|---|---|---|
| 작성 |  |  |  |  |
| 팀 검토 |  |  |  |  |
| 승인 |  |  |  |  |

---

## 14. Issue #1 종료 절차

1. 본 파일을 `planning/project-plan` Branch의 `docs/project-management/project-plan.md`로 등록한다.
2. 팀원이 범위, 정량 목표, 일정, 담당 역할을 Review한다.
3. Review 의견을 반영하고 승인 기록을 작성한다.
4. Pull Request 제목을 `[#1] Add Smart Factory project plan`으로 작성한다.
5. PR 본문에 변경 요약, 검토 항목, 결과 화면 또는 문서 링크, `Closes #1`을 작성한다.
6. Review 승인과 CI 성공 후 Team Leader가 `develop`에 Merge한다.
7. Merge 후 Issue #1이 자동으로 닫혔는지와 GitHub Project 상태가 `Done`인지 확인한다.
