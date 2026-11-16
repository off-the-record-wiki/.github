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
