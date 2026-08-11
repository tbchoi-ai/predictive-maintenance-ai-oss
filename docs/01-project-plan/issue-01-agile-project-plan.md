# [Agile 계획] 설비 상태 모니터링 및 AI 기반 예지보전 시스템 프로젝트 추진계획 수립

## 1. Issue 기본정보

| 항목 | 권장 설정값 |
|---|---|
| Issue 번호 | `#1` |
| Issue 유형 | Agile 프로젝트 계획 / Product Planning |
| 적용 방법 | Scrum 기반의 반복·점진적 개발 |
| Sprint 주기 | 2주 |
| 전체 수행기간 | 10주, 총 5개 Sprint |
| 권장 Assignee | 팀장 또는 Scrum Master |
| 권장 Labels | `type: planning`, `agile`, `priority: high`, `documentation` |
| 권장 Project | `Predictive Maintenance AI & OSS Project` |
| 권장 Milestone | `Release 1.0 – Predictive Maintenance MVP` |
| Relationships | 선행 이슈 없음 |
| 작업 Branch | `planning/project-plan` |
| PR 대상 Branch | `develop` |
| 산출물 파일 | `docs/01-project-plan/agile-project-plan.md` |

---

## 2. 프로젝트 개요

본 프로젝트는 제조설비의 진동, 온도, 전류, 압력 등 센서데이터를 수집·저장·시각화하고, AI 모델을 이용하여 고장징후를 사전에 예측하는 시스템을 개발하는 것을 목적으로 한다. 예측된 설비 상태에 따라 Normal, Warning, Alert를 구분하여 표시하고, 운용자와 정비담당자가 조기에 점검·정비 조치를 수행할 수 있도록 지원한다.

프로젝트는 Scrum 기반의 반복·점진적 개발방식을 적용한다. 프로젝트 초기에 모든 요구사항과 설계를 완전히 확정하지 않고 Product Backlog를 구성한 후, 우선순위가 높은 User Story부터 2주 단위 Sprint로 개발한다. 각 Sprint 종료 시 실제로 실행 가능한 시스템 Increment를 시연하고, 사용자 및 교수자의 피드백을 다음 Sprint의 Product Backlog와 설계에 반영한다.

---

## 3. Product Vision

> 설비 운용자와 정비담당자가 실시간 설비 상태와 AI가 예측한 고장징후를 쉽게 확인하고, Warning 또는 Alert 발생 시 고장 전에 점검·정비 조치를 수행할 수 있는 개방형 OSS 기반 예지보전 시스템을 제공한다.

### Product Goal

10주 이내에 센서데이터 수집부터 AI 고장징후 예측, 대시보드 표시, Warning/Alert 발생 및 대응조치 기록까지 연결되는 실행 가능한 MVP를 완성하고 시연한다.

### 주요 사용자 클래스

| User Class | 주요 요구 및 역할 |
|---|---|
| 설비 운용자 | 설비 상태 확인, Warning/Alert 인지, 초기 대응 |
| 정비담당자 | 고장징후와 원인정보 확인, 점검·정비 수행 및 결과 기록 |
| 생산관리자 | 설비별 상태, 경보이력 및 가동현황 확인 |
| 데이터·AI 담당자 | 학습데이터 관리, AI 모델 학습·평가·배포 및 성능 감시 |
| 시스템 관리자 | 사용자, 센서, OSS 구성, 보안, 로그 및 시스템 상태 관리 |

---

## 4. MVP 범위

### MVP 포함범위

- [ ] 1종 이상의 설비 또는 공개 예지보전 데이터셋을 대상으로 한다.
- [ ] 온도, 진동, 전류 등 3종 이상의 센서데이터를 처리한다.
- [ ] 센서데이터 수집, 저장, 조회 및 대시보드 시각화를 구현한다.
- [ ] 데이터 정제, 결측처리, 특징 추출 및 학습데이터 생성을 구현한다.
- [ ] 최소 1개의 기준 AI 모델과 1개의 비교모델을 개발·평가한다.
- [ ] 선정된 AI 모델의 추론기능을 모니터링 시스템에 적용한다.
- [ ] Normal, Warning, Alert 상태와 근거정보를 표시한다.
- [ ] 운용자 확인, 정비 요청 및 조치 결과 기록 흐름을 구현한다.
- [ ] OSS 구성요소의 라이선스, 보안 및 유지관리 상태를 평가한다.
- [ ] 통합시험, 사용자 시연 및 최종 결과보고서를 작성한다.

