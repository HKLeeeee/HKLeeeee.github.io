# 검색 기능 구현

## 사용 라이브러리

**[Simple Jekyll Search](https://github.com/christian-fei/Simple-Jekyll-Search)** v1.10.0

클라이언트 사이드 검색. Jekyll 빌드 시 생성되는 `search.json`을 브라우저에서 로드하여 검색.  
별도 서버 없이 동작 (GitHub Pages 완전 지원).

---

## 검색 동작 원리

```
Jekyll 빌드 → assets/json/search.json 생성 (전체 포스트 인덱스)
               ↓
브라우저가 /search/ 진입 시 search.json fetch
               ↓
사용자 입력 → SimpleJekyllSearch가 JSON에서 title/tags/categories 매칭
               ↓
#results-container에 결과 렌더링
```

**매칭 방식:** 기본값 `fuzzy: false` → 입력 문자열 포함 여부로 검색.  
`fuzzy: true`로 바꾸면 오타 허용 퍼지 검색 (오탐 많아 비권장).

---

## 관련 파일

| 파일 | 역할 |
|---|---|
| `assets/json/search.json` | Jekyll이 빌드 시 포스트 목록을 JSON으로 생성 |
| `assets/js/simple-jekyll-search.min.js` | 검색 라이브러리 (node_modules에서 복사, 정적 서빙) |
| `_layouts/search.html` | 검색 UI + SimpleJekyllSearch 초기화 스크립트 |
| `search.md` | `/search/` 페이지 (layout: search 사용) |
| `_sass/my-style.scss` | `.search-wrap`, `#results-container` 스타일 |

---

## search.json 인덱스 구조

`assets/json/search.json`은 front matter `layout: none`을 가진 Liquid 템플릿.  
Jekyll이 처리하여 실제 JSON 파일로 출력.

인덱스에 포함된 필드: `title`, `categories`, `tags`, `date`, `url`

검색 결과 표시에 `content` 필드를 추가하면 본문 전문 검색 가능하지만, 파일 크기가 커져 로딩 느려짐.

---

## 검색 범위 조정

`_layouts/search.html`의 `SimpleJekyllSearch()` 옵션:

```js
SimpleJekyllSearch({
  searchInput: document.getElementById('search-input'),
  resultsContainer: document.getElementById('results-container'),
  json: '/assets/json/search.json',
  searchResultTemplate: '<li><a href="{url}">{title}</a><span class="search-result-meta">{date} · {categories}</span></li>',
  noResultsText: '<li class="no-results">검색 결과가 없습니다.</li>',
  limit: 30,       // 최대 결과 수
  fuzzy: false     // 정확 매칭
});
```

`searchResultTemplate`의 `{필드명}`은 `search.json`의 키와 대응.  
본문 검색 추가 시: `search.json`에 `"content": "{{ post.content | strip_html | truncate: 500 | jsonify }}"` 추가 후 템플릿에 `{content}` 추가.

---

## JS 파일 관리

`assets/js/simple-jekyll-search.min.js`는 `node_modules/simple-jekyll-search/dest/`에서 수동 복사.

버전 업그레이드 시:
```bash
npm update simple-jekyll-search
cp node_modules/simple-jekyll-search/dest/simple-jekyll-search.min.js assets/js/
git add assets/js/simple-jekyll-search.min.js
```

GitHub Actions 워크플로우에서 `npm install`을 실행하지만 Jekyll 빌드에 직접 사용하지 않음.  
→ 반드시 `assets/js/`에 파일 직접 포함해야 배포 동작.

---

## Hydejack 내장 검색과의 관계

Hydejack PRO 전용 기능이므로 Free 버전에서는 동작 안 함.  
`_config.yml`의 `no_search: false`는 PRO 검색 활성화 플래그이나 무관하게 무시됨.  
→ Simple Jekyll Search로 대체 구현.
