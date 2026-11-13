<h1 align="center">🧩 Off The Record Wiki</h1>
<p align="center">생각을 코드로 정리하는 백엔드 개발자입니다.</p>
<p align="center">"왜 이렇게 동작하는가"를 직접 구현해보며 이해하고,<br>
부분이 아닌 전체 시스템의 상호작용 관점에서 문제를 바라봅니다.</p>

<p align="center">
  <img alt="Java" src="https://img.shields.io/badge/Java-E76F00?style=flat-square&amp;logo=openjdk&amp;logoColor=white" />
  <img alt="Kotlin" src="https://img.shields.io/badge/Kotlin-7F52FF?style=flat-square&amp;logo=kotlin&amp;logoColor=white" />
</p>
<p align="center">
  <img alt="Spring" src="https://img.shields.io/badge/Spring-43852D?style=flat-square&amp;logo=spring&amp;logoColor=white" />
  <img alt="Spring Security" src="https://img.shields.io/badge/Spring%20Security-43852D?style=flat-square&amp;logo=springsecurity&amp;logoColor=white" />
  <img alt="Spring Data JPA" src="https://img.shields.io/badge/Spring%20Data%20JPA-43852D?style=flat-square&amp;logo=spring&amp;logoColor=white" />
  <img alt="Spring Batch" src="https://img.shields.io/badge/Spring%20Batch-43852D?style=flat-square&amp;logo=spring&amp;logoColor=white" />
  <img alt="JUnit" src="https://img.shields.io/badge/JUnit-25A162?style=flat-square&amp;logo=junit5&amp;logoColor=white" />
</p>
<p align="center">
  <img alt="Kafka" src="https://img.shields.io/badge/Kafka-231F20?style=flat-square&amp;logo=apachekafka&amp;logoColor=white" />
</p>
<p align="center">
  <img alt="MySQL" src="https://img.shields.io/badge/MySQL-4479A1?style=flat-square&amp;logo=mysql&amp;logoColor=white" />
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&amp;logo=postgresql&amp;logoColor=white" />
  <img alt="Redis" src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&amp;logo=redis&amp;logoColor=white" />
  <img alt="OpenSearch" src="https://img.shields.io/badge/OpenSearch-005EB8?style=flat-square&amp;logo=opensearch&amp;logoColor=white" />
</p>
<p align="center">
  <img alt="AWS" src="https://img.shields.io/badge/AWS-232F3E?style=flat-square" />
  <img alt="AWS CDK" src="https://img.shields.io/badge/AWS%20CDK-232F3E?style=flat-square" />
  <img alt="Terraform" src="https://img.shields.io/badge/Terraform-844FBA?style=flat-square&amp;logo=terraform&amp;logoColor=white" />
  <img alt="Docker" src="https://img.shields.io/badge/Docker-086DD7?style=flat-square&amp;logo=docker&amp;logoColor=white" />
  <img alt="Kubernetes" src="https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&amp;logo=kubernetes&amp;logoColor=white" />
</p>
<p align="center">
  <img alt="GitHub Actions" src="https://img.shields.io/badge/GitHub%20Actions-2455A4?style=flat-square&amp;logo=githubactions&amp;logoColor=white" />
</p>


## 🏗️ Projects

### [coupon-system-design](https://github.com/thought-corner/coupon-system-design/releases/tag/v1.0.0) - 선착순 한정 쿠폰 발급·사용

> **"1만 장 한정 쿠폰에 오픈 1초 만에 사람이 몰리면, 더 나가거나 두 번 나가지 않으면서 누구에게 무엇을 기다리게 할까"라는 질문에서 출발했습니다.**
> **동기 방식에서 비동기 방식으로 설계를 점진적으로 변화해나가면서 설계한 아키텍처가 무엇을 얻고 무엇을 내줬는지 클라우드에 배포해서 같은 환경·같은 부하에서 비교했습니다.**
- **응답 지연** - 동기 방식은 초당 1만 요청에서 **p95·p99 모두 10초 초과(응답의 69%가 타임아웃)**. Kafka로 바꾼 뒤 **p95 359ms / p99 392ms**, 동시 약 2만 요청에서도 **10초 안에 결과를 못 받은 사용자 85% → 0%**
- **처리량** - 동시 약 2만 요청에서 응답 처리량 **초당 1,484건 → 3,551건**, 초당 1만 요청에서 **903건 → 6,681건**
- **정합성** - 접수와 확정을 나눈 뒤에도 **10회 측정 모두 초과 발급·중복 발급 0건**. 같은 요청이 다시 와도 한 번만 반영되게 요청마다 고유 번호를 붙여 처리

### [bbs-system-design](https://github.com/thought-corner/bbs-system-design/releases/tag/v1.1.0) - 대규모 트래픽 게시판

> **"트래픽이 몰리는 B2C 서비스를 가정해 무엇이 먼저 무너질까"라는 질문에서 출발해, 상세 조회 초당 10만 건·게시글 10억 건을 전제로 게시판을 설계했습니다**
> **샤드 키를 벗어나지 않는 쿼리, 쓰기와 분리한 CQRS 읽기 모델, 멱등 이벤트 소비로 설계하고, 그 설계가 실제 부하에서도 맞는지 AWS에 올려 1,000만 건 규모로 검증했습니다.**
- 게시글·댓글·좋아요 각 1,000만 건에서 **상세 조회 초당 4,000건, 실패 0건, p99 22ms, 읽기 모델 적중률 99.8% 달성**
- 쓰기 초당 800건에서 **이벤트 발행 초당 75건 → 240건, outbox 적체 19,164건 → 6건, 읽기 모델 반영 지연 p95 30초 이상 → 27ms** - Snowflake ID 하위 비트 문제로 모든 이벤트를 쓰레드 하나로 보내던 결함을 해시 분산과 비동기 전송으로 해결
- 쓰기 **28만 건 뒤 표본 1,000개의 원본·읽기 모델 불일치 0건 달성**
- 한 글에 좋아요·조회 **각 2만 건을 동시에 몰아도 유실·중복 0건 달성**