### MVP 제외범위

- 실제 공장 전체 설비에 대한 상용 수준 배포
- 안전제어장치의 자동 정지 또는 직접 제어
- 다수 공장 간 대규모 통합운영
- 장기간 현장데이터를 이용한 모델 재학습 자동화
- 모바일 애플리케이션과 ERP·MES의 완전한 연동

---

## 5. Agile 추진원칙

1. 기능은 사용자 가치가 확인되는 작은 User Story 단위로 분할한다.
2. Product Owner는 사용자 가치, 위험, 의존성 및 학습효과를 기준으로 Product Backlog의 우선순위를 결정한다.
3. Sprint 중에는 Sprint Goal을 안정적으로 유지하며, 긴급 변경은 Product Owner와 팀의 합의로 처리한다.
4. 각 Sprint에서 분석, 설계, OSS 검토, 구현, 시험 및 문서화를 함께 수행한다.
5. 각 Sprint 종료 시 실행 가능한 Increment를 시연한다.
6. AI 모델은 기준모델, 성능개선 모델, 시스템 통합모델 순으로 반복 개발한다.
7. OSS는 문서평가만으로 결정하지 않고 최소 기능검증 또는 PoC 결과를 반영한다.
8. 비기능 요구사항과 보안은 마지막 Sprint에 집중하지 않고 모든 Sprint의 Definition of Done에 적용한다.
9. GitHub Issue, Project, Branch, Pull Request 및 Review 기록을 프로젝트 관리의 공식 근거로 사용한다.

---

## 6. Scrum 역할과 책임

| 역할 | 권장 담당 | 주요 책임 |
|---|---|---|
| Product Owner | 교수자 또는 지정 사용자 대표 | Product Goal 제시, Backlog 우선순위 결정, Increment 수용 여부 판단 |
| Scrum Master | 팀장 | Scrum 진행 지원, 장애요인 제거, 회의 운영 및 팀 협업 촉진 |
| Developers | 학생 팀원 전체 | 분석, 설계, OSS 조사, 코딩, AI 개발, 시험 및 문서화 공동 수행 |
| Stakeholder | 설비 운용자·정비담당자 역할 학생 또는 외부 검토자 | Sprint Review 참여, 사용자 관점 피드백 제공 |

Scrum Master는 업무를 일방적으로 지시하는 관리자가 아니라, 팀이 Sprint Goal을 달성하도록 지원하고 장애요인을 제거하는 역할을 수행한다.

---

## 7. 초기 Product Backlog

아래 항목은 프로젝트 착수 시점의 초기 Backlog이며, Sprint Review 결과에 따라 추가·수정·재정렬할 수 있다.

| ID | Product Backlog Item | User Story 요약 | 우선순위 | 초기 추정치 |
|---|---|---|---:|---:|
| PB-01 | 센서데이터 수집 | 운용자로서 실시간 설비데이터를 수집하고 싶다. | Must | 8 SP |
| PB-02 | 데이터 저장·조회 | 운용자로서 현재·과거 데이터를 조회하고 싶다. | Must | 5 SP |
| PB-03 | 상태 대시보드 | 운용자로서 주요 센서값과 설비상태를 한 화면에서 보고 싶다. | Must | 8 SP |
| PB-04 | 데이터 품질관리 | AI 담당자로서 결측·이상 데이터를 확인하고 정제하고 싶다. | Must | 5 SP |
| PB-05 | OSS 후보 검증 | 개발팀으로서 계층별 OSS를 동일 기준으로 평가하고 싶다. | Must | 8 SP |
| PB-06 | AI 기준모델 | AI 담당자로서 고장징후 예측의 기준 성능을 확보하고 싶다. | Must | 13 SP |
| PB-07 | AI 모델 개선 | 정비담당자로서 신뢰할 수 있는 고장징후를 조기에 알고 싶다. | Must | 13 SP |
| PB-08 | 실시간 추론 연동 | 운용자로서 새 센서데이터에 대한 AI 예측결과를 확인하고 싶다. | Must | 13 SP |
| PB-09 | Warning·Alert | 운용자로서 위험도에 따라 구분된 경보를 받고 싶다. | Must | 8 SP |
| PB-10 | 조기 대응관리 | 정비담당자로서 경보 확인, 정비요청 및 조치결과를 기록하고 싶다. | Should | 8 SP |
| PB-11 | 보안·성능·신뢰성 | 관리자로서 시스템이 안전하고 안정적으로 작동하는지 확인하고 싶다. | Must | 8 SP |
| PB-12 | 최종 통합·시연 | 관리자로서 전체 기능과 성능을 검증하고 결과를 확인하고 싶다. | Must | 8 SP |

