---
name: blog-feature-add
description: Use when adding new features (search, comments, analytics, dark mode, etc.) to the HKLeeeee.github.io Hydejack blog — requires web research for Hydejack compatibility before any implementation.
---

# Blog Feature Add

## Overview

HKLeeeee.github.io (Hydejack 9.2.1 + Jekyll 4.3) 블로그에 기능 추가.  
**반드시 웹 조사 먼저, 구현은 그 다음.**

## 실행 순서

1. **웹 조사** — Hydejack 공식 문서 + 커뮤니티에서 호환 방법 확인
2. **wiki 확인** — `wiki/` 디렉토리에 기존 관련 내용 있는지 확인
3. **구현 계획 제시** — 사용자 확인 후 진행
4. **구현**
5. **로컬 테스트** — `bundle exec jekyll serve`로 동작 확인
6. **wiki 업데이트** — 구현 방법, 설정 경로, 트러블슈팅 기록
7. **커밋 & 푸시**

## 조사 대상 소스 (우선순위 순)

1. `https://hydejack.com/docs/` — 공식 문서
2. `https://hydejack.com/blog/` — 공식 블로그 (버전별 변경사항)
3. GitHub: `hydecorp/hydejack-starter-kit` v9 브랜치
4. Jekyll 공식 문서 + 커뮤니티

## 커스텀 파일 위치

| 파일 | 용도 |
|---|---|
| `_includes/my-head.html` | `<head>` 커스텀 태그 (스크립트, 메타태그) |
| `_includes/my-body.html` | `<body>` 끝 커스텀 태그 (서드파티 스크립트) |
| `_sass/my-style.scss` | 커스텀 CSS |
| `_sass/my-inline.scss` | 인라인 critical CSS |
| `_layouts/` | 레이아웃 오버라이드 |
| `_config.yml` | 플러그인, 테마 설정 |

Hydejack은 이 파일들을 override point로 제공. 테마 파일 직접 수정 금지 (업그레이드 시 덮어씌워짐).

## 기능별 구현 가이드

### 댓글 (giscus 권장)
- GitHub Discussions 기반, 무료, 한국어 지원
- `_includes/my-body.html`에 스크립트 삽입
- `https://giscus.app`에서 설정 생성

### 댓글 (utterances)
- GitHub Issues 기반
- `_includes/my-body.html`에 스크립트 삽입

### 검색
- `simple-jekyll-search` (npm) 이미 설치됨 (`node_modules/`)
- `_layouts/search.html` 커스텀 레이아웃 존재
- `assets/` 에 `search.json` 인덱스 파일 필요

### Analytics
- Google Analytics: `_config.yml`의 `google_analytics:` 키
- 기타: `_includes/my-head.html`에 스크립트 삽입

### 파비콘
- `assets/icons/` 디렉토리에 파일 배치
- `_includes/my-head.html`에 link 태그

## 주의사항

- `jekyll-theme-hydejack` gem 내부 파일 직접 수정 금지
- 새 Jekyll 플러그인 추가 시 `Gemfile` + `_config.yml` plugins 모두 추가
- `Gemfile.lock` 변경 후 `bundle lock --add-platform x86_64-linux` 실행 필수 (GitHub Actions Linux 빌드용)