### [oms-system-design](https://github.com/thought-corner/oms-system-design/releases/tag/v2.0.0) - 주문 도메인 MSA 분산 트랜잭션(Saga Orchestration Based Kafka + Outbox)

> **커피 주문 앱에서 결제가 여러 번 빠져나가고, 고객센터에 문의한 뒤에야 한참 늦게 환불된 경험에서 시작했습니다.**
> **주문·재고·포인트·결제 4개 서비스의 Saga를 동기 HTTP로 먼저 만들고, 결제 3초 동안 스레드가 묶이고 참여자가 잠깐만 죽어도 결제가 실패하는 한계를 Kafka + Outbox로 바꿔 풀었습니다.**
- 메시지 재수신·잘못된 메시지·브로커 한 대 다운·승인 대기 중 취소 등 **장애 13가지를 일으켜 확인** - 메시지 순서가 아니라 사가별 잠금 한 행으로 정방향과 취소를 줄 세워 **중복 결제 0건, "실패 + 결제됨" 주문 0건 달성**
- 목표 부하에서 결제가 밀리는 원인을 **트랜잭션 안의 승인 대기**로 찾아 밖으로 옮기고 파티션을 거꾸로 계산해 늘려, **완료 중앙값 48.5초 → 5.6초, 멈춤 감지 재발행 137회 → 0회, 720건 모두 재고·포인트 차감과 결제가 주문당 한 번씩만 반영**

### [oms-system-design](https://github.com/thought-corner/oms-system-design/releases/tag/v1.0.0) - 주문 도메인 MSA 분산 트랜잭션(Saga Orchestration Based HTTP 통신)

> **커피 주문 앱에서 결제가 여러 번 빠져나가고, 고객센터에 문의한 뒤에야 한참 늦게 환불된 경험에서 시작했습니다.**
> **주문·재고·포인트·결제를 4개의 서비스로 나눴을 때, 어디서 실패하든 돈과 재고가 정확히 맞게 끝나도록 Saga를 설계하고 장애를 직접 일으켜 검증했습니다.**
- 재고 부족, 결제 서버 다운·무응답, 주문 서버 강제 종료, 같은 주문 동시 결제 등 **실패 상황 8가지를 실제로 일으켜 판정 43개 전부 통과 — 중복 결제·중복 차감 0건, 처리 중에 멈춘 주문 0건**
- 재고·잔액 부족은 요청 안에서 **0.2초 안에 되돌리고**, 서버 장애는 복구 작업이 **64~79초 안에 환불 또는 결제 완료로 마무리** — 이 시간이 코드가 아니라 복구 규칙(대기 60초 + 점검 주기 10초)에서 정해진다는 것까지 계산으로 확인
- 응답이 늦어 포기한 결제가 환불 처리보다 늦게 도착하면 자동으로 거절해, 환불된 주문에 돈이 다시 빠져나가지 않도록 차단
- 돈과 재고는 정확히 정리됐지만 사용자에게는 결제 실패로 보이는 사례 1건을 발견해 한계로 기록

### [order-system](https://github.com/thought-corner/order-system) - 비동기 주문 시스템(RabbitMQ)

> **주문 API가 메시지 발행 즉시 응답하고, 컨슈머가 재고 차감·주문 생성을 처리하는 구조입니다.**
- MySQL Named Lock(주문 단위) + JPA 비관적 락(재고 단위) 이중 락으로 동시성 제어
- **k6 부하 테스트: 4,000 VUs에서 TPS 2.23k, 실패 0건, 재고 정합성 오차 0** 실측 기록
- Dead Letter Queue + 재발행으로 실패 메시지 유실 방지, prefetch·컨슈머 수 튜닝 과정 문서화

### [query-performance](https://github.com/thought-corner/query-performance) - 대용량 조회 성능 개선(SQL 튜닝 → Redis 캐싱을 통한 단계적 개선)

> **30만 건 데이터에서 풀 테이블 스캔으로 최대 14초 걸리던 필터링 조회를 단계적으로 개선했습니다.**
- EXPLAIN으로 풀 테이블 스캔(type: ALL) 확인 → 가격 인덱스 적용으로 조회 시간**70.5% 단축**(1s → 0.295s)
- **인덱스를 생성했는데도 동작하지 않던 원인 분석** — 낮은 카디널리티(LocalDate 일 단위 저장 + 중복도 높은 더미 데이터)로 옵티마이저가 인덱스를 버리는 상황을 규명하고, 타입·데이터 분포를 바로잡아 **82.25% 단축** (2s → 0.355s)
- 시스템 변경 없는 SQL 튜닝을 먼저, 그 위에 Redis Cache-Aside를 얹어 **추가 45.7% 개선**(1.01s → 0.548s) — 캐시-DB 정합성 한계까지 문서화

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github-stats-extended.vercel.app/api?username=dnwls16071&show_icons=true&include_all_commits=true&rank_icon=github&hide_border=true&theme=github_dark">
  <img src="https://github-stats-extended.vercel.app/api?username=dnwls16071&show_icons=true&include_all_commits=true&rank_icon=github&hide_border=true&theme=default" alt="Jang Woo's GitHub stats">
</picture>