> Story Point는 시간 단위가 아니라 상대적인 작업 규모, 복잡성 및 불확실성을 나타낸다. 첫 Sprint 이후 실제 수행결과를 기준으로 추정치를 조정한다.

---

## 8. 대표 User Story 및 인수조건

### US-01 설비 상태 모니터링

**User Story**  
설비 운용자로서, 현재 센서값과 설비 상태를 실시간 대시보드에서 확인하고 싶다. 그래야 이상 상태를 신속하게 인지할 수 있다.

**Acceptance Criteria**

- [ ] 온도, 진동, 전류 등 최소 3종의 센서값이 표시된다.
- [ ] 데이터 수집 후 대시보드 표시까지의 지연시간은 정상 부하에서 p95 기준 5초 이하이다.
- [ ] 센서 연결이 중단되면 30초 이내에 데이터 단절 상태가 표시된다.
- [ ] 설비별 현재 상태가 Normal, Warning, Alert 중 하나로 표시된다.

### US-02 AI 고장징후 예측

**User Story**  
정비담당자로서, AI가 분석한 고장징후와 위험도를 확인하고 싶다. 그래야 실제 고장 전에 점검과 정비를 수행할 수 있다.

**Acceptance Criteria**

- [ ] 동일 데이터 분할조건에서 기준모델과 비교모델의 성능이 제시된다.
- [ ] 최종모델은 시험데이터 기준 F1-score 0.85 이상을 목표로 한다.
- [ ] 고장징후 Recall은 0.90 이상을 목표로 한다.
- [ ] False Positive Rate는 10% 이하를 목표로 한다.
- [ ] 예측결과에 모델 버전, 예측시간, 위험점수 및 주요 입력정보가 기록된다.
- [ ] 시계열 데이터가 조기예측 평가에 적합한 경우 고장 발생 10분 전 Warning 탐지를 목표로 한다.

### US-03 경보 및 조기 대응

**User Story**  
설비 운용자로서, 위험수준에 따른 Warning 또는 Alert를 받고 조치상태를 기록하고 싶다. 그래야 경보가 실제 정비활동으로 연결되었는지 확인할 수 있다.

**Acceptance Criteria**

- [ ] 위험점수 또는 규칙에 따라 Warning과 Alert가 구분된다.
- [ ] AI 추론 완료 후 경보 표시까지의 지연시간은 p95 기준 3초 이하이다.
- [ ] 경보에는 설비 ID, 발생시각, 위험수준, 관련 센서값 및 권고조치가 포함된다.
- [ ] 사용자가 경보 확인, 정비요청, 조치완료 상태를 기록할 수 있다.
- [ ] 경보 발생부터 조치완료까지의 이력이 저장되고 조회된다.

---

## 9. Sprint 및 Release 계획

전체 기간은 10주이며 2주 단위의 5개 Sprint로 구성한다. Sprint별 Backlog는 Sprint Planning에서 팀의 Capacity와 우선순위를 고려하여 확정한다.

