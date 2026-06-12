---
name: blog-wiki-writer
description: Use when accumulating or updating knowledge about this blog — Hydejack configuration, GitHub Pages operations, troubleshooting history, feature changes, or blog policy updates should all be written to wiki/.
---

# Blog Wiki Writer

## Overview

HKLeeeee.github.io 블로그 운영 지식을 `wiki/` 디렉토리에 축적.  
트러블슈팅, 설정 변경, 운영 정책 등 이 블로그에 대한 모든 정보의 단일 출처.

## wiki/ 디렉토리 구조

```
wiki/
  README.md                  # 인덱스 (전체 문서 목록)
  github-pages-hosting.md    # GitHub Pages 제약, 빌드, 배포
  blog-policy.md             # 카테고리, 워크플로우, TODO
  <새문서>.md                # 필요시 추가
```

## README.md 인덱스 유지 규칙

새 문서 추가 또는 기존 문서 변경 시 `wiki/README.md` 표 업데이트 필수:

```markdown
| [문서제목](파일명.md) | 한 줄 설명 |
```

## 기록해야 할 항목

| 상황 | 기록 위치 | 포함 내용 |
|---|---|---|
| 빌드/배포 오류 해결 | `github-pages-hosting.md` | 오류 메시지, 원인, 해결책 |
| 새 기능 추가 | 해당 기능 섹션 또는 신규 파일 | 설정 위치, 코드, 주의사항 |
| 카테고리 추가/변경 | `blog-policy.md` | 카테고리명, 디렉토리, 용도 |
| Hydejack 버전 업그레이드 | `github-pages-hosting.md` | 변경사항, 마이그레이션 노트 |
| 운영 정책 변경 | `blog-policy.md` | 정책 내용, 변경 이유 |

## 문서 작성 원칙

- **재현 가능하게**: 명령어, 파일 경로, 설정값 구체적으로 기재
- **원인 기록**: 왜 이렇게 해야 하는지 이유 포함
- **코드 블록**: 명령어와 설정값은 코드 블록으로
- **날짜 불필요**: 시간 기반 정보보다 상태 기반 정보 위주

## 웹 조사 후 기록 패턴

새 지식을 웹에서 얻은 경우:
1. 출처 URL 확인 (공식 문서 우선)
2. 이 블로그 환경(Hydejack 9.2.1, Jekyll 4.3)에 적용 가능한지 확인
3. 실제 적용 후 동작 확인된 내용만 기록
4. 미검증 정보는 "미확인" 표시

## 커밋 규칙

wiki 업데이트는 기능 구현 커밋과 분리하거나 함께 포함:
```
Update wiki: <변경 내용 한 줄 요약>
```
