---
layout: post
title: "Weekly Dev Trend — 2026년 24주차 (6/7~6/13)"
description: >
  토스 AI Agent Skill 품질 프레임워크, 당근마켓 디자인시스템 진화, LINE AX 로드맵, NHN Cloud 관리형 Kafka. 이번 주 한국 기술 블로그 요약.
sitemap: true
categories: dev-trend
tags: [weekly, ai, design-system, kafka, infra]
---

한국 주요 기술 블로그 RSS 피드 기반 주간 트렌드 요약 (2026-06-07 ~ 2026-06-13).

---

## AI / ML

### 토스 — AI Agent Skill 품질 관리를 위한 Rubric 설계
**[원문 →](https://toss.tech/article/skill-quality-rubric)** (2026-06-08)

내부 AI Agent 툴의 품질을 측정하기 위해 6개 항목·30개 체크리스트로 구성된 Rubric을 설계하고 시스템화한 과정.
결정론적 규칙 기반 검사(deterministic rule-based)와 시맨틱 모델 기반 검증(semantic model-based)을 분리한 점이 핵심.

> 체크리스트만 있으면 "됐다/안됐다"를 알 수 있지만, Rubric이 있어야 "얼마나 잘 됐는지"를 알 수 있다.

### 토스 — 얼굴 인식 60년 역사와 페이스페이
**[원문 →](https://toss.tech/article/history-of-face-recognition-facepay)** (2026-06-09)

수동 특징 매핑에서 딥러닝까지 얼굴 인식 기술의 역사를 정리하고, 토스 페이스페이가 NIST 평가 세계 12위를 달성한 과정 공유.

### LINE (LY Corp) — 레거시에서 AI 드리븐 프로젝트로, AX 로드맵
**[원문 →](https://techblog.lycorp.co.jp/ko/legacy-to-ai-driven-project-ax-roadmap)** (2026-06-10)

기존 레거시 시스템을 AI 드리븐 방식으로 전환하기 위한 단계별 AX(AI Transformation) 로드맵 소개.
점진적 전환 전략과 팀 역량 변화 관리에 초점.

---

## 설계 / 조직

### 당근마켓 — 디자인시스템 팀은 디자인시스템만 잘 만들면 될까
**[원문 →](https://medium.com/daangn/디자인시스템-팀은-디자인시스템만-잘-만들면-될까-4f6f2478a8db)** (2026-06-11)

컴포넌트 라이브러리를 잘 만드는 것 이상으로, 팀이 올바른 결정을 내릴 수 있도록 돕는 역할이 필요하다는 주장.
AI 기반 컨텍스트 가이드와 구조화된 디자인 지식 제공을 통한 확장 방향 제시.

### 토스 — TAM(Technical Account Manager)의 문제 해결 방식
**[원문 →](https://toss.tech/article/tam-connect-2025)** (2026-06-09)

토스와 카카오페이 TAM이 기술과 비즈니스 사이를 잇는 방법, 빠르게 성장하는 조직에서 운영 문제를 해결하는 실제 사례 공유.

---

## 인프라 / 백엔드

### NHN Cloud — 운영하지 않는 Kafka, EasyQueue 소개
**[원문 →](https://meetup.nhncloud.com/posts/415)** (2026-06-11)

Apache Kafka 클러스터 운영을 NHN Cloud가 전담하고, 사용자는 토픽·파티션 제어만 하면 되는 완전 관리형 서비스.
웹 콘솔 기반 테스트·모니터링 기능 내장.

---

## 이번 주 트렌드 요약

| 키워드 | 내용 |
|---|---|
| **AI Agent 품질 관리** | Rubric 기반 정량 평가 체계 도입 확산 |
| **AI 전환(AX) 로드맵** | 레거시 탈출을 위한 단계적 접근법 |
| **디자인시스템 역할 확장** | 컴포넌트 제공자 → 의사결정 지원자 |
| **관리형 메시지큐** | Kafka 운영 부담 줄이는 서비스 수요 |

---

*RSS 피드 출처: 토스, 당근마켓, LINE(LY Corp), NHN Cloud 기술블로그*  
*피드 목록 전체: [wiki/rss-feeds.md](/wiki/rss-feeds)*