| Sprint | 기간 | Sprint Goal | 주요 후보 Backlog | 시연 가능한 Increment |
|---|---|---|---|---|
| Sprint 1 | 1~2주 | 센서데이터가 시스템에 들어와 화면에 표시되는 기본 흐름 구축 | PB-01, PB-02, PB-03 일부, PB-05 일부 | 모의 센서데이터 수집·저장·기본 차트 표시 |
| Sprint 2 | 3~4주 | 신뢰할 수 있는 데이터 파이프라인과 상태 모니터링 완성 | PB-03, PB-04, PB-05, PB-11 일부 | 데이터 품질확인, 설비상태 대시보드, OSS PoC 결과 |
| Sprint 3 | 5~6주 | AI 기준모델을 개발하고 평가 가능한 결과 확보 | PB-06, PB-07 일부 | 학습데이터셋, 기준모델, 비교평가 리포트 |
| Sprint 4 | 7~8주 | AI 예측결과를 실시간 시스템과 Warning·Alert에 연결 | PB-07, PB-08, PB-09 | 센서입력→AI 추론→경보 표시 End-to-End 시연 |
| Sprint 5 | 9~10주 | 사용자 조기대응 흐름과 품질을 검증하고 MVP Release 완성 | PB-10, PB-11, PB-12 | 경보 조치관리, 통합시험, 최종 시연 및 Release 1.0 |

### Release 기준

- Release 이름: `Release 1.0 – Predictive Maintenance MVP`
- Release 목표일: 10주차 Sprint Review 종료 시점
- Release 대상: `main` Branch
- Release Tag 예시: `v1.0.0`

---

## 10. Scrum Event 운영계획

| Event | 수행 시점 | 권장 시간 | 주요 결과 |
|---|---|---:|---|
| Product Backlog Refinement | 매주 1회 | 30~45분 | Story 분할, 우선순위 및 추정치 보완 |
| Sprint Planning | 각 Sprint 첫날 | 60~90분 | Sprint Goal 및 Sprint Backlog 확정 |
| Daily Scrum | 매일 또는 수업일마다 | 10~15분 | 진행상태, 당일계획, 장애요인 공유 |
| Sprint Review | 각 Sprint 마지막 날 | 45~60분 | 실행 가능한 Increment 시연 및 사용자 피드백 |
| Sprint Retrospective | Review 이후 | 30~45분 | 협업·도구·프로세스 개선항목 합의 |

Daily Scrum을 매일 대면으로 수행하기 어려운 경우 GitHub Project의 Status 갱신과 짧은 온라인 보고로 대체하되, 각 팀원은 진행내용과 장애요인을 매일 기록한다.

---

## 11. Definition of Ready

User Story를 Sprint Backlog에 포함하려면 다음 조건을 충족해야 한다.

- [ ] User Class와 사용자 가치가 명확하다.
- [ ] User Story가 `As a–I want–So that` 형식으로 작성되어 있다.
- [ ] Acceptance Criteria가 시험 가능한 형태로 작성되어 있다.
- [ ] 필요한 데이터, OSS, API 및 외부 의존성이 식별되어 있다.
- [ ] 보안, 성능, 라이선스 등 주요 제약조건이 확인되어 있다.
- [ ] 한 Sprint 안에 완료할 수 있는 크기로 분할되어 있다.
- [ ] Story Point가 팀 합의로 추정되어 있다.
- [ ] Product Owner가 우선순위를 확인하였다.

---

## 12. Definition of Done

User Story 또는 Task는 다음 조건을 모두 충족해야 Done으로 처리한다.

- [ ] Acceptance Criteria를 모두 충족한다.
- [ ] 코드, 구성파일 또는 문서가 지정된 작업 Branch에 작성되어 있다.
- [ ] 자동시험 또는 수동시험 결과가 기록되어 있다.
- [ ] 핵심 로직에 단위시험 또는 재현 가능한 검증절차가 있다.
- [ ] 치명적·높음 등급의 미조치 보안취약점이 없다.
- [ ] 사용한 OSS의 명칭, 버전, 출처 및 라이선스가 기록되어 있다.
- [ ] AI 결과물에는 데이터 버전, 모델 버전, 평가방법 및 성능지표가 기록되어 있다.
- [ ] Pull Request가 생성되고 최소 1명의 Review 승인을 받았다.
- [ ] Review 의견이 조치되었고 `develop`에 병합되었다.
- [ ] 사용자 문서 또는 기술문서가 변경내용에 맞게 갱신되었다.
- [ ] Sprint Review에서 실행 가능한 결과를 시연할 수 있다.
- [ ] Product Owner가 해당 Increment를 수용하였다.

---

## 13. GitHub Project 운영방법

### 권장 Status 열

