---
layout: post
title: "Agentic Engineering"
description: >
  AI Agent를 잘 쓰기 위한 도구 — 입력/출력 토큰 최적화부터 멀티 에이전트 프레임워크, Claude skill과 subagent 활용법까지
sitemap: true
categories: AI
tags: [claude, agent, agentic-engineering, llm, claude-code]
---

Coding Agent 덕분에 생산성은 올랐다. 기능도 잘 돌아간다. 그런데 정작 고객에게 납품하기 어려운 제품이 만들어지는 문제가 생겼다.

- 코드를 직접 이해할 필요가 줄어들면서 의도에 맞지 않는 숨은 버그와 오버엔지니어링이 발생함
- 전체 코드 구조에 대한 이해도가 떨어져 성능 최적화나 개선 아이디어를 도출하기 어려워짐
- 결국 제품 SW 품질에 대한 신뢰와 자신감이 사라짐

**Agentic Engineering**은 이 문제를 해결하기 위한 엔지니어링 방법론이다. AI 에이전트를 단순히 _사용하는_ 것에서 나아가, 에이전트가 더 잘 동작하도록 **설계하고 최적화하는** 접근이다. 도구(tools), 워크플로우(workflow), 스킬(skills)을 통해 품질 문제를 해결한다.

---

## 1. Engineering의 발전 흐름

Coding Agent와 함께 Engineering 방법론도 진화해 왔다. 그 흐름을 이해하면 Agentic Engineering에서 무엇에 집중해야 하는지 파악할 수 있다.

