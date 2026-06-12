# GitHub Pages 호스팅 가이드

## 핵심 제약사항

### Jekyll 버전
GitHub Pages는 **Jekyll 3.10.0만** 지원. `Gemfile`에 `jekyll ~> 4.1` 지정해도 로컬만 4.x, GitHub Pages 빌드는 3.10.0 강제 적용.

Jekyll 4.x 기능(예: `link` 태그 변경, Sass 업그레이드) 사용 시 GitHub Pages 빌드 실패.

### 지원 플러그인 (화이트리스트)
GitHub Pages는 `--safe` 모드로 빌드. 아래 목록 외 플러그인은 **빌드 오류** 발생.

| 플러그인 | 지원 여부 |
|---|---|
| jekyll-feed | ✅ |
| jekyll-paginate | ✅ |
| jekyll-redirect-from | ✅ |
| jekyll-relative-links | ✅ |
| jekyll-seo-tag | ✅ |
| jekyll-sitemap | ✅ |
| jekyll-default-layout | ✅ |
| jekyll-optional-front-matter | ✅ |
| jekyll-readme-index | ✅ |
| jekyll-titles-from-headings | ✅ |
| jekyll-include-cache | ✅ |
| **jekyll-last-modified-at** | ❌ 비지원 |
| **kramdown-math-katex** | ❌ 비지원 |
| **jekyll-compose** | ❌ 비지원 (로컬 전용) |

전체 목록: https://pages.github.com/versions/

### 강제 설정값
GitHub Pages가 덮어쓰는 `_config.yml` 값들:

```yaml
lsi: false
safe: true
source: [repo 루트]
incremental: false
highlighter: rouge   # 변경 불가
```

---

## 이 블로그의 현재 문제 및 해결방안

### 문제 진단
로컬에서 보이지만 `https://hkleeeee.github.io`에서 안 보이는 원인:

1. **`jekyll-last-modified-at`** — `_config.yml` plugins에 등록 → 빌드 실패
2. **Jekyll 4.x** — Gemfile에 `~> 4.1` 명시 → GitHub Pages 빌드 실패
3. **`kramdown-math-katex`** — KaTeX 수식 렌더링 비지원
4. **`2ch.md` front matter 오류** — `# ---`로 시작 (주석 처리됨)

빌드 실패 시 GitHub Pages는 이전 성공 빌드를 유지하므로 새 포스트가 반영 안 됨.

### 해결 방법 (2가지 선택지)

#### 옵션 A: GitHub Actions로 직접 빌드 배포 (권장)
Jekyll 4.x, 비지원 플러그인 모두 사용 가능. KaTeX도 동작.

`.github/workflows/jekyll.yml` 생성:

```yaml
name: Deploy Jekyll site to Pages

on:
  push:
    branches: ["main"]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ruby/setup-ruby@v1
        with:
          ruby-version: '3.1'
          bundler-cache: true
      - run: bundle exec jekyll build
        env:
          JEKYLL_ENV: production
      - uses: actions/upload-pages-artifact@v3

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

GitHub 저장소 설정: Settings → Pages → Source → **GitHub Actions** 선택.

#### 옵션 B: GitHub Pages 기본 빌드 유지
`_config.yml`과 `Gemfile`에서 비지원 플러그인 제거.

```yaml
# _config.yml plugins에서 제거:
# - jekyll-last-modified-at
```

```ruby
# Gemfile에서 제거:
# gem "kramdown-math-katex"
# gem "duktape"
# gem "jekyll-compose"  # (로컬 개발용이라면 :development group으로 이동)
```

---

## Post 작성 규칙

### Front Matter 형식
반드시 `---`로 시작 (주석 `#` 없이):

```yaml
---
layout: post
title: 제목
description: >
  설명 (~160자)
sitemap: true
categories: 카테고리명
tags: [태그1, 태그2]
---
```

### 파일명 규칙
`YYYY-MM-DD-slug.md` — 미래 날짜면 기본적으로 발행 안 됨.  
미래 날짜 포스트 발행하려면 `_config.yml`에 `future: true` 추가.

### `_posts` 하위 디렉토리
Jekyll은 `_posts/` 하위 폴더도 탐색함. 한글 폴더명도 동작.  
카테고리는 폴더 구조가 아닌 front matter `categories:`로 결정됨.

---

## 빌드 확인 방법

GitHub 빌드 오류 확인: 저장소 → **Actions** 탭 (GitHub Actions 사용 시) 또는 Settings → Pages에서 빌드 상태 확인.

빌드 실패 시 등록된 이메일로 알림 발송됨.