| Status | 의미 |
|---|---|
| Backlog | 향후 개발할 Product Backlog Item |
| Ready | DoR를 만족하여 다음 Sprint에 선택 가능 |
| In Progress | 담당자가 현재 작업 중 |
| Review | PR, 시험 또는 Product Owner 검토 중 |
| Done | DoD와 인수조건을 모두 충족 |

### Issue 계층

| 계층 | GitHub 표현 | 예시 |
|---|---|---|
| Epic | 상위 Issue 또는 `type: epic` Label | AI 기반 고장징후 예측 |
| User Story | Issue와 `type: story` Label | 정비담당자의 고장징후 확인 |
| Task | Sub-issue 또는 `type: task` Label | 특징 추출 코드 작성 |
| Bug | Issue와 `type: bug` Label | 경보 중복 발생 수정 |
| Spike | Issue와 `type: spike` Label | AI 알고리즘·OSS 기술검증 |

### 권장 Custom Field

- `Status`: Backlog / Ready / In Progress / Review / Done
- `Sprint`: Sprint 1~5
- `Priority`: Must / Should / Could / Won't
- `Story Points`: 1 / 2 / 3 / 5 / 8 / 13
- `User Class`: Operator / Maintainer / Manager / AI Engineer / Administrator
- `Component`: Sensor / Data / Dashboard / AI / Alert / DevOps

### 작업 제한

- 팀원 1인당 동시에 진행하는 Issue는 원칙적으로 1개, 최대 2개로 제한한다.
- 완료되지 않은 작업을 추가로 시작하기보다 Review 또는 장애해결을 먼저 지원한다.
- Sprint 종료 시 미완료 항목은 자동으로 Done 처리하지 않고 Product Backlog로 되돌려 재평가한다.

---

## 14. Branch, Commit 및 Pull Request 계획

### Branch 구조

```text
main
└── develop
    ├── planning/project-plan
    ├── feature/<issue-number>-<feature-name>
    ├── ai/<issue-number>-<model-name>
    ├── docs/<issue-number>-<document-name>
    └── fix/<issue-number>-<bug-name>
```

### Issue #1 작업 절차

1. `develop` Branch를 기준으로 `planning/project-plan`을 생성한다.
2. 본 Agile Project Plan을 `docs/01-project-plan/agile-project-plan.md`에 작성한다.
3. Product Owner와 팀원이 Product Goal, MVP, Sprint 계획 및 DoD를 검토한다.
4. Commit 후 원격 Repository로 Push한다.
5. 다음 조건으로 Pull Request를 생성한다.

```text
base: develop  ←  compare: planning/project-plan
```

6. PR 본문에 `Relates to #1`을 입력한다.
7. Review 의견을 반영한 후 `develop`에 병합한다.
8. Product Owner 승인 후 Issue #1을 Close한다.

### Commit 메시지 예시

```text
docs: add agile project plan for predictive maintenance MVP
```

### PR 제목 예시

```text
[Issue #1] Agile 프로젝트 추진계획서 작성
```

### User Story Branch 예시

```text
feature/12-sensor-data-ingestion
feature/18-monitoring-dashboard
ai/25-failure-prediction-baseline
feature/31-warning-alert-service
```

---

## 15. 추정 및 진척관리

### Story Point 추정기준

| Point | 상대적 의미 |
|---:|---|
| 1 | 매우 작고 명확한 작업 |
| 2 | 작은 작업, 불확실성 낮음 |
| 3 | 보통 규모, 일부 검토 필요 |
| 5 | 여러 작업이 연계되거나 기술검증 필요 |
| 8 | 복잡하고 불확실성이 높은 작업 |
| 13 | 너무 크거나 불확실함. 가능한 경우 분할 필요 |

### 관리 지표

- Sprint Goal 달성 여부
- 계획 Story Point 대비 완료 Story Point
- Sprint별 Velocity 추세
- Sprint Burndown Chart
- 계획 대비 미완료 Story 수
- 결함 수와 재발 결함 수
- Pull Request 평균 Review 대기시간
- AI 모델 F1-score, Recall 및 False Positive Rate
- 데이터 수집·표시 지연시간과 경보 발생 지연시간

Velocity는 팀 성과를 비교하거나 개인을 평가하는 용도가 아니라 다음 Sprint의 적정 작업량을 예측하는 용도로만 사용한다.

---

## 16. 예상 위험 및 Agile 대응방안

