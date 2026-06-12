# 블로그 운영 정책

## 카테고리 구조

| 카테고리 | 디렉토리 | 내용 |
|---|---|---|
| SQLTuning | `_posts/친절한SQL튜닝/` | "친절한 SQL 튜닝" 책 스터디 |
| Computer | `_posts/computer/` | 컴퓨터 일반 |
| AI | `_posts/AI/` | AI 관련 |

## 포스트 작성 워크플로우

1. `bundle exec jekyll post "제목"` 으로 초안 생성 (로컬)
2. front matter 작성 — `# ---` 주의, 반드시 `---` 시작
3. `bundle exec jekyll serve`로 로컬 확인 (http://localhost:4000)
4. `git add`, `git commit`, `git push` → 자동 배포

## 로컬 vs 배포 차이

| 항목 | 로컬 | GitHub Pages |
|---|---|---|
| Jekyll 버전 | 4.x | 3.10.0 (기본 빌드) |
| KaTeX 수식 | 동작 | 동작 안 함 |
| jekyll-last-modified-at | 동작 | 빌드 실패 |
| 미래 날짜 포스트 | 표시됨 | 표시 안 됨 |

→ GitHub Actions 빌드 전환 시 로컬과 동일 환경 가능 (wiki/github-pages-hosting.md 참고)

## TODO

- [x] GitHub Actions 빌드 전환 (`.github/workflows/jekyll.yml` 생성 완료)
- [ ] 사이드바 이미지 변경 (`assets/img/sidebar.jpg` 준비됨)
- [ ] 댓글 기능 (utterances 또는 giscus 추천)
- [ ] 파비콘 설정
- [ ] Light/Dark 모드
