# 포스트 작성 가이드

## 이미지 삽입

```markdown
![alt 텍스트](/assets/img/포스트슬러그/image.jpg)
```

**스타일 클래스:**

| 클래스 | 효과 |
|---|---|
| `{:.lead}` | 전체 너비 큰 이미지 |
| `{:.tail}` | 여백 없이 꽉 채움 |
| `{:width="400"}` | 너비 지정 (px) |

**캡션:**
```markdown
![alt](/assets/img/foo.jpg)
이미지 설명 텍스트.
{:.figcaption}
```

**주의:** 이미지 파일 반드시 git commit에 포함. 누락 시 배포 후 미표시.  
권장 경로: `assets/img/<포스트슬러그>/image.jpg`

---

## 2열 레이아웃

`_sass/my-style.scss`에 `.two-col` 클래스 등록됨. 바로 사용 가능.

```html
<div class="two-col" markdown="1">
<div markdown="1">

왼쪽 내용 **(마크다운, 코드블록 모두 가능)**

</div>
<div markdown="1">

오른쪽 내용

</div>
</div>
```

**주의사항:**
- `markdown="1"` 속성 필수 — 없으면 div 안 마크다운 렌더링 안 됨
- `<div markdown="1">` 와 내용 사이 빈 줄 필요
- 모바일(640px 이하)에서 자동으로 1열로 전환

**응용 — 코드블록 2열 비교:**
```html
<div class="two-col" markdown="1">
<div markdown="1">

**Before**
```python
# 기존 코드
```

</div>
<div markdown="1">

**After**
```python
# 개선 코드
```

</div>
</div>
```

---

## 텍스트 강조 클래스 (Hydejack 전용)

```markdown
중요한 텍스트.
{:.lead}

노트 박스 텍스트.
{:.note}

경고 박스 텍스트.
{:.note title="Warning"}
```
