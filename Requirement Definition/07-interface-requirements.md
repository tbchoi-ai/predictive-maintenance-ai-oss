# Smart Factory 예지보전 시스템 인터페이스 요구사항 명세서

## 1. 목적

설비 센서, IoT Gateway, 사용자 단말, 알림서비스, 외부 업무시스템 및 AI 모델서비스 사이에서 교환되는 정보와 통신·보안·오류처리 조건을 정의한다. 특정 OSS 제품을 결정하기 전 단계이므로 표준과 필요한 기능을 중심으로 작성한다.

## 2. 인터페이스 목록

| ID | Interface | 송신 | 수신 | 주요 데이터 |
|---|---|---|---|---|
| IF-01 | Sensor-Gateway | 센서/PLC | IoT Gateway | 측정값, 상태, 측정시각 |
| IF-02 | Gateway-Message Ingestion | Gateway | 수집·Message Service | 표준 센서 메시지, Heartbeat |
| IF-03 | Processing-Storage | 처리서비스 | 시계열·관계형 저장소 | 원시·가공 데이터, Metadata |
| IF-04 | Analysis-Model Service | 분석 Orchestrator | AI 모델서비스 | 특징 Vector, Model Version |
| IF-05 | Model Result | AI 모델서비스 | 분석·경보서비스 | Score, Class, Confidence |
| IF-06 | Web/API-User | Backend API | Dashboard/Client | 상태, 경보, 정비, KPI |
| IF-07 | Alert-Notification | 경보서비스 | Email/SMS/메시지 | 경보내용, 수신자, 결과 |
| IF-08 | Maintenance-MES/CMMS | 통합서비스 | 외부 업무시스템 | 설비, 작업지시, 정비이력 |
| IF-09 | Identity Provider | 인증서비스 | 사용자·API | Token, Role, Session |
| IF-10 | Monitoring-Admin | 모든 서비스 | Monitoring/Logging | Metric, Log, Trace, Health |

## 3. 공통 메시지 요구사항

| ID | 인터페이스 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-COM-001 | 모든 센서·분석 메시지는 Schema Version을 포함해야 한다. | P0 | I/T |
| IR-COM-002 | 메시지는 UTC 기준 Event Time과 시스템 수신시간을 포함해야 한다. | P0 | I/T |
| IR-COM-003 | 메시지는 추적 가능한 Message ID 또는 Correlation ID를 포함해야 한다. | P0 | I/T |
| IR-COM-004 | 메시지의 필수항목, 자료형, 단위 및 허용범위를 Schema로 검증할 수 있어야 한다. | P0 | T |
| IR-COM-005 | 잘못된 메시지는 정상 데이터와 분리하여 오류원인과 함께 저장하거나 격리해야 한다. | P0 | T |
| IR-COM-006 | Interface 변경은 하위호환 또는 명시된 Migration 절차를 제공해야 한다. | P1 | I/A |

## 4. IF-01 Sensor-Gateway 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-SG-001 | Gateway는 각 센서의 ID, 측정항목, 값, 단위, 측정시각 및 품질상태를 수신해야 한다. | P0 | T |
| IR-SG-002 | Sensor Protocol Adapter는 설비별 원본 Protocol과 상위 표준메시지를 분리해야 한다. | P1 | A/I |
| IR-SG-003 | Gateway는 센서 연결상태와 마지막 정상수신 시각을 유지해야 한다. | P0 | T |
| IR-SG-004 | 센서·Protocol 오류는 다른 센서 데이터 수집을 중단시키지 않아야 한다. | P0 | T |

## 5. IF-02 Gateway-Message Ingestion 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-GM-001 | Gateway와 Message Service는 MQTT 3.1.1 이상 또는 동등한 표준 Pub/Sub Protocol을 지원해야 한다. | P0 | I/T |
| IR-GM-002 | Topic은 공장, 라인, 설비, 센서 및 메시지유형을 식별할 수 있는 구조를 가져야 한다. | P0 | I/T |
| IR-GM-003 | 중요 센서 메시지는 최소 At-Least-Once 전달수준을 지원해야 한다. | P0 | T |
| IR-GM-004 | Gateway는 연결단절 시 데이터를 로컬 버퍼에 저장하고 복구 후 원 측정시각과 함께 재전송해야 한다. | P0 | T |
| IR-GM-005 | Message Service는 장치별 인증과 Topic별 Publish/Subscribe 권한통제를 지원해야 한다. | P0 | T/I |
| IR-GM-006 | Heartbeat 메시지는 Gateway ID, 상태, 마지막 센서수신 및 자원상태를 포함해야 한다. | P1 | I/T |

## 6. 센서 메시지 예시 Schema

| Field | 자료형 | 필수 | 설명 |
|---|---|---:|---|
| schemaVersion | String | Y | 메시지 Schema 버전 |
| messageId | String | Y | 중복·추적용 고유 ID |
| equipmentId | String | Y | 설비 고유 ID |
| sensorId | String | Y | 센서 고유 ID |
| metric | String | Y | vibrationRms, temperature 등 |
| value | Number | Y | 측정값 |
| unit | String | Y | mm/s, Celsius, Ampere 등 |
| eventTime | ISO 8601 | Y | 센서 측정시각 UTC |
| gatewayTime | ISO 8601 | Y | Gateway 수신시각 UTC |
| quality | Enum | Y | Good, Suspect, Bad |
| sequence | Integer | N | 순서·누락 확인용 번호 |