<div style="margin:1.5rem 0; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;">
<svg width="100%" viewBox="0 0 680 470" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Engineering 발전 흐름 타임라인: 2020년 Prompt Engineering부터 2026년 Agentic Engineering까지">
  <style>
    .tl-spine { stroke:#c9c7be; stroke-width:1.5; }
    .tl-conn  { stroke:#c9c7be; stroke-width:1; }
    .tl-dot   { stroke-width:1; }
    .tl-title { font:500 14px sans-serif; }
    .tl-sub   { font:400 12px sans-serif; }
    .tl-meta  { font:400 12px sans-serif; fill:#8a897f; }
    @media (prefers-color-scheme: dark) {
      .tl-spine, .tl-conn { stroke:#55534b; }
      .tl-meta { fill:#9c9a90; }
    }
  </style>
  <line x1="60" y1="60" x2="60" y2="430" class="tl-spine"/>

  <circle cx="60" cy="80" r="8" class="tl-dot" fill="#e9e7e0" stroke="#9b998f"/>
  <rect x="90" y="60" width="280" height="46" rx="8" fill="#f1efe8" stroke="#9b998f" stroke-width="0.5"/>
  <text x="110" y="79" class="tl-title" fill="#2c2c2a">Prompt Engineering</text>
  <text x="110" y="96" class="tl-sub" fill="#5f5e5a">어떻게 질문하느냐가 전부였던 시기</text>
  <text x="390" y="78" class="tl-meta">2020년</text>
  <text x="390" y="94" class="tl-meta">User → LLM → Answer</text>
  <line x1="60" y1="88" x2="60" y2="148" class="tl-conn"/>

  <circle cx="60" cy="160" r="8" class="tl-dot" fill="#e1f5ee" stroke="#0f6e56"/>
  <rect x="90" y="140" width="280" height="46" rx="8" fill="#e1f5ee" stroke="#0f6e56" stroke-width="0.5"/>
  <text x="110" y="159" class="tl-title" fill="#085041">Context Engineering</text>
  <text x="110" y="176" class="tl-sub" fill="#0f6e56">컨텍스트 창 안을 구조적으로 설계</text>
  <text x="390" y="158" class="tl-meta">2023년</text>
  <text x="390" y="174" class="tl-meta">RAG · 메모리 · 히스토리</text>
  <line x1="60" y1="168" x2="60" y2="228" class="tl-conn"/>

  <circle cx="60" cy="240" r="8" class="tl-dot" fill="#e1f5ee" stroke="#0f6e56"/>
  <rect x="90" y="220" width="280" height="46" rx="8" fill="#e1f5ee" stroke="#0f6e56" stroke-width="0.5"/>
  <text x="110" y="239" class="tl-title" fill="#085041">AI Workflow 확산</text>
  <text x="110" y="256" class="tl-sub" fill="#0f6e56">여러 단계에 걸쳐 LLM을 반복 활용</text>
  <text x="390" y="238" class="tl-meta">2023년</text>
  <text x="390" y="254" class="tl-meta">LangGraph 등 주목</text>
  <line x1="60" y1="248" x2="60" y2="308" class="tl-conn"/>

  <circle cx="60" cy="320" r="8" class="tl-dot" fill="#eeedfe" stroke="#534ab7"/>
  <rect x="90" y="300" width="280" height="46" rx="8" fill="#eeedfe" stroke="#534ab7" stroke-width="0.5"/>
  <text x="110" y="319" class="tl-title" fill="#3c3489">Harness Engineering</text>
  <text x="110" y="336" class="tl-sub" fill="#534ab7">Workflow 레벨 안전장치 설계</text>
  <text x="390" y="318" class="tl-meta">2025년</text>
  <text x="390" y="334" class="tl-meta">장시간 실행이 핵심 키워드</text>
  <line x1="60" y1="328" x2="60" y2="388" class="tl-conn"/>

  <circle cx="60" cy="402" r="10" class="tl-dot" fill="#faece7" stroke="#993c1d" stroke-width="1.5"/>
  <rect x="90" y="380" width="280" height="50" rx="8" fill="#faece7" stroke="#993c1d" stroke-width="1.5"/>
  <text x="110" y="400" class="tl-title" fill="#712b13">Agentic Engineering</text>
  <text x="110" y="417" class="tl-sub" fill="#993c1d">SW 품질 · 사람과 AI의 협업 설계</text>
  <text x="390" y="396" class="tl-meta">2026년 ~</text>
  <text x="390" y="412" class="tl-meta">현재 우리가 있는 지점</text>
  <text x="390" y="428" class="tl-meta">도구 · 워크플로우 · 스킬</text>
</svg>
</div>

### Prompt Engineering (2020년)

구조: `User → LLM → Answer`

결과 품질이 사실상 프롬프트 하나에 의해 결정됐던 시기. **어떻게 질문하느냐**가 전부였다. 이 시기의 노하우들이 쌓여 "프롬프트 엔지니어링"이라는 방법론으로 정리됐다.

| 기법                   | 내용                                 |
| ---------------------- | ------------------------------------ |
| Few-shot               | 예제 몇 개를 함께 제시하며 질문      |
| CoT (Chain of Thought) | "단계별로 생각해줘" 키워드 활용      |
| Role 프롬프팅          | 역할·페르소나를 부여                 |
| Output Format 지정     | 결과 형식을 명시적으로 요청          |
| Reflection             | 답이 맞는지 한 번 더 검토하도록 지시 |

### Context Engineering (2023년)

LLM은 한 번에 처리할 수 있는 입력 범위인 **Context Window**를 갖는다. 이 제한된 공간 안에 어떤 정보를, 어떻게 구조적으로 넣을 것인가를 다루는 접근이다. 프롬프트를 잘 쓰는 것을 넘어, **컨텍스트 자체를 설계**하는 단계로 넘어갔다.

- 시스템 프롬프트 설계 (Rule 파일 등으로 구성)
- RAG, 메모리, 멀티턴 히스토리 구성
- 필요한 정보만 선별해 효율적으로 전달하는 전략

### AI Workflow 확산 (2023년)

단일 LLM 호출만으로는 실제 AI 서비스를 구현하기 어렵다는 것이 명확해진 시기. **여러 단계에 걸쳐 LLM을 반복 활용**해 최종 결과를 만들어내는 Workflow 개념이 등장했고, LangGraph 같은 라이브러리가 주목받기 시작했다.

Agent로 구성되는 주요 Workflow 패턴:

- 순차적(Sequential) Workflow
- 병렬적(Parallel) Workflow
- 평가-개선(Evaluator-optimizer) Workflow

### Harness Engineering (2025년)

Agent가 **장시간 실행되더라도 올바른 임무를 수행하도록** 하는 방법론. 여기서 핵심 키워드는 **장시간 실행**이다.

에이전트 자체의 성능을 높이는 것보다, Workflow 레벨에서 안전장치를 설계하는 것에 집중한다. 고삐 풀린 에이전트가 방향을 잃지 않도록 "하네스"를 장착하는 셈이다.

### Agentic Engineering (2026년)

생산성과 기능은 확보됐다. 이제 문제는 **SW 품질**이다.

코드를 이해하지 않아도 만들 수 있게 되자, 역설적으로 코드의 품질을 보장하기 어려워졌다. Agentic Engineering은 이 문제를 **사람과 AI의 협업 구조 설계**로 해결하려는 시도다.

---

## 2. ROI 관점에서 본 Agentic Engineering

### 핵심 사이클

AI에게 바로 코딩을 시키는 대신, **먼저 문서(스펙)를 작성하고 검토**한 후 지시한다. 결과물이 의도와 다르면 코드가 아닌 **문서부터 수정**한다.

<div style="margin:1.5rem 0; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;">
  <div style="display:flex; gap:12px; margin-bottom:1.25rem; flex-wrap:wrap;">
    <div style="flex:1; min-width:130px; background:#eaf3de; border-radius:8px; padding:1rem;">
      <div style="font-size:13px; color:#3b6d11; margin-bottom:4px;">플랜 문서 작성 &amp; 검토</div>
      <div style="font-size:22px; font-weight:500; color:#27500a;">낮음</div>
      <div style="font-size:12px; color:#639922; margin-top:4px;">투자 효율 最高</div>
    </div>
    <div style="flex:1; min-width:130px; background:#eaf3de; border-radius:8px; padding:1rem;">
      <div style="font-size:13px; color:#3b6d11; margin-bottom:4px;">AI 구현 비용</div>
      <div style="font-size:22px; font-weight:500; color:#27500a;">매우 낮음</div>
      <div style="font-size:12px; color:#639922; margin-top:4px;">거의 무시 가능</div>
    </div>
    <div style="flex:1; min-width:130px; background:#fcebeb; border-radius:8px; padding:1rem; border:1px solid #e24b4a;">
      <div style="font-size:13px; color:#a32d2d; margin-bottom:4px;">코드 리뷰 비용</div>
      <div style="font-size:22px; font-weight:500; color:#791f1f;">매우 큼 ⚠</div>
      <div style="font-size:12px; color:#a32d2d; margin-top:4px;">ROI의 핵심 변수</div>
    </div>
  </div>

  <div style="background:#f5f4ef; border-radius:8px; padding:0.75rem 1rem; border-left:3px solid #185fa5;">
    <div style="font-size:13px; color:#5f5e5a; margin-bottom:8px;">핵심 사이클</div>
    <div style="display:flex; align-items:center; gap:8px; flex-wrap:wrap;">
      <span style="font-size:13px; font-weight:500; padding:5px 12px; background:#fff; border:1px solid #d3d1c7; border-radius:8px; color:#2c2c2a;">문서 작성</span>
      <span style="color:#a8a69c;">→</span>
      <span style="font-size:13px; font-weight:500; padding:5px 12px; background:#fff; border:1px solid #d3d1c7; border-radius:8px; color:#2c2c2a;">검토/개선</span>
      <span style="color:#a8a69c;">→</span>
      <span style="font-size:13px; font-weight:500; padding:5px 12px; background:#fff; border:1px solid #d3d1c7; border-radius:8px; color:#2c2c2a;">AI 지시</span>
      <span style="color:#a8a69c;">→</span>
      <span style="font-size:13px; font-weight:500; padding:5px 12px; background:#fff; border:1px solid #d3d1c7; border-radius:8px; color:#2c2c2a;">결과 확인</span>
      <span style="color:#a8a69c;">→</span>
      <span style="font-size:13px; font-weight:500; padding:5px 12px; background:#fff; border:1px solid #d3d1c7; border-radius:8px; color:#2c2c2a;">수정</span>
    </div>
  </div>
</div>

### 세 가지 비용 구조

Agentic Engineering에서의 비용은 크게 세 가지다. ROI를 높이는 핵심은 가장 비싼 **리뷰 비용을 줄이는 것**이다.

| 비용 항목             | 상대적 크기 | 비고                          |
| --------------------- | ----------- | ----------------------------- |
| 플랜 문서 작성 & 검토 | 낮음        | 코드 수정 대비 투자 효율 높음 |
| AI 구현 비용          | 매우 낮음   | —                             |
| **코드 리뷰 비용**    | **매우 큼** | ROI의 핵심 변수               |

### ROI를 높이는 세 가지 전략

**1) 가독성 확보 (클린코드)**
가독성이 좋을수록 코드 이해 시간이 줄고, 리뷰 속도가 빨라지며, 전체 개발 시간이 단축된다. **클린코드는 곧 비용 절감**이다.

**2) 리뷰 가능한 단위로 분해 (Phase 설계)**
코드를 한 번에 크게 생성하는 것이 아니라, 사람이 충분히 검토할 수 있는 단위로 나누어 개발한다. "리뷰 가능한 크기"로 쪼개는 것이 핵심이다.

**3) 개발 역량 강화**
개발자의 역량이 Agentic Engineering의 효율을 크게 좌우한다.

- 클린코드·리팩터링 경험이 많을수록 → 일관된 가독성의 코드를 설계할 수 있음
- 개발 경험이 풍부할수록 → AI가 생성할 코드 형태를 예측하고 리뷰 가능한 Phase로 나눌 수 있음
- 자료구조·알고리즘 이해도가 높을수록 → 문제 분해 능력과 AI 구현 방식 예측력이 향상됨

---

## 3. 클로드를 잘 쓰기 위한 도구

### 3-1. 입력 토큰 최적화: RTK

> [github.com/rtk-ai/rtk](https://github.com/rtk-ai/rtk)

**RTK(Rust Token Killer)**는 CLI 명령어 출력을 AI에 전달하기 전에 **필터링하고 압축**하는 Rust 기반 프록시다. 단일 바이너리, 의존성 없음, 오버헤드 10ms 미만.

에이전트가 `git diff`를 실행하면 결과가 통째로 컨텍스트에 들어간다. RTK는 그 사이에 끼어들어 불필요한 내용을 제거한다.

**작동 방식:** 네 가지 전략을 조합한다.

- **필터링** — 무관한 줄 제거
- **그룹핑** — 반복 패턴 묶기
- **트런케이션** — 긴 출력 자르기
- **중복 제거** — 같은 내용 재출력 방지

**실측 절감 (30분 Claude Code 세션):**

| 작업                      | 기본         | RTK         | 절감     |
| ------------------------- | ------------ | ----------- | -------- |
| `ls` / `tree`             | 2,000        | 400         | **-80%** |
| `git diff`                | 10,000       | 2,500       | **-75%** |
| `npm test` / `cargo test` | 25,000       | 2,500       | **-90%** |
| `pytest`                  | 8,000        | 800         | **-90%** |
| **합계**                  | **~118,000** | **~23,900** | **-80%** |

**설치:**

```bash
brew install rtk        # macOS
rtk init -g             # Claude Code / GitHub Copilot
```

> **주의:** RTK가 너무 공격적으로 압축하면 에이전트가 필요한 컨텍스트를 잃어버릴 수 있음. 처음엔 보수적인 설정으로 시작하는 것이 좋다.

---

### 3-2. 출력 토큰 최적화: Caveman

> [github.com/JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman)

**Caveman**은 Claude Code 스킬로, 에이전트의 응답을 원시인 말투로 바꿔 **출력 토큰을 65~75% 줄인다.** 기술적 정확도는 100% 유지된다.

```
# 일반 Claude
"The reason your React component is re-rendering is likely because
you're creating a new object reference on each render cycle..."

# Caveman Claude
"New object ref each render. Wrap in useMemo."
```

코드 블록, 에러 메시지, 기술 용어는 그대로 유지하고, 불필요한 인사말·부연 설명·헤징 표현만 제거한다.

**압축 레벨:**

| 레벨     | 특징                        |
| -------- | --------------------------- |
| `lite`   | 필러 표현만 제거, 문법 유지 |
| `full`   | 기본 원시인 모드            |
| `ultra`  | 전보문 수준 최대 압축       |
| `wenyan` | 한문체, 가장 짧음           |

**설치:**

```bash
npx skills add JuliusBrussee/caveman
```

세션 내에서 `/caveman` 또는 `talk like caveman`으로 활성화. 한 번 켜면 세션 전체에 유지된다.

---

### 3-3. 멀티 에이전트 프레임워크 비교

세 프레임워크는 성격이 뚜렷이 다르다. 한눈에 비교하면 다음과 같다.

<div style="margin:1.5rem 0; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;">
  <div style="display:flex; gap:12px; flex-wrap:wrap;">

    <div style="flex:1; min-width:200px; background:#fff; border:1px solid #d3d1c7; border-radius:12px; padding:1rem;">
      <div style="font-size:11px; font-weight:500; letter-spacing:.03em; color:#185fa5; margin-bottom:6px;">개발 방법론</div>
      <div style="font-size:16px; font-weight:500; margin-bottom:4px; color:#2c2c2a;">Superpowers</div>
      <div style="font-size:12px; color:#5f5e5a; margin-bottom:12px;">코드 품질 향상</div>
      <div style="border-top:1px solid #e9e7e0; padding-top:10px;">
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">핵심 개념</span><span style="color:#2c2c2a;">Skill, TDD</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">기억</span><span style="color:#8a897f;">없음</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">자동화</span><span style="color:#2c2c2a;">낮음</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">난이도</span><span style="color:#3b6d11;">쉬움</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px;"><span style="color:#5f5e5a;">Claude 의존</span><span style="color:#2c2c2a;">높음</span></div>
      </div>
      <div style="margin-top:10px; font-size:11px; padding:6px 8px; background:#e6f1fb; border-radius:8px; color:#185fa5;">개인/팀 개발에 최적</div>
    </div>

    <div style="flex:1; min-width:200px; background:#fff; border:2px solid #185fa5; border-radius:12px; padding:1rem;">
      <div style="font-size:11px; font-weight:500; letter-spacing:.03em; color:#185fa5; margin-bottom:6px;">Agent OS</div>
      <div style="font-size:16px; font-weight:500; margin-bottom:4px; color:#2c2c2a;">Ouroboros</div>
      <div style="font-size:12px; color:#5f5e5a; margin-bottom:12px;">요구사항 → 명세 → 구현</div>
      <div style="border-top:1px solid #e9e7e0; padding-top:10px;">
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">핵심 개념</span><span style="color:#2c2c2a;">Spec First</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">기억</span><span style="color:#2c2c2a;">프로젝트 단위</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">자동화</span><span style="color:#2c2c2a;">중간</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">난이도</span><span style="color:#854f0b;">중간</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px;"><span style="color:#5f5e5a;">Claude 의존</span><span style="color:#2c2c2a;">높음</span></div>
      </div>
      <div style="margin-top:10px; font-size:11px; padding:6px 8px; background:#e6f1fb; border-radius:8px; color:#185fa5;">중대형 프로젝트에 최적</div>
    </div>

    <div style="flex:1; min-width:200px; background:#fff; border:1px solid #d3d1c7; border-radius:12px; padding:1rem;">
      <div style="font-size:11px; font-weight:500; letter-spacing:.03em; color:#5f5e5a; margin-bottom:6px;">개인 AI Agent</div>
      <div style="font-size:16px; font-weight:500; margin-bottom:4px; color:#2c2c2a;">Hermes</div>
      <div style="font-size:12px; color:#5f5e5a; margin-bottom:12px;">지속적 자동화</div>
      <div style="border-top:1px solid #e9e7e0; padding-top:10px;">
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">핵심 개념</span><span style="color:#2c2c2a;">Memory First</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">기억</span><span style="color:#3b6d11;">영구 기억</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">자동화</span><span style="color:#3b6d11;">매우 높음</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px; margin-bottom:6px;"><span style="color:#5f5e5a;">난이도</span><span style="color:#a32d2d;">높음</span></div>
        <div style="display:flex; justify-content:space-between; font-size:12px;"><span style="color:#5f5e5a;">Claude 의존</span><span style="color:#2c2c2a;">선택적</span></div>
      </div>
      <div style="margin-top:10px; font-size:11px; padding:6px 8px; background:#f1efe8; border-radius:8px; color:#5f5e5a;">개발 + 업무 자동화</div>
    </div>

  </div>
</div>

#### Ouroboros — Agent OS

> [github.com/Q00/ouroboros](https://github.com/Q00/ouroboros)

**"Stop prompting. Start specifying."**

Ouroboros는 AI 코딩을 위한 **Agent OS**다. 에이전트의 모든 행동을 **추적 가능하고 재현 가능한 실행 계약**으로 바꾸는 런타임 레이어다. 핵심 철학은 **Specification-First**. 바로 코딩을 시키는 대신 먼저 스펙을 정의하고 검증한 후 실행한다.

```
ourocode (쉘/TUI)
  └─ ouroboros-plugins (PR, Jira, 릴리즈 등 도메인 워크플로우)
      └─ ouroboros core (Seed · Ledger · Runtime · MCP)
```

- **Seed** — 모든 작업의 출발점이 되는 스펙 단위
- **Ledger** — 모든 에이전트 행동을 감사 가능하도록 기록
- **Runtime** — Claude Code, Codex, Gemini 등 멀티 런타임 지원

`"로그인 기능 만들어줘"`라고 하면 바로 만들지 않고, 왜 필요한지·사용자는 누구인지·실패 조건·성공 기준·보안 요구사항 등을 인터뷰한 뒤 → 스펙 생성 → 태스크 분해 → 실행 → 검증의 흐름을 밟는다.

#### Superpowers — Skills 기반 방법론

> [github.com/obra/superpowers](https://github.com/obra/superpowers)

**Superpowers**는 AI 코딩 방법론 전체를 제공하는 스킬 프레임워크다. 에이전트가 곧바로 코드부터 치지 않도록 훈련시킨다.

```
요구사항 → Brainstorm → Plan → TDD → Implementation → Review → Verification
```

기본 Claude Code가 `요구사항 → 코드 작성`의 2단계라면, Superpowers는 7단계의 구조화된 흐름을 강제한다. "구현해줘"라고 하면 TDD 사이클이, "버그 고쳐줘"라고 하면 디버깅 워크플로우가 자동으로 실행된다.

```bash
/plugin install superpowers@claude-plugins-official
```

#### Hermes Agent — 자기 학습 에이전트

> [github.com/nousresearch/hermes-agent](https://github.com/nousresearch/hermes-agent)

Nous Research가 만든 **자기 개선(self-improving) AI 에이전트**. 다른 도구들과의 결정적 차이는 **학습 루프 내장**이다.

| 기능              | 설명                                                 |
| ----------------- | ---------------------------------------------------- |
| 스킬 자동 생성    | 복잡한 작업 완료 후 재사용 가능한 스킬을 스스로 생성 |
| 크로스 세션 기억  | FTS5 세션 검색 + LLM 요약으로 과거 대화 참조         |
| 플랫폼 독립       | Telegram, Discord, Slack, WhatsApp, Signal 등        |
| 멀티 모델         | OpenRouter(200+모델), Nous Portal, OpenAI 등         |
| 병렬 서브에이전트 | 독립적인 작업을 병렬로 처리                          |
| 스케줄 자동화     | 자연어로 cron 작업 설정                              |

랩톱에 묶이지 않고 $5짜리 VPS나 GPU 클러스터에서도 실행된다. 사용하지 않을 땐 서버리스로 거의 비용이 들지 않는다.

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
hermes setup
```

---

## 4. Claude Skill과 Subagent

### Skill이란?

**Skill**은 Claude Code의 행동 방식을 정의하는 **마크다운 파일**이다. 특정 상황에서 에이전트가 어떻게 생각하고 행동해야 하는지를 지정한다. `.claude/skills/` 디렉토리에 저장되며 특정 키워드나 상황에서 자동으로 트리거된다.

```
.claude/
└── skills/
    ├── tdd.md          # "TDD로 구현해줘" → 자동 트리거
    ├── debugging.md    # 버그 발생 시 자동 트리거
    └── blog-post.md    # 블로그 글 작성 시 자동 트리거
```

### Subagent란?

**Subagent**는 메인 에이전트가 특정 작업을 위해 **독립적으로 파생시키는 에이전트**다. Claude Code에서는 `Agent` 도구를 통해 실행한다.

- **병렬 처리** — 독립적인 두 작업을 동시에 실행
- **컨텍스트 보호** — 서브에이전트의 긴 작업이 메인 컨텍스트를 오염시키지 않음
- **전문화** — 각 서브에이전트에게 전문화된 역할 부여 가능

```
메인 에이전트
├── Subagent 1: 파일 탐색 (read-only)
├── Subagent 2: 테스트 작성
└── Subagent 3: 문서 업데이트
```

### 유용한 Skills 모음

| 스킬                   | 용도                                                           |
| ---------------------- | -------------------------------------------------------------- |
| `systematic-debugging` | 버그·테스트 실패 시 가설→검증→수정 사이클을 따름               |
| `code-review`          | PR/diff 검토. `--fix`로 즉시 수정, `ultra`로 멀티에이전트 리뷰 |
| `agent-browser`        | 헤드리스 브라우저 자동화. 참조 번호 방식으로 컨텍스트 93% 절감 |
| `skill-creator`        | 대화형 Q&A로 새 스킬 설계 및 `SKILL.md` 생성                   |
| `excalidraw-diagram`   | 자연어로 다이어그램 생성, Playwright 기반 시각 검증            |
| `artifacts-builder`    | React·Tailwind·shadcn/ui로 독립실행형 HTML 아티팩트 생성       |
| `mcp-client`           | 임의의 MCP 서버에 표준 인터페이스로 연결하는 범용 커넥터       |

### 스킬 설치 방법

```bash
# Superpowers 전체 설치 (추천)
/plugin install superpowers@claude-plugins-official

# 개별 스킬 설치
npx skills add JuliusBrussee/caveman
npx skills add <github-user>/<repo>

# 로컬 스킬 직접 작성
mkdir -p .claude/skills
# .claude/skills/my-skill.md 파일 생성 후 마크다운으로 지침 작성
```

---

## 마치며

Agentic Engineering은 아직 빠르게 진화 중인 분야다. 오늘 소개한 도구들도 몇 달 후면 더 나은 것들로 대체될 수 있다. 그러나 핵심 원칙은 변하지 않는다.

> **에이전트를 믿되, 맹목적으로 믿지 마라.**
> 입력을 최적화하고, 출력을 간결하게 하고, 반복 가능한 워크플로우를 갖추고, 사람이 중요한 지점에서 검토하는 구조를 만드는 것. 그것이 Agentic Engineering의 본질이다.

AI가 코드를 잘 짜는 것보다, 엔지니어가 AI가 만든 코드를 얼마나 빠르고 정확하게 이해하고 검증할 수 있느냐가 진짜 경쟁력이다. 클린코드, 구조적 사고, 리팩토링 능력 — AI 시대에도 변함없이 중요하다.
