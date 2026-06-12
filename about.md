---
layout: about
title: About Me
description: >
  배움에 이유를 찾고, 코드로 이야기하며, 자동화를 좋아하는 개발자 이희경입니다.
hide_description: true
---

# 개발자 이희경

<div class="two-col" markdown="1">
<div markdown="1">

**Heekyoung Lee**
{:.lead}

배움에 이유를 찾고, 코드로 이야기하며, 자동화를 좋아하는 개발자.  
웹 개발과 인공지능에 관심을 가지고 있으며, 기술로 사회에 긍정적인 임팩트를 만드는 것을 목표로 합니다.

</div>
<div markdown="1">

<img class="round-img" src="https://avatars.githubusercontent.com/u/84272873?v=4">

</div>
</div>

---

## 🛠️ Skills

**Languages**
`Java` `Python` `JavaScript`

**Database**
`MySQL` `Oracle` `Redis` `MongoDB`

**Libraries / Framework**
`Spring` `NestJS` `Express` `Flask` `TensorFlow` `PyTorch` `TensorRT`

**Others**
`Git` `Docker` `AWS` `Wandb`

---

## 💼 경력

**Samsung Electronics** _(2024.10 ~)_

- SW개발 / MES팀

**Ecube Labs** _(2024.04 ~ 2024.06)_

- Full-stack Engineer / SW팀
  - 솔루션 내 인공지능 적용 PoC
  - 쓰레기통 내부 특정 물품 판단 모델, RAG 활용 사내 챗봇
  - MLOps 도입 전략 조사 (Airflow, MLflow)

**Human ICT 기술연구소** _(2022.11 ~ 2023.06)_

- 매니저 / AI모델연구개발팀
  - Vision AI 활용 솔루션 개발
  - cctv 상 영상 내 높은 곳에서 낙하하는 사람과 정지하여 움직이지 않는 사람 감지
    - yolov7(Object Detection), SORT(Multi-Object Tracking Algorithm), Lucas-Kanade(Optical Flow) 활용
    - Python, Pytroch, Onnx, TensorRT
  - SORT 알고리즘과 Optical FLow를 활용하여 감지된 사람 객체의 움직임을 파악하고 이벤트 발생

---

## 👩‍💼 Projects

### 🐳 AlgoITNi — 협동 알고리즘 학습 플랫폼

