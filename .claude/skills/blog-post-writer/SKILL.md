---
name: blog-post-writer
description: Use when given a markdown file to publish as a blog post — converting to hosting-ready format, placing in correct category directory, and deploying via git commit and push.
---

# Blog Post Writer

## Overview

마크다운 파일을 받아 HKLeeeee.github.io에 배포 가능한 Jekyll 포스트로 변환 후 커밋 & 푸시.

## 실행 순서

1. **파일 읽기** — 입력 마크다운 파일 내용 파악
2. **카테고리 결정** — 아래 카테고리 표 참고
3. **front matter 작성** — 아래 템플릿 사용
4. **파일 저장** — `_posts/<카테고리디렉토리>/YYYY-MM-DD-slug.md`
5. **로컬 빌드 검증** — `bundle exec jekyll build` 오류 없는지 확인
6. **커밋 & 푸시** — `git add`, `git commit`, `git push origin main`

## 카테고리 표

| 주제 | categories 값 | 저장 디렉토리 |
|---|---|---|
| SQL / DB 튜닝 | `SQLTuning` | `_posts/친절한SQL튜닝/` |
| 컴퓨터 일반 / CS | `Computer` | `_posts/computer/` |
| AI / ML | `AI` | `_posts/AI/` |
| 예시 / 테스트 | `Example` | `_posts/example/` |

카테고리 불명확하면 사용자에게 확인 후 진행.

## Front Matter 템플릿

```yaml
---
layout: post
title: <제목>
description: >
  <160자 이내 요약>
sitemap: true
categories: <카테고리>
tags: [<태그1>, <태그2>]
---
```

**주의사항:**
- 첫 줄 반드시 `---` (절대 `# ---` 아님)
- `description:` 들여쓰기 2칸
- `tags:` 배열 형식 `[태그]` 또는 단일 `태그`

## 파일명 규칙

`YYYY-MM-DD-한글-또는-영문-slug.md`

- 날짜: 오늘 날짜 (미래 날짜 사용 시 배포 후 미노출)
- slug: 영문 소문자 + 하이픈 권장, 한글도 동작

## 배포 확인

푸시 후 GitHub Actions 빌드 상태 확인:
```bash
gh run list --repo HKLeeeee/HKLeeeee.github.io --limit 1 --json status,conclusion,name --jq '.[]'
```

빌드 실패 시 `--log-failed` 옵션으로 원인 파악.

## 이미지 포함 포스트

이미지 파일은 반드시 커밋에 포함. 누락 시 배포 환경에서 미표시.
권장 경로: `assets/img/<포스트슬러그>/image.jpg`

대용량 이미지(수 MB) push 실패 시:
```bash
git config http.postBuffer 524288000
git push origin main
```
