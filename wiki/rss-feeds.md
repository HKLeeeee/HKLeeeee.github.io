# 한국 개발 기술 블로그 RSS 피드 목록

dev-trend 포스트 작성에 사용하는 RSS 피드 모음. 유효성은 2026-06-13 기준 검증.

## 유효한 피드

| 이름 | RSS 주소 | 비고 |
|---|---|---|
| 무신사 기술블로그 | https://medium.com/feed/musinsa-tech | 활성 |
| 우아한형제들 기술블로그 | https://techblog.woowahan.com/feed | 활성 |
| LINE(LY Corporation) 기술블로그 | https://techblog.lycorp.co.jp/ko/feed/index.xml | 원래 주소 301 리다이렉트됨 |
| 쿠팡 기술블로그 | https://medium.com/feed/coupang-engineering | 활성 (게시 빈도 낮음) |
| 당근마켓 기술블로그 | https://medium.com/feed/daangn | 활성 |
| 토스 기술블로그 | https://toss.tech/rss.xml | 활성, 게시 빈도 높음 |
| 왓챠 기술블로그 | https://medium.com/feed/watcha | 활성 (게시 빈도 낮음) |
| 뱅크샐러드 기술블로그 | https://blog.banksalad.com/rss.xml | 활성 (최신 2026-04) |
| Hyperconnect 기술블로그 | https://hyperconnect.github.io/feed.xml | 활성 (최신 2026-04) |
| 요기요 기술블로그 | https://techblog.yogiyo.co.kr/feed | 활성 (최신 2026-04) |
| 쏘카 기술블로그 | https://tech.socarcorp.kr/feed | 활성 (최신 2026-02) |
| 리디 기술블로그 | https://www.ridicorp.com/feed | 활성, 기술/마케팅 혼재 |
| NHN Cloud 기술블로그 | https://meetup.nhncloud.com/rss | 활성 |
| GeekNews | https://news.hada.io/rss/news | 매우 활성, 큐레이션 뉴스 |
| 개발자스럽다 | https://feeds.feedburner.com/gaeraeblog | 유효 (최신 2026-03), 원래 주소 리다이렉트 |
| 44BITS | https://www.44bits.io/ko/feed/all | 유효 (최신 2026-01) |
| 카카오엔터프라이즈 기술블로그 | https://tech.kakaoenterprise.com/feed | 유효하나 2023 이후 비활성 |
| 데브시스터즈 기술블로그 | https://tech.devsisters.com/rss.xml | 유효하나 게시 빈도 매우 낮음 |
| 직방 기술블로그 | https://medium.com/feed/zigbang | 유효하나 2023 이후 비활성 |

## 접근 불가 피드

| 이름 | 원래 RSS 주소 | 상태 |
|---|---|---|
| 네이버 D2 기술블로그 | https://d2.naver.com/d2.atom | Claude WebFetch 접근 차단 |
| 마켓컬리 기술블로그 | https://helloworld.kurly.com/feed.xml | HTTP 403 Forbidden |

## 제외 피드

| 이름 | RSS 주소 | 제외 이유 |
|---|---|---|
| Velog 전체 | https://v2.velog.io/rss/ | 전체 RSS는 스팸 게시물 다수, 특정 블로거 개별 RSS 사용 권장 |

## 리다이렉트 주의

- `engineering.linecorp.com/ko/feed/index.html` → `techblog.lycorp.co.jp/ko/feed/index.xml` (301)
- `blog.gaerae.com/feeds/posts/default?alt=rss` → `feeds.feedburner.com/gaeraeblog` (302)

## dev-trend 포스트 작성 프로세스

1. 각 RSS 피드에서 최근 1주일 글 수집
2. 기술 트렌드 중심으로 분류 (AI/ML, 인프라, 프론트엔드, 백엔드 등)
3. `_posts/dev-trend/YYYY-MM-DD-weekly-dev-trend-YYYY-wWW.md` 형식으로 저장
4. 카테고리: `dev-trend`
