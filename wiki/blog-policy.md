# 블로그 운영 정책

## 카테고리 구조

| 카테고리 | slug | 디렉토리 | 예정 내용 |
|---|---|---|---|
| AI | `ai` | `_posts/AI/` | AI 트렌드, 최신논문, Agentic Engineering, LLM, PyTorch, TensorRT |
| SW Engineering | `sw-engineering` | `_posts/sw-engineering/` | 디자인 패턴, 애자일, 클린코드, 개발 철학 |
| Dev Trend | `dev-trend` | `_posts/dev-trend/` | 매주 개발 트렌드 정리 (현재 빈 카테고리) |
| Infra | `infra` | `_posts/infra/` | Docker, Kubernetes, CI/CD (현재 빈 카테고리) |
| Database | `database` | `_posts/database/` | SQL 튜닝, Oracle, NoSQL, Graph DB |

### 카테고리명 대안 제안 (SW Engineering)
디자인 패턴·애자일·클린코드 성격에 맞는 후보:
- **Craftsmanship** — 소프트웨어 장인정신, 가장 의미 정확
- **Dev Practice** — 개발 실천법, 직관적
- **Engineering** — 간결하지만 범위 너무 넓음
- 현재 **SW Engineering** 유지 중 → 변경 원하면 `_featured_categories/sw-engineering.md` + `_config.yml` menu + 포스트 `categories` 3곳 수정

### 삭제된 카테고리
- `computer` — Docker(Infra), k8s(Infra), SOLID(SW Engineering)으로 분리됨
- `example`, `test` — 테마 예시 파일 삭제
- `SQLTuning` (친절한SQL튜닝) → `database`로 통합

## 포스트 작성 워크플로우

1. `bundle exec jekyll post "제목"` 으로 초안 생성 (로컬)
2. front matter 작성 — `# ---` 주의, 반드시 `---` 시작
3. `bundle exec jekyll serve`로 로컬 확인 (http://localhost:4000)
4. `git add`, `git commit`, `git push` → 자동 배포

## 이미지 설정

### 사이드바 배경 / 커버 페이지 배경
`_config.yml`:
```yaml
accent_image: /assets/img/sidebar.jpg   # 사이드바 + 최초 진입 커버 배경
```
파일을 `assets/img/sidebar.jpg`에 두고 **반드시 git commit에 포함**해야 배포에 반영됨.  
로컬에만 있고 커밋 안 하면 GitHub Actions 빌드 시 파일 없어서 이미지 미노출.

### 포스트 커버 이미지 (jekyll_compose 기본값)
`_config.yml` jekyll_compose 섹션의 `image.path: /assets/img/sidebar-bg.jpg` 는 새 포스트 생성 시 front matter 자동 입력용.  
`sidebar-bg.jpg` 파일이 없으면 해당 포스트 커버 이미지 미표시 (빌드 오류는 아님).

### 이미지 파일 push 오류 대처
바이너리 파일(이미지) push 시 HTTP 400 오류 발생할 수 있음:
```bash
git config http.postBuffer 524288000
git push origin main
```

## 로컬 vs 배포 차이

| 항목 | 로컬 | GitHub Actions (현재) |
|---|---|---|
| Jekyll 버전 | 4.3.x | 4.3.x (동일) |
| KaTeX 수식 | 동작 | 동작 |
| jekyll-last-modified-at | 동작 | 동작 |
| 미래 날짜 포스트 | 표시됨 | 표시 안 됨 |
| 미커밋 파일 | 표시됨 | **표시 안 됨** |

## About 페이지

`about.md` — 포트폴리오 용도로 활용.  
현재 기본 템플릿 작성 상태. 실제 경력/프로젝트 내용으로 채울 것.  
참고: https://vigorous-pawpaw-311.notion.site/Portfolio-e26ad5cc58704ef499ce1d587c9387f7 (Notion 페이지 — 클라이언트 렌더링이라 자동 접근 불가, 수동 업데이트 필요)

## TODO

- [x] GitHub Actions 빌드 전환 (`.github/workflows/jekyll.yml` 생성 완료)
- [x] 사이드바 이미지 (`assets/img/sidebar.jpg` 커밋 완료)
- [x] 카테고리 재편 (AI, SW Engineering, Dev Trend, Infra, Database)
- [ ] About 페이지 포트폴리오 내용 채우기 (Notion 기반)
- [x] 검색 기능 (Simple Jekyll Search, `/search/` 페이지)
- [ ] 댓글 기능 (utterances 또는 giscus 추천)
- [ ] 파비콘 설정
- [ ] Light/Dark 모드