**2023.11 ~ 2023.12 (6주)** | Web · BE · Team Project (BE 2, FE 2)  
[GitHub](https://github.com/boostcampwm2023/web05-AlgoITNi)

화상·음성·채팅으로 동료와 함께 알고리즘 문제를 풀 수 있는 플랫폼.

`NestJS` `TypeScript` `Socket.IO` `MongoDB` `MySQL` `Redis` `Docker` `GitHub Actions` `Nginx`

- Socket + Message Queue + Pub/Sub 도입으로 CPU 사용률 43%, Memory 21% 감소
- Blue-Green 무중단 배포 구현
- OAuth2.0 + JWT 쿠키 기반 인증/인가
- 커스텀 데코레이터 + AsyncLocalStorage 트랜잭션 관심사 분리
- [**네이버클라우드 클로바 스튜디오 포럼 우수 사례 선정**](https://www.ncloud-forums.com/topic/213/)

---

### 🚌 버스어디 - 버스 도착 정보 앱

[GitHub](https://github.com/Pepsi-Club/WhereMyBus-BE) [🍎 Store](https://apps.apple.com/us/app/%EC%A0%84%EA%B5%AD-%EC%8A%A4%EB%A7%88%ED%8A%B8-%EB%B2%84%EC%8A%A4-%EC%8B%A4%EC%8B%9C%EA%B0%84-%EB%8F%84%EC%B0%A9%EC%8B%9C%EA%B0%84-%EC%9C%84%EC%B9%98-%EC%A3%BC%EB%B3%80%EC%9E%A5%EC%86%8C/id884947832?l=ko)

서울 안 어디서나,버스어디로 간편하게 ! 버스 즐겨찾기와 정기알람으로 버스 사용을 더 간편하게 ! 쉬운 사용성과 편리함을 갖춘 버스어디를 지금 만나보세요.

`NestJS` `TypeScript` `MongoDB` `PM2` `FCM(Firebase Cloud Messaging)` `GitHub Actions` `Nginx`

<div class="two-col-without-gap">
  <div><img class="round-img" src="https://is1-ssl.mzstatic.com/image/thumb/PurpleSource221/v4/19/bd/67/19bd6771-dbc3-7d68-2b50-817394e7ccde/6a1c816c-bab7-4f9b-929f-be5129a31cdb_appstore_screen.jpg/230x498bb.webp"></div>
  <div><img class="round-img" src="https://is1-ssl.mzstatic.com/image/thumb/PurpleSource221/v4/5b/76/97/5b769755-90f3-5ee9-6b21-3f8251a3dc33/fdc9ae75-214c-4be9-a1ec-a4da27b20a91_appstore_screen02.jpg/230x498bb.webp"></div>
</div>

---

### 📱 Teengle — 10대 커뮤니티 앱

**2024.01 ~ 2024.03** | Web · BE · Team Project (BE 2, FE 2, 디자인 1, 기획 1)

10대들이 자유롭게 소통할 수 있는 모바일 커뮤니티 앱.

`Java` `Spring Boot` `QueryDSL` `JPA` `MongoDB` `MySQL` `Redis` `Docker` `AWS` `GitHub Actions` `React Native`

- 해커스 뉴스 랭킹 알고리즘 기반 인기글 정렬
- Cursor Based Pagination 도입으로 데이터 유실 감소
- Bulk Update 적용으로 처리 속도 약 77% 감소
- Logback 기반 서버 로그 모니터링

---

### 🚗 상습 침수지역 모니터링 및 위험 정보 제공 서비스

**2022.09 ~ 2022.12** | AI · Team Project (AI 1, BE 2, FE 1)  
[GitHub](https://github.com/CSID-DGU/2022-2-SCS4031-9to6)

공공 CCTV에 적용 가능한 딥러닝 기반 침수 탐지 모델을 개발하여 실시간 위험 정보를 제공하는 웹 서비스.

`Python` `Flask` `PyTorch` `TensorFlow` `Celery` `Redis` `Docker` `AWS EC2/S3/RDS` `React` `MySQL`

- 전이학습 + 가중치 튜닝으로 객체 탐지 모델 성능 50% 이상 개선
- Celery + Redis 메시지 브로커 큐 활용 비동기 모델 API 구현
- Wandb 도입으로 학습 과정 관리 및 시각화
- **소프트웨어 등록 (C-2023-011779) · 특허 출원 (10-2023-0070846)**

---

### 🐿️ 생태통로 효율성 추정 및 주요 요인 분석

**2022** | Data Analysis · Team Project (6인)  
[GitHub](https://github.com/TeamHKL/datacampus_dao)

생태통로 효율성에 영향을 미치는 요인 데이터 수집 및 분석.

`Python` `Selenium` `BeautifulSoup` `QGIS` `MySQL` `AWS RDS` `pycaret` `scikit-learn` `pandas`

- 웹 크롤링 + GIS 데이터 전처리
- pycaret 기반 머신러닝 분석 파이프라인 구현

---

## 💬 특허

**상습 침수지역 모니터링 및 위험 정보 제공 방법 및 이를 수행하기 위한 기록매체**  
출원번호: 10-2023-0070846 | 출원일자: 2023.06.01  
역할: 침수 탐지 AI 모델 개발 및 배포, 공동발명자, 팀장

---

## ❓ 대외활동 및 교육

| 기간              | 활동                                                                                    |
| ----------------- | --------------------------------------------------------------------------------------- |
| 2023.07 ~ 2023.12 | 네이버 부스트캠프 웹・모바일 8기 (JavaScript/TypeScript)                                |
| 2022.06 ~ 2022.08 | 데이터청년캠퍼스 — 데이터사이언스 기반 지능소프트웨어 과정, 한국데이터산업진흥원 (350h) |
| 2022.01 ~ 2022.06 | K-digital Training AI 서비스 개발 — 멀티캠퍼스 (880h)                                   |
| 2021.05 ~ 2021.09 | 동국대학교 Farm — 소프트웨어융합 기술 동아리                                            |
| 2020.01 ~ 2020.05 | 교환학생 — Brno University of Technology (체코), Faculty of IT                          |

---

<!--posts-->