## 7. IF-03 Processing-Storage 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-PS-001 | 처리서비스는 원시데이터와 변환·집계데이터를 논리적으로 구분하여 저장해야 한다. | P0 | I/T |
| IR-PS-002 | 저장 Interface는 Batch와 Stream 입력을 구분하고 중복방지 기준을 제공해야 한다. | P1 | T/I |
| IR-PS-003 | 시계열 조회는 설비, 센서, 시작·종료시각, 집계간격 및 품질상태를 입력받아야 한다. | P0 | T |
| IR-PS-004 | 정비·사용자·장치 Metadata는 참조무결성을 유지해야 한다. | P0 | T/I |

## 8. IF-04·05 AI 모델서비스 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-AI-001 | 분석요청은 설비 ID, 분석시각, Feature Set Version, Model ID·Version과 특징값을 포함해야 한다. | P0 | I/T |
| IR-AI-002 | 분석응답은 Model ID·Version, Score, 예측 Class, Confidence, 처리시간 및 오류코드를 포함해야 한다. | P0 | I/T |
| IR-AI-003 | 모델서비스는 Health Check와 Model Metadata 조회 Interface를 제공해야 한다. | P0 | T/D |
| IR-AI-004 | 모델서비스 오류 또는 Timeout은 경보서비스의 전체중단을 유발하지 않아야 한다. | P0 | T |
| IR-AI-005 | 입력 특징 누락 또는 품질저하 시 오류·저하모드를 명확히 반환해야 한다. | P0 | T |
| IR-AI-006 | 모델서비스는 승인된 모델버전만 운영 Endpoint에 연결해야 한다. | P0 | I/T |
| IR-AI-007 | 외부 AI API의 단순호출이 아닌 학생이 직접 개발한 모델을 배포·호출할 수 있어야 한다. | P0 | I/D |

## 9. IF-06 Web/API-User 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-WEB-001 | Web API는 HTTPS 기반의 표준 REST/JSON Interface를 제공해야 한다. | P0 | I/T |
| IR-WEB-002 | API는 사용자 Token과 Role을 검증하고 권한 없는 요청에 적절한 오류를 반환해야 한다. | P0 | T |
| IR-WEB-003 | 목록 API는 Pagination, 정렬, 필터 및 조회기간 제한을 지원해야 한다. | P1 | T |
| IR-WEB-004 | API 오류응답은 오류코드, 사용자 메시지, Correlation ID와 발생시각을 포함해야 한다. | P0 | I/T |
| IR-WEB-005 | 경보상태 변경 API는 동시수정 충돌을 검출하거나 최신버전을 확인해야 한다. | P1 | T |

## 10. IF-07 Alert-Notification 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-ALR-001 | 알림요청은 경보 ID, 등급, 설비, 발생시각, 요약, 수신자 및 이동 Link를 포함해야 한다. | P0 | I/T |
| IR-ALR-002 | 알림서비스는 전달요청, 성공, 실패, 재시도 및 최종결과를 반환해야 한다. | P0 | T |
| IR-ALR-003 | 동일 경보의 반복알림은 등급과 미확인 시간에 따라 통제할 수 있어야 한다. | P1 | T |
| IR-ALR-004 | 알림서비스 장애 시 경보원본과 Dashboard 표시는 유지되어야 한다. | P0 | T |

## 11. IF-08 MES/CMMS 연계 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-EXT-001 | 외부 시스템 연계는 설비 Master ID Mapping을 관리해야 한다. | P1 | I/T |
| IR-EXT-002 | 작업지시와 정비결과의 생성·갱신·취소 상태를 식별해야 한다. | P1 | T |
| IR-EXT-003 | 연계실패 데이터는 재처리 가능하게 보존하고 중복작업 생성을 방지해야 한다. | P1 | T |
| IR-EXT-004 | 외부 시스템이 제공하지 않는 필수정보는 `Unknown`과 같은 명시적 상태로 관리해야 한다. | P1 | T |

## 12. IF-09 인증·권한 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-ID-001 | 사용자 및 Service API 인증은 만료시간이 있는 Token 또는 동등한 안전한 Mechanism을 사용해야 한다. | P0 | I/T |
| IR-ID-002 | 장치인증 정보와 사용자 인증정보는 서로 분리하여 관리해야 한다. | P0 | I/T |
| IR-ID-003 | Role, 설비범위 및 수행기능을 이용한 권한검사를 각 보호 API에 적용해야 한다. | P0 | T |
| IR-ID-004 | 인증·권한 실패는 감사로그에 기록하되 비밀번호·Token 원문을 남기지 않아야 한다. | P0 | I/T |

## 13. IF-10 Monitoring/Logging 요구사항

| ID | 요구사항 | 우선순위 | 검증 |
|---|---|---:|---:|
| IR-MON-001 | 핵심 서비스는 Ready, Alive, Version 및 주요 Dependency 상태를 제공해야 한다. | P0 | T/D |
| IR-MON-002 | Metric은 처리량, 오류율, 지연시간, Queue, Storage와 자원사용량을 포함해야 한다. | P0 | I/D |
| IR-MON-003 | Log는 Timestamp, Service, Severity, Correlation ID와 Message를 포함해야 한다. | P0 | I |
| IR-MON-004 | 센서 메시지에서 경보까지 동일 Correlation ID 또는 추적정보로 연결 가능해야 한다. | P1 | I/T |

## 14. 인터페이스 검토 체크리스트

- [ ] 송신자, 수신자, 데이터와 책임경계가 명확한가?
- [ ] 메시지 ID, Schema Version, Event Time 및 품질상태가 포함되는가?
- [ ] 인증·암호화·권한과 오류처리가 정의되는가?
- [ ] 재전송, 중복, 지연, 순서역전과 장애복구를 고려하는가?
- [ ] 특정 OSS에 과도하게 종속되지 않고 후보비교가 가능한가?
- [ ] AI 모델입력·출력과 버전추적 요구가 충분한가?