| ID | 위험 | 초기 대응 및 Backlog 반영방법 |
|---|---|---|
| RSK-01 | 실제 고장데이터 부족 | Sprint 1에 데이터 적합성 Spike 수행, 공개데이터와 이상탐지 방식 병행 |
| RSK-02 | 센서데이터 결측·노이즈 | Sprint 2에 데이터 품질 User Story를 Must로 배치 |
| RSK-03 | AI 성능목표 미달 | Sprint 3 기준모델 결과를 Review하고 Sprint 4 개선 Backlog 재정렬 |
| RSK-04 | Warning·Alert 오탐·미탐 | 임계값 조정, 혼동행렬 검토, 사용자 피드백을 다음 Sprint에 반영 |
| RSK-05 | OSS 통합 실패 | 핵심 OSS는 Sprint 1~2에 Spike와 최소 PoC로 조기검증 |
| RSK-06 | OSS 라이선스·취약점 문제 | DoR·DoD에 라이선스 및 보안검토를 포함하고 대체후보 유지 |
| RSK-07 | 특정 팀원에게 작업 집중 | Story 분할, Pair Work, WIP 제한 및 Review 공동수행 |
| RSK-08 | Sprint 범위 과다 | 우선순위가 낮은 항목을 Product Backlog로 반환하고 Sprint Goal 중심으로 조정 |

---

## 17. Issue #1 세부 작업

- [ ] Product Vision과 Product Goal을 작성한다.
- [ ] 주요 User Class와 Stakeholder를 식별한다.
- [ ] 10주 내 개발할 MVP의 포함범위와 제외범위를 정의한다.
- [ ] Product Owner, Scrum Master 및 Developers 역할을 지정한다.
- [ ] 초기 Product Backlog를 작성하고 우선순위를 부여한다.
- [ ] 대표 User Story와 정량적 Acceptance Criteria를 작성한다.
- [ ] 2주 단위 5개 Sprint의 Sprint Goal과 예상 Increment를 정의한다.
- [ ] Scrum Event 일정과 운영방법을 정한다.
- [ ] Definition of Ready와 Definition of Done을 팀이 합의한다.
- [ ] GitHub Project Status와 Custom Field를 구성한다.
- [ ] Branch, Commit, Pull Request 및 Review 규칙을 정의한다.
- [ ] 초기 위험목록과 Agile 대응방안을 작성한다.
- [ ] 팀 내부검토와 Product Owner 승인을 받는다.

---

## 18. Issue #1 완료기준

다음 조건을 모두 충족하면 Issue #1을 완료한다.

- [ ] `docs/01-project-plan/agile-project-plan.md`가 작성되어 있다.
- [ ] Product Vision, Product Goal 및 MVP 범위가 팀에 공유되어 있다.
- [ ] 주요 User Class와 Scrum 역할별 담당자가 정해져 있다.
- [ ] 초기 Product Backlog가 GitHub Issues 또는 Project에 등록되어 있다.
- [ ] 각 Backlog Item에 우선순위가 설정되어 있다.
- [ ] Sprint 1 후보 User Story가 DoR을 충족한다.
- [ ] 총 5개 Sprint의 목표와 Release 계획이 정의되어 있다.
- [ ] 팀이 Definition of Ready와 Definition of Done에 합의하였다.
- [ ] GitHub Project의 Status, Sprint, Priority 및 Story Points 필드가 설정되어 있다.
- [ ] `planning/project-plan`에서 `develop`로 향하는 PR이 생성되어 있다.
- [ ] PR Review 의견이 반영되고 `develop`에 병합되어 있다.
- [ ] Product Owner가 Agile Project Plan과 Sprint 1 착수를 승인하였다.

---

## 19. 후속 작업

Issue #1 완료 후 다음 활동을 수행한다.

1. 초기 Product Backlog 항목을 실제 GitHub User Story Issue로 등록한다.
2. 큰 Backlog Item은 한 Sprint 안에 완료할 수 있도록 Sub-issue 또는 Task로 분할한다.
3. 팀 단위로 Story Point를 추정한다.
4. Product Owner가 우선순위를 확정한다.
5. Sprint 1 Planning을 수행하고 Sprint Goal과 Sprint Backlog를 확정한다.
6. Sprint 1 개발을 시작한다.
