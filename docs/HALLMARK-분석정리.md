# Hallmark 전수조사 · 분석 정리

> 작성일: 2026-10-12
> 작성: 카리나 (Claude Code) 💖
> 원본 레포: https://github.com/nutlope/hallmark
> **내 포크 레포: https://github.com/bmshin94/hallmark**
> 공식 데모 사이트: https://www.usehallmark.com
> 라이선스: MIT (상업적 사용·포크·재배포 자유)
> 제작: Together AI (Nutlope / Hassan El Mghari)

---

## 목차

1. [한 줄 요약](#1-한-줄-요약)
2. [폴더 구조 전체 지도](#2-폴더-구조-전체-지도)
3. [이게 정확히 뭐 하는 건가](#3-이게-정확히-뭐-하는-건가)
4. [4개의 동작 (Verbs)](#4-4개의-동작-verbs)
5. [실행 플로우 Step 0~7](#5-실행-플로우-step-07)
6. [21개 골격 · 21개 테마 전체 목록](#6-21개-골격--21개-테마-전체-목록)
7. [58개 슬롭 테스트 게이트](#7-58개-슬롭-테스트-게이트)
8. [안티패턴 목록](#8-안티패턴-목록)
9. [쉬운 비유로 다시 설명](#9-쉬운-비유로-다시-설명)
10. [설치 및 사용법](#10-설치-및-사용법)
11. [플러그인? 스킬? MCP?](#11-플러그인-스킬-mcp)
12. [API 토큰 필요 여부](#12-api-토큰-필요-여부)
13. [AI 에이전트 구축에 도움이 되는가](#13-ai-에이전트-구축에-도움이-되는가)
14. [React / PHP 로 만들 수 있는가](#14-react--php-로-만들-수-있는가)
15. [유튜브 강의 제작 가능성](#15-유튜브-강의-제작-가능성)
16. [수익화 아이디어 11개 상세](#16-수익화-아이디어-11개-상세)
17. [추천 실행 로드맵](#17-추천-실행-로드맵)
18. [한계와 리스크](#18-한계와-리스크)
19. [로드맵 (원작자 계획)](#19-로드맵-원작자-계획)

---

## 1. 한 줄 요약

> **"AI가 만든 것처럼 안 보이는 UI를 만들어주는 AI 코딩 어시스턴트용 디자인 '스킬(Skill)'"**

Claude Code · Cursor · Codex 에서 동작하며, 21개 페이지 골격 × 21개 테마 × 58개 품질 게이트로
LLM이 기본값으로 뱉어내는 "AI 티 나는 UI"를 구조적으로 차단한다.

**핵심 철학 (docs/talk-slides.md 원문):**
> *"Models ship the mean of their training set."*
> (모델은 학습 데이터의 평균을 출력한다)

---

## 2. 폴더 구조 전체 지도

전체 288개 파일 · 18MB · skills 폴더만 107개 `.md` 파일 (980KB)

```
hallmark/
├── CLAUDE.md          ← 내가 직접 올린 '카리나 페르소나' 파일 (원본엔 없음)
├── GEMINI.md          ← 위와 동일 (Gemini용)
├── README.md          ← 프로젝트 소개 + 스크린샷 갤러리
├── ROADMAP.md         ← 향후 기능 로드맵
├── LICENSE            ← MIT
├── package.json       ← npm 패키지 v1.1.0 (실행 코드 없음!)
├── vercel.json        ← site/ 정적 호스팅 설정
│
├── skills/hallmark/   ⭐ 핵심 (107개 .md · 980KB)
│   ├── SKILL.md       ← 두뇌 (67KB · 558줄 · 약 9,400 단어)
│   └── references/
│       ├── macrostructures/  (21개) ← 페이지 '골격' 카탈로그
│       ├── components/       (50개) ← 네비 14 / 히어로 9 / 푸터 8 / 기능 6 /
│       │                              섹션헤드 5 / CTA 4 / 후기 4
│       ├── themes/           (5개)  ← carnival, cobalt, grid, hum, lumen 상세 스펙
│       ├── genres/           (4개)  ← editorial, modern-minimal, atmospheric, playful
│       ├── verbs/            (2개)  ← audit.md, redesign.md
│       └── (24개 루트 파일)
│           ├── slop-test.md         (31KB) ← 58게이트 + 자가채점
│           ├── anti-patterns.md     (25KB) ← 70+ 안티패턴
│           ├── study.md             (42KB) ← DNA 추출 프로토콜
│           ├── custom-craft.md      (34KB) ← CSS아트/SVG 제작
│           ├── hero-enrichment.md   (32KB) ← 히어로 보강
│           ├── component-cookbook.md(30KB) ← 50 컴포넌트 인덱스
│           ├── assets.md            (25KB) ← 이미지/아이콘 소스
│           ├── custom-theme.md      (24KB) ← 커스텀 테마 설계
│           ├── microinteractions.md (20KB)
│           ├── typography.md        (18KB)
│           ├── structure.md         (15KB)
│           ├── export-formats.md    (14KB) ← 4포맷 익스포트
│           ├── interaction-and-states.md (13KB) ← 8개 상태
│           ├── copy.md              (12KB)
│           ├── macrostructures.md   (11KB) ← 21골격 슬림 인덱스
│           ├── imagery-kit.md       (8KB)
│           ├── design-md.md         (6KB)
│           ├── layout-and-space.md  (6KB)
│           ├── responsive.md        (6KB)
│           ├── floating-nav.md      (5KB)
│           ├── color.md             (4KB)  ← OKLCH
│           ├── motion.md            (4KB)
│           ├── preview-examples.md  (3KB)
│           └── contract.md          (2KB)
│
├── docs/
│   ├── recipes.md        (13KB) ← 복붙용 검증 프롬프트 9개
│   ├── study-examples.md (12KB) ← DNA 추출 실전 예제 3개
│   ├── talk-slides.md    (14KB) ← 발표 슬라이드 원고 14장 ⭐유튜브 대본
│   └── screenshots/      (18장)
│
└── site/              ← 데모 사이트 (usehallmark.com 소스)
    ├── index.html        (63KB) ← T키 누르면 21개 테마 순환!
    ├── css/
    │   ├── tokens.css     (55KB) ⭐ 21테마 전체 토큰
    │   ├── components.css (134KB)
    │   ├── sections.css   (60KB)
    │   └── base.css       (6KB)
    ├── js/main.js        (48KB)
    ├── examples/  (19개) ← 완성 랜딩페이지 (전부 바닐라 HTML+CSS)
    │   ├── tally, wayfare, najm, hyperlane, bananastudio
    │   ├── hum-07, cobalt-01, carnival-01, lumen-01, garden-01
    │   ├── riso-01, press-01, grid-01
    │   └── custom-01 ~ custom-05
    └── _tests/    (18개) ← 레시피별 테스트 빌드 + verbs 예제
```

### 🔑 가장 중요한 발견

```bash
$ find skills -type f ! -name '*.md'
(결과 없음)
```

**`skills/` 폴더에 실행 파일이 단 하나도 없다.** 전부 마크다운.
→ 이건 "프로그램"이 아니라 **"AI에게 주는 초강력 지침서"**다.

---

## 3. 이게 정확히 뭐 하는 건가

### 문제 정의

AI에게 "랜딩페이지 만들어줘" 하면 항상 똑같은 걸 뱉는다:

| AI가 늘 뱉는 그것 | 왜? |
|---|---|
| 보라→파랑 그라데이션 히어로 | 학습 데이터의 평균값 |
| Inter 폰트 (또는 Poppins) | 제일 흔하니까 |
| 아이콘 위 + 제목 아래, 3칸 카드 그리드 | 템플릿 1위 |
| 화면 꽉 채운 가운데정렬 히어로 | 안전빵 |
| 히어로 → 기능3개 → CTA → 푸터 | 영원한 그 구조 |

### Hallmark의 해결 방식 — 5단 방어선

**① 21개 macrostructure (페이지 골격)를 코드 쓰기 *전에* 강제 선택**
각 골격은 제목 배치 · 본문 구성 · 구분선 언어 · 버튼 voice · 이미지 처리 · 등장 방식을
하나의 이름으로 묶은 **완결된 페이지 형태**.

**② 21개 테마 (색·폰트 토큰 세트) + Custom 모드**
카탈로그에 없는 느낌이면 OKLCH 팔레트를 그 자리에서 설계.

**③ 58개 slop test 게이트**
빌드 후 58개 질문에 전부 "아니오"가 나와야 통과.

**④ 출력 전 자가채점 (Pre-emit self-critique)**
6축(Philosophy·Hierarchy·Execution·Specificity·Restraint·Variety)을 1~5점 셀프 채점.
3점 미만이면 스스로 revision pass. CSS 맨 위에 도장:
```css
/* Hallmark · pre-emit critique: P5 H4 E5 S4 R5 V5 */
```

**⑤ 다양화 강제 (Diversification)**
`.hallmark/log.json`에 빌드 기록을 남기고, 다음 실행에서 **반드시 읽어서** 중복 회피.

```json
[{
  "date": "2026-05-04",
  "macrostructure": "Marquee Hero",
  "theme": "custom",
  "theme_axes": "light / geometric-sans / warm",
  "vibe": "hyped Moroccan drop, editorial fashion, sun-warm earth",
  "enrichment": "Tier-A pure-CSS art (zellige + textile gradients)",
  "brief": "NAJM · 모로칸 의류 브랜드 · 랜딩 + 카트"
}]
```

**테마 3축 규칙** — 연속된 두 테마는 아래 3축 중 **최소 1개**가 달라야 통과:
- **Paper band** — dark (L<30%) / mid (30~85%) / light (>85%)
- **Display style** — high-contrast-serif / roman-serif / classical-serif /
  geometric-sans / grotesk-sans / rounded-sans / mono / display-condensed /
  display-heavy / risograph-bold
- **Accent hue** — warm (10~60°) / cool (200~300°) / neutral / chromatic-other

**추가로 네비·푸터도 다양화 대상** — "연속된 출력은 같은 네비 archetype 또는
같은 푸터 archetype을 공유할 수 없다". SKILL.md는 이걸 "실무에서 가장 많이 위반되는 규칙"이라 표현.

---

## 4. 4개의 동작 (Verbs)

| 명령 | 동작 |
|---|---|
| *(기본)* | 새 UI 제작. 골격 선택 → 테마 선택 → 빌드 → 58게이트 검사 |
| `hallmark audit <대상>` | 안티패턴으로 채점. **수정 안 하고 지적만** (critical/major/minor 펀치리스트) |
| `hallmark redesign <대상> [--mood <name>]` | 내용·IA·브랜드 유지, **구조만 새로**. 기존 구현 경계 안에서 작업 |
| `hallmark study <스샷\|URL>` | **DNA 추출** (골격·타입페어링·컬러앵커). 픽셀 복제 거부, 유료 템플릿 URL 거부 |

### audit 상세
- **Tell** (명명된 안티패턴) + **Where** (파일:줄) + **Severity** + **Fix** (한 줄 수정법)
- 구조적 지문도 검사: "AI 템플릿 구조면 시각적으로 괜찮아도 critical"
- **Stamp-vs-page 검사**: 도장이 "Bento Grid"인데 실제가 가운데정렬 히어로면 `stamp lies` critical
- **Genre-aware**: 도장에 genre가 있으면 장르별 완화 규칙 적용
- **design.md 감사**: 시스템 관리 프로젝트는 테마 드리프트를 critical로 처리

### study 상세
- URL 모드: WebFetch로 HTML/CSS 읽어 **정확한 폰트명·컬러값** 추출 (리듬은 판단 불가)
- 이미지 모드: 스크린샷 기반
- 진단 후 3가지 선택: ⓐ `build it` ⓑ `lock the DNA` / `give me a design.md` ⓒ 진단만
- URL 모드로 design.md 발행 시 **"본인 소유 또는 자기 브랜드용 공개 레퍼런스"임을 확인(attestation)** 요구
- auth-walled / JS-only SPA / 읽기 불가 시 스크린샷 요청으로 폴백

---

## 5. 실행 플로우 Step 0~7

```
Step 0  Pre-flight scan
        ├ design.md (있으면 최우선! 모든 걸 덮어씀)
        ├ 폰트 스택 (next/font, @fontsource, geist, Google Fonts link, tailwind fontFamily)
        ├ 팔레트 (:root OKLCH/HSL/hex, tailwind colors, tokens.json, DTCG)
        ├ 모션 스탠스 (framer-motion, gsap, motion, lenis, lottie-react, react-spring)
        ├ 스페이싱 스케일 (tailwind spacing, --space-* 패턴, 4pt/8pt)
        └ 프레임워크 (Next, Astro, Vue, Svelte, Remix, 바닐라)
        → .hallmark/preflight.json 캐시 (mtime 비교로 재스캔 판단)

Step 1  Design-context gate
        "① 타깃(Audience) ② 핵심 액션(Use case) ③ 톤(Tone)" 3가지 질문
        - 무조건 1번은 물어봄 (5단어 브리프라도!)
        - "go ahead" / "알아서 해" 하면 추론해서 진행
        - audit / study / redesign --mood 는 게이트 생략
        - 톤은 극단을 고르게: editorial·brutalist·soft·utilitarian·
          luxury·playful·technical·austere ("깔끔하고 모던"은 톤이 아님)

Step 2  골격 먼저 선택! (코드 전에)
        - 21개 중 1개 + 네비(N1a~N13, 14종) + 푸터(Ft1~Ft8, 8종)
        - 슬림 인덱스만 읽고 '고른 1개 파일만' 로드 (토큰 절약)
        - 소리내어 선언: "Macrostructure: X. Nav: Y. Footer: Z. Theme: W.
                        지난번과 다른 축: ___"
        - N1a(워드마크+2링크) / Ft3(4단 링크+소셜) 는 'AI 지문 1순위' → 기본 회피
        - Specimen 골격은 더 이상 기본값 아님 (명시적 요청 시에만)

Step 2.5 프로젝트 메모리
        .hallmark/log.json 최근 3~5개 읽고 중복 회피
        → 로테이션을 평문으로 선언 (사용자 책임 라인)

Step 2.6 테마 라우팅 (4분기)
        0) study 진단 직후 "build it" → studied-DNA (다양화 일시 중단)
        1) 사용자가 custom 지정 → custom-theme.md 로드
        2) 사용자가 catalog 지정 → 21테마 중 선택
        3) 아무 신호 없음 (vanilla) → catalog 기본, 묻지 않음

Step 3  룰셋 로딩 (선별 로드 = 토큰 비용 관리)
        ├ Always:      genre 파일 1개 + (있으면) 테마 스펙 1개
        ├ Index-pick:  macrostructures.md → 1개 / component-cookbook.md → 5~7개
        ├ Per-build:   typography, color, layout-and-space, motion, copy, anti-patterns
        ├ Conditional: microinteractions, interaction-and-states, responsive,
        │              structure, hero-enrichment, custom-craft, assets,
        │              custom-theme, design-md, preview-examples
        ├ At-the-end:  slop-test(Step7만!), contract, export-formats
        └ Human-only:  docs/recipes.md, docs/study-examples.md (자동 로드 금지)

Step 4  히어로 보강 판단
        기본값 = "타이포만". 이미지 계층(강제):
        타이포만 → Tier A 순수CSS아트 → Tier B 수제SVG
          → Tier C 생성AI(Nanobanana/Recraft) → Tier D 라이브러리
          → Tier E Lottie (최후! "CSS로 가능한데 Lottie 쓰면 그게 새로운 AI 티")

Step 5  Preview (코드 쓰기 전!)
        마크다운 불릿 6개 + 선택 1개 + CTA 1줄
        - Macrostructure · Theme · Enrichment · Sections · Motion · Slop test
        - (선택) Diversification
        - *"System portable? Say `lock the system` to extract..."*
        → 여기서 방향 수정하면 코드 낭비 0

Step 6  Build
        - OKLCH 전용 색 + :root 커스텀 프로퍼티
        - 4pt 스페이싱 스케일 (--space-sm 등 시맨틱 네이밍)
        - 디스플레이 + 본문 폰트 페어링 (단일폰트는 그게 디자인일 때만)
        - 8개 상태 전부
        - transform / opacity 만 애니메이션 (레이아웃 속성 금지)
        - 명명된 3개 이징만 (--ease-out/in/in-out), 브라우저 기본 ease 금지
        - prefers-reduced-motion 지원 (공간 모션 → ≤150ms 크로스페이드)
        - :focus-visible 링 3:1 이상, 절대 애니메이션 금지 (즉시 표시)
        - 모션은 추가 전에 삭제 ("제거해도 정보 손실 없으면 제거")
        - 도장 찍기: /* Hallmark · macrostructure: X · tone: Y · anchor hue: Z */
        - .hallmark/log.json 앞쪽에 append (최근 20개 유지)
        - 기존 글로벌 스타일시트는 append-only (@tailwind 지시문 보존!)
        - tokens.css 무조건 발행 (단일 페이지 빌드도)
        - design.md 있으면 4포맷 익스포트
          (tokens.css / Tailwind v4 @theme / DTCG tokens.json / shadcn CSS vars)

Step 7  Slop test
        58게이트. 하나라도 걸리면 고치고 재검사. "Do not ship slop."
```

### 컴포넌트 스코프 분기

"버튼만 만들어줘" 같은 요청은 **페이지용 장치를 전부 끈다**:
- 유지: Step 0 프리플라이트, Step 1 장르, Step 2.6 테마, 2+1 폰트, **8상태(더 엄격!)**, 보편 게이트
- 생략: 골격 / 네비 / 푸터 / 히어로 폴리시 / Step 4 보강 / 멀티섹션 프리뷰 / log.json 기록
- 추가 발행: `<Component>.preview.html` — 8개 상태를 한 페이지에 세로로 나열한 데모

```css
/* Hallmark · component: <type> · genre: <genre> · theme: <theme>
 * states: default · hover · focus · active · disabled · loading · error · success
 * contrast: pass (46–50)
 */
```

---

## 6. 21개 골격 · 21개 테마 전체 목록

### 21개 macrostructure (페이지 골격)

| # | 이름 | 설명 |
|---|---|---|
| 01 | **Bento Grid** | 크기 다른 모듈 블록의 불규칙 그리드. 리듬은 크기 변화에서 |
| 02 | **Long Document** | 메모·편지·일기처럼 읽힘. 마케팅 구조 없음. 제품에 대한 '문학' |
| 03 | **Marquee Hero** | 히어로가 곧 첫 화면 전체. 서브헤드·CTA 없음. 아래는 다른 것 |
| 04 | **Stat-Led** | 히어로가 거대한 숫자. 모든 게 그걸 뒷받침. 데이터가 서사 |
| 05 | **Workbench** | 제품 스크린샷이 주 콘텐츠. 앱 사용 가이드 투어 |
| 06 | **Conversational FAQ** | 굵은 질문 + 짧은 답. 제품과의 정직한 인터뷰 |
| 07 | **Manifesto** | 논쟁적 대형 타입. 선언 에너지. 정치 포스터 미학 |
| 08 | **Photographic** | 거대 이미지가 각 폴드를 지배. 텍스트는 작은 주석 |
| 09 | **Quote-Led** | 히어로가 인용구 + 출처. 빌려온 신뢰로 시작 |
| 10 | **Specimen** | 좌측 번호 라벨 + 거대 세리프 + 비대칭 스팬. 활자 주조소 에너지 |
| 11 | **Catalogue** | 같은 것의 변형을 균일 그리드로. 재고의 시각적 색인 |
| 12 | **Letter** | 1인칭 친밀. "친애하는 ___," 로 시작. 첫 화면에 버튼 없음 |
| 13 | **Index-First** | 페이지가 곧 링크 목록. 내비게이션이 디자인 |
| 14 | **Narrative Workflow** | 번호 붙은 단계로 사용 과정을 서사화 (1.0 → 2.0 → 3.0) |
| 15 | **Split Studio** | 딥틱. 모든 블록이 화면을 둘로. 방향이 교대로 바뀜 |
| 16 | **Feature Stack** | 좌측 sticky 라벨 + 우측 스크롤 동기 스크린샷. 시네마틱 |
| 17 | **Type Specimen** | 타입페이스가 곧 디자인. 주조소 홈페이지 |
| 18 | **Portfolio Grid** | 필터 가능한 프로젝트 카드. 작업물이 제품 |
| 19 | **Map / Diagram** | 거대 공간 다이어그램이 페이지를 조직. 정보를 '공간적'으로 |
| 20 | **Ecosystem Index** | 복수의 발견 표면 (featured/latest/category/people). 브라우징이 가치 |
| 21 | **Component Playground** | 코드+프리뷰 블록이 주 콘텐츠. 복붙 가능하게 |

> 브리프가 애매할 때는 **01~10번 중에서** 고르라고 명시 (80% 브리프 커버)

### 21개 테마 (site/css/tokens.css 에서 추출)

```
specimen · midnight · brutal · garden · atelier · newsprint · terminal
manifesto · almanac · sport · studio · riso · bloom · coral · cobalt
aurora · editorial · carnival · lumen · hum · grid
```

**상세 스펙 파일이 있는 테마 5개:** carnival, cobalt, grid, hum, lumen

**테마별 컴포넌트 voice (radius/border 규율):**
- 에디토리얼 (specimen, newsprint, atelier) → 각진 사각형 유지
- 테크니컬 (almanac, midnight, terminal) → 각진 사각형 유지
- 브루탈 (brutal, manifesto) → 두꺼운 테두리 (`--rule-card: 2px`)
- 소프트 (garden, studio, bloom, coral, aurora) → 둥근 모서리 (bloom은 16px + pill 999px)

### 네비 14종 · 푸터 8종

**네비:** N1a(최소 2링크) · N1b(정석 SaaS 3섹션) · N2(플로팅 칩) · N3(사이드 레일) ·
N4(⌘K 숨김) · N5(플로팅 필) · N6(신문 마스트헤드) · N7(브루탈 슬랩) · N8(터미널) ·
N9(엣지 정렬) · N10(스크롤 모프) · N11(메가메뉴) · N12(배너+리트랙트) · N13(인라인 ⌘K 필)

**푸터:** Ft1(마스트헤드) · Ft2(인라인 룰 1줄) · Ft3(색인형 카테고리) · Ft4(고밀도 타이포) ·
Ft5(스테이트먼트) · Ft6(레터 클로즈) · Ft7(뉴스레터 우선) · Ft8(마키 스크롤)

> ⚠️ **N1a 와 Ft3 는 "가장 잘 알려진 AI 지문"** → 기본 회피 대상

---

## 7. 58개 슬롭 테스트 게이트

### 자가채점 6축 (게이트 검사 *전에* 실행)

| 축 | 채점 기준 |
|---|---|
| **A Philosophy** | 명확한 '왜'가 있나? 페이지가 취하는 입장이 있나? 아니면 그냥 레이아웃인가? |
| **B Hierarchy** | 2초 안에 1차·2차·3차를 구분할 수 있나? 전부 같은 무게인가? |
| **C Execution** | 룰 두께·강조색 면적·텍스트 랩·포커스 링·대비가 스펙대로인가? |
| **D Specificity** | '이 브리프'처럼 보이나? 아니면 '아무나'일 수 있는 페이지인가? |
| **E Restraint** | 제 역할 못 하는 걸 전부 제거했나? 장식·중복·패딩용 패딩? |
| **F Variety** | 이전 출력과 구조적 지문을 공유하나? (색 교체는 다양성 아님) |

> 2패스는 정상. **3패스면 디자인이 아니라 브리프가 잘못된 것** → 브리프 재독

### 게이트 카테고리 (총 58개)

| 카테고리 | 게이트 번호 | 주요 내용 |
|---|---|---|
| Visual | 1~7 | Inter 폰트 / 보라-파랑 그라데 / 3칸 카드 / 카드속카드 / 사이드스트라이프 / 100vh 가운데 히어로 / 순수 #000·#fff |
| Structural | 8~9 | AI 템플릿 구조 재사용 / 섹션이 동일 리듬 |
| Microinteractions | 10~19 | transition:all / hover:scale-105 / 바운스 이징 / 다중 호버 / 레이아웃 애니메이션 / 포커스링 페이드 / 축하 토스트 / 툴팁 딜레이 동일 / 캐러셀 일시정지 없음 / Jane Doe·Acme |
| Variety | 20~21 | 도장 누락 / Specimen 기본값 사용 |
| Implementation | 22~27 | chroma 0 회색 / 강조색 5% 초과 / 스케일 밖 간격 / measure 45~75ch 벗어남 / 8상태 미구현 / reduced-motion 누락 |
| Hero enrichment | 28~33 | (이미지 보강 관련) |
| Diversification | ~ | log.json 기반 중복 |
| Layout safety | 34~ | **가로 스크롤 / overflow-x: clip (hidden 아님!)** |
| Typography | 38a 등 | **이탤릭 헤더 금지** (AI 티 1순위) |
| Input state | ~ | 입력 상태 |
| Contrast | 40~41 | 대비 비율 |
| Nav·Footer·Hero slop | 42~45 | **AI 네비 / AI 푸터 / 모든 섹션 eyebrow** |
| Honest copy | 46 | **조작된 지표 ("50,000+ 팀", "47% 향상")** |
| Re-drawn chrome | 47 | **가짜 브라우저 바 / 폰 프레임 / IDE 창** |
| Token discipline | 48 | **중간에 raw OKLCH/hex 직접 쓰기** |
| Responsive click | 49 | **클릭 텍스트 2줄 되기** |
| Mobile 비협상 | 50~53 | 이미지 그리드 `minmax(0,1fr)` / 긴 단어 `overflow-wrap:anywhere` / 섹션헤드 1단 붕괴 / 라디오탭 스크롤점프 |
| 추가 | 54 | **섹션 라벨 좌우 2단 배치 (가장 확실한 템플릿 티)** |

### 장르별 완화 (genre-scoped)

| 게이트 | 완화 장르 | 내용 |
|---|---|---|
| 2 (그라데이션) | atmospheric | 배경에만 radial 허용. **텍스트 그라데는 어떤 장르도 불허** |
| 6 (가운데 히어로) | atmospheric, playful | 캔버스 자체가 디자인일 때 허용 (Suno 스타일) |
| 7 (순수 #fff) | modern-minimal | 허용 (Stripe / ElevenLabs 학파) |
| 21 (Specimen) | atmospheric, modern-minimal, playful | 절대 기본값 안 됨 |
| 22 (chroma 0) | modern-minimal | 무채색 허용 (모노크롬 학파) |
| 23 (강조색 5%) | atmospheric | radial bloom 20%까지 허용 |

### 6개 전역 디시플린 (모든 verb에 적용)

1. **Pre-emit self-critique** — 6축 채점, 3점 미만 → revision
2. **Honest copy** — 지표/후기/로고/케이스 수 조작 금지. 없으면 `—` + "metric to confirm"
3. **Locked tokens** — 빌드 중 raw OKLCH/hex/rgb 금지. 무조건 `var(--token)`
4. **Re-drawn chrome 금지** — 가짜 브라우저/폰/IDE 창
5. **Mobile responsiveness** — 320/375/414/768px 전부 검증 (hard floor)
6. **Typography purity** — 이탤릭 헤더 금지. 강조는 weight/accent/underline으로

---

## 8. 안티패턴 목록

`anti-patterns.md` (25KB)에 **70개 이상**이 "이름 + 왜 실패하는지 + 고치는 법" 3단으로 정리됨.

### 🔴 Critical (슬롭으로 출하됨) — 16개

보라 그라데 히어로 · Inter-everywhere · 3칸 기능 그리드 · 카드속카드 ·
그라데이션 헤드라인 · 사이드스트라이프 카드 · 전체화면 가운데 히어로 ·
순수 검정/흰색 · **기본값 동일성(default-attractor sameness)** · **Specimen 폴스루** ·
**AI 네비** · **AI 푸터** · 오로라 블롭 배경 · 플로팅 오브 장식 ·
소리 자동재생 · LCP 지연로딩

### 🟡 Major (AI가 만든 것처럼 보임) — 17개

바운스/엘라스틱 이징 · 전부 가운데정렬 · **이탤릭 헤더** · 모든 섹션에 eyebrow ·
다크에 섀도글로우 · 아이콘타일 기능카드 · 목적 없는 글래스모피즘 ·
호버 전용 어포던스 · tabular-nums 없는 표 데이터 · 전부 스크롤 애니메이션 ·
아이콘 세트 불일치 · AI 일러스트 룩 · **조작된 지표** · 기능 아이콘에 범용 이모지 ·
재그린 UI 크롬 · 렌더 중 토큰 즉흥 · 클릭 텍스트 2줄 랩 · Lottie 지름길 ·
정물에 Three.js

### 🔵 Microinteraction tells — 13개

`transition-all` · 범용 `hover:scale-105` · UI에 바운스 오버슈트 ·
호버 그라데 애니메이션 · 커서 팔로워 점 · 일시정지 없는 자동 캐러셀 ·
축하 성공 토스트 · 되돌릴 수 있는 작업에 확인 다이얼로그 ·
호버/포커스 딜레이 동일한 툴팁 · 페이드인 되는 포커스 링 ·
레이아웃 밀어내는 토스트 · 범용 스크롤 페이드업 · 깜빡이는 스피너

### ⚪ Minor (작은 취향 문제) — 8개

직선 따옴표(") · 하이픈 2개(--) · 마침표 3개(...) · 플레이스홀더 이름(Jane Doe) ·
스타트업 클리셰 작명(Acme/Nexus/Seamless/Unleash) · `z-index: 9999` ·
모든 섹션 동일 패딩 · 100vw 폭

---

## 9. 쉬운 비유로 다시 설명

### 🍜 비유 1: Hallmark = "AI를 위한 디자인 교과서 + 시험지"

- **AI(클로드)** = 요리사
- **내 요청** = "파스타 해주세요"
- 문제: 이 요리사는 전 세계 레시피를 다 외웠는데, 그래서 **항상 "가장 평균적인 파스타"**만 만든다

Hallmark가 하는 일:
1. 📖 **교과서를 쥐어줌** → "면 21개 중 하나 골라. 지난번 쓴 건 빼고"
2. 📝 **시험지 58문항** → 만든 뒤 "MSG 넣었니? 아니오..." 전부 통과해야 서빙
3. 📒 **장부를 적게 함** → "지난주 크림이었으니 이번엔 오일"

### 📁 비유 2: 폴더를 책꽂이로 보면

| 폴더 | 비유 |
|---|---|
| `SKILL.md` | 🧠 두뇌 / 매뉴얼 1권 |
| `macrostructures/` | 🏠 집 평면도 카탈로그 |
| `components/` | 🚪 문·창문·계단 부품 카탈로그 |
| `themes/` | 🎨 페인트 색상표 |
| `anti-patterns.md` | 🚫 "이거 하면 촌스러움" 블랙리스트 |
| `slop-test.md` | ✅ 최종 품질검사 체크리스트 |
| `docs/recipes.md` | 📋 "이렇게 주문하세요" 예시 |
| `site/examples/` | 🖼️ 모델하우스 19채 |

### 🔄 비유 3: Before / After

**Hallmark 없을 때**
```
나:  "베이커리 랜딩페이지 만들어줘"
AI:  (코드 500줄) → 보라 그라데 + Inter + 3칸 카드 + 가운데 히어로
나:  "...어디서 본 것 같은데"
```

**Hallmark 있을 때**
```
나:  "베이커리 랜딩페이지 만들어줘"
AI:  ① 프리플라이트 스캔 (폰트/팔레트/프레임워크 파악)
     ② "타깃 / 핵심액션 / 톤 3가지 알려줘" (또는 "알아서 해")
     ③ 선언: "Macrostructure: Long Document. Theme: Garden.
              Nav: N6 Masthead. Footer: Ft6 Letter-close.
              지난번과 다른 축: 강조색 색조 + 디스플레이 서체"
     ④ 프리뷰 6불릿 → 여기서 방향 수정 가능 (코드 낭비 0)
     ⑤ 코드 작성
     ⑥ 58게이트 검사
     ⑦ tokens.css 발행 + log.json 기록
```

**차이점 3가지**
- 코드 **쓰기 전에** 미리보기 → 토큰 절약
- 선택을 **말로 선언** → 머릿속 기본값 차단
- **기록을 남김** → 다음엔 다른 걸 고름

### 🤔 비유 4: 왜 효과가 있나 (원리)

```
AI의 자연스러운 길:  "랜딩페이지" → [평균 템플릿] → 출력
                                    ↑
방어선 ①  골격 21개 중 "지난번과 다른 것" 강제 선택  (평균 경로 차단)
방어선 ②  테마 21개 + 3축 중 1축 이상 달라야 함      (색 돌려쓰기 차단)
방어선 ③  58게이트 사후 검사                        (빠져나온 것 사살)
```

복잡한 기술 없음. **"선택지를 강제로 늘리고, 체크리스트로 검사한다"** 끝.

---

## 10. 설치 및 사용법

### 방법 1 — npx 한 줄 (추천)

```bash
npx skills add nutlope/hallmark
```
업데이트는 같은 명령 재실행.

### 방법 2 — 수동 복사 (내 포크 버전)

```bash
git clone https://github.com/bmshin94/hallmark.git
cd hallmark

# Claude Code (전역)
mkdir -p ~/.claude/skills/hallmark && cp -r skills/hallmark/* ~/.claude/skills/hallmark/

# Claude Code (프로젝트)
mkdir -p .claude/skills/hallmark && cp -r skills/hallmark/* .claude/skills/hallmark/

# Codex (개인 / 프로젝트)
mkdir -p ~/.codex/skills/hallmark && cp -r skills/hallmark/* ~/.codex/skills/hallmark/
mkdir -p .codex/skills/hallmark   && cp -r skills/hallmark/* .codex/skills/hallmark/
```

### 방법 3 — Cursor

```bash
mkdir -p .cursor/rules
sed '1,5d' skills/hallmark/SKILL.md > .cursor/rules/hallmark.mdc   # 프론트매터 제외
```
⚠️ Cursor는 `references/` 상대경로를 자동 추적 못 함 → 필요한 파일은 `@파일`로 수동 첨부

### 데모 사이트 로컬 실행

```bash
npm run serve            # python3 -m http.server --directory site 4173
# → http://localhost:4173   (T 키 = 21테마 순환!)
```

### 트리거 문구 치트시트

| 하고 싶은 것 | 문구 |
|---|---|
| 질문 건너뛰고 바로 빌드 | `go ahead` / `알아서 해` / `just build it` / `you pick` / `don't ask` |
| 디자인 시스템 파일 뽑기 | `lock the system` / `give me a design.md` / `make this portable` |
| 프리플라이트 재스캔 | `refresh pre-flight` / `scan again` / `re-scan` |
| 커스텀 테마 강제 | 브랜드 컬러 지정 + 다속성 vibe 명시 |
| 컴포넌트만 작업 | `버튼만` / `just the X` / `only the Y` / `this one element` |
| study DNA로 빌드 | `build it` / `make it` / `use this DNA` |
| DNA 고정 | `lock the DNA` |

### 설치 후 프로젝트에 생기는 파일

```
내프로젝트/
├── .hallmark/
│   ├── log.json        ← 빌드 기록 (최근 20개, 다양화용)
│   └── preflight.json  ← 스캔 결과 캐시
├── tokens.css          ← 디자인 토큰 (매 빌드 무조건 발행)
├── design.md           ← (선택) "lock the system" 시에만
└── styles.css          ← 맨 윗줄 도장
                           /* Hallmark · macrostructure: ... */
```

> `.hallmark/`를 git에 커밋하면 팀원끼리 다양화 기록 공유 가능

---

## 11. 플러그인? 스킬? MCP?

### 정답: **100% "스킬(Skill)"**

증거:
```yaml
# skills/hallmark/SKILL.md 프론트매터
---
name: hallmark
description: "Anti-AI-slop design skill for greenfield pages, audits,
              redesigns, and design extraction from URLs or screenshots..."
version: 1.1.0
---
```
```json
// package.json
"skill": {
  "entry": "skills/hallmark/SKILL.md",
  "references": "skills/hallmark/references",
  "harnesses": ["claude-code", "cursor", "codex"]
}
```
```bash
$ find skills -type f ! -name '*.md'    # → 결과 없음 (실행 코드 0개)
```

### 3개 개념 비교

| | **Skill** (=Hallmark ✅) | **Plugin** | **MCP** |
|---|---|---|---|
| 정체 | AI가 읽는 지침서 (마크다운) | 기능 묶음 패키지 | 외부 도구 연결 프로토콜 |
| 구성 | SKILL.md + references/ | 커맨드+에이전트+훅+스킬 | 서버 프로세스 |
| 실행 | ❌ 읽기만 | ⭕ 훅 등 실행 | ⭕ 서버 상시 실행 |
| 로딩 | description 매칭 시 자동 | 설치 시 등록 | 설정 등록 후 연결 |
| 설치 위치 | `~/.claude/skills/<name>/` | `~/.claude/plugins/` | settings.json / .mcp.json |
| 네트워크 | ❌ 불필요 | 경우에 따라 | ⭕ 필요 |
| 비유 | 📖 교과서 | 🧰 공구세트 | 🔌 전화선 |

### 플러그인으로 포장 가능

```
hallmark-plugin/
├── .claude-plugin/plugin.json
├── skills/hallmark/          ← 지금 스킬 그대로
├── commands/
│   ├── hm-audit.md           ← /hm-audit 슬래시 커맨드
│   └── hm-study.md
└── hooks/hooks.json          ← 저장 시 자동 slop-test 등
```

### MCP로 만들면? (로드맵 "Later"에 있음, 미구현!)

> *"Live preview as an MCP server — watch the file, render in a sandbox,
> screenshot, feed the screenshot back for self-critique against the slop test."*

현재 최대 약점 = **실제 렌더 화면을 안 보고 CSS 코드만 보고 58게이트 검사**
MCP 서버로 만들면:
1. 파일 저장 감지 → Playwright 렌더
2. 320/375/414/768px 스크린샷 4장
3. 스크린샷을 AI에 재입력 → **실제로 보고** 검사
4. 실패 시 자동 수정 루프

→ **선점 가능한 큰 기회** (수익화 아이디어 5번)

---

## 12. API 토큰 필요 여부

### 결론: **Hallmark 자체는 토큰 0개, 완전 무료**

```bash
$ grep -rniE 'api[_-]?key|api token|\$[A-Z_]*API' skills/
→ API 키를 '요구'하는 코드/설정: 0건
→ 언급된 건 전부 '추천 도구 목록' 안에서만
```

### 상황별 정리

| 상황 | 토큰 필요? | 비용 |
|---|---|---|
| 스킬 설치 | ❌ | 무료 (MIT) |
| 기본 빌드 (타이포만) | ❌ | AI 구독료만 |
| `hallmark audit` | ❌ | AI 구독료만 |
| `hallmark redesign` | ❌ | AI 구독료만 |
| `hallmark study` (스샷) | ❌ | AI 구독료만 |
| `hallmark study` (URL) | ❌ (WebFetch 내장) | AI 구독료만 |
| 데모 사이트 로컬 | ❌ | 무료 |
| Tier A/B 이미지 (CSS아트/SVG) | ❌ | 무료 |
| **Tier C 이미지 (생성AI)** | ⭕ 선택적 | 아래 표 |

### Tier C 쓸 때만 비용 (선택사항)

| 도구 | 가격 | 특징 | 출력 |
|---|---|---|---|
| **Nanobanana 2** (Gemini 2.5 Flash Image) | **$0.039/장** (≈55원) | 캐릭터 일관성, 레퍼런스 이미지로 브랜드 톤 유지 | PNG (투명 지원) |
| **Recraft V4** | **~$0.04/장** (≈56원) | **유일한 프로덕션급 SVG 출력** → 로고/아이콘 최적 | SVG + PNG |
| Midjourney | 구독제 | 분위기 중심 | PNG |

> SKILL.md 원문: *"Most builds are typography-only and never touch this file."*
> → **실제로 Tier C까지 갈 일이 거의 없음**

### 유일한 실제 비용 = AI 구독료 + 토큰 소모

| 항목 | 비용 |
|---|---|
| Claude Code Pro | $20/월 |
| Claude Code Max | $100~200/월 |
| Cursor Pro | $20/월 |
| Anthropic API | 사용량 과금 |

**토큰 소모량:** SKILL.md 67KB(≈2만 토큰) + 빌드당 reference 5~10개
→ 한 번 빌드에 **5~8만 토큰** 가능

Hallmark 자체 토큰 절약 규칙:
- "slop-test.md는 Step 7에서만 로드" (미리 읽으면 7K 낭비)
- "macrostructure 인덱스만 읽고 고른 1개만 로드" (전체 로드는 37KB 낭비)
- "component-cookbook 전체 로드는 **스킬 최대 토큰 낭비**"
- *"over-eager loading is the largest avoidable cost of running Hallmark"*

### 보안

```
✅ 외부 서버 전송: 없음
✅ 텔레메트리/추적: 없음
✅ 실행 코드: 없음 (마크다운뿐)
✅ 네트워크: study URL 모드의 WebFetch만 (AI 자체 기능)
✅ 코드베이스 안전장치:
   - 프로덕션 파일/라우트/컴포넌트 디렉토리 삭제 금지
   - globals.css 는 append-only (@tailwind 지시문 보존)
   - 편집 전 수정/생성/삭제 파일 목록 선언, 삭제는 명시적 승인 필요
   - PDF/README/.md 브리프는 참고자료로만 (verbatim 복사 금지)
```

---

## 13. AI 에이전트 구축에 도움이 되는가

### 결론: **도움됨. 3가지 다른 의미로.**

### 의미 ① "에이전트 설계의 교재" (가장 큰 가치 ⭐⭐⭐⭐⭐)

| # | Hallmark 패턴 | 왜 중요 | 내 에이전트 적용법 |
|---|---|---|---|
| 1 | **Progressive Disclosure** | SKILL.md는 라우터만, 상세는 reference로 분리 | 프롬프트를 거대 한 덩어리로 안 쓰고 "인덱스 + 온디맨드 로드" → 토큰 급감 |
| 2 | **강제 선언 (Say-it-out-loud)** | "코드 전에 '골격: X' 라고 말로 선언하라" | LLM이 머릿속에서 몰래 기본값 고르는 걸 차단. **출력 강제 = 행동 강제** |
| 3 | **사후 검증 게이트** | 58개 질문에 전부 "아니오" | 품질 검증을 체크리스트화. 애매한 "잘 해줘"보다 100배 효과 |
| 4 | **자가채점 + 재작업 루프** | 6축 1~5점, 3점 미만 revision | self-critique 루프의 가장 깔끔한 구현 |
| 5 | **상태 지속** | `.hallmark/log.json` 기록 → 다음 실행에서 읽음 | 세션을 넘는 에이전트 메모리. 파일 하나로 구현 |
| 6 | **멱등성 캐시** | preflight.json + mtime 비교 | 비싼 작업의 조건부 재실행 |
| 7 | **스코프 라우팅** | "버튼 하나" 요청엔 페이지 장치 전부 끔 | 요청 규모별 파이프라인 분기 → 과잉 처리 방지 |
| 8 | **안전 레일** | 삭제 금지 + 파일 목록 선언 후 승인 | destructive action 가드레일 설계 |
| 9 | **거부 레이어** | study가 유료 템플릿/픽셀 복제 거부 | 윤리·법적 refusal layer 구현 |
| 10 | **출력 계약** | 도장 형식, 프리뷰 6불릿, 발행 규칙 | 에이전트 출력을 파싱 가능한 구조로 강제 |
| 11 | **다양화 알고리즘** | 3축 중 1축 이상 달라야 | mode collapse(평균 회귀) 방지 구체적 알고리즘 |
| 12 | **비용 명시** | "이 파일 미리 로드하면 7K 토큰 낭비" | 프롬프트 안에 비용 의식 심기 |

> **Hallmark의 진짜 가치는 "디자인"이 아니라 이 12가지 패턴.**
> 그대로 베껴서 다른 도메인 스킬 만들면 바로 먹힘.

### 의미 ② "에이전트의 프론트엔드 담당" (⭐⭐⭐⭐)

```
에이전트 제품 개발 흐름:
  ① 백엔드/에이전트 로직 → Claude Code
  ② UI 생성            → Claude Code + Hallmark ⭐
  ③ 품질 검사           → hallmark audit
  ④ 디자인 시스템 고정   → design.md → 전 페이지 일관성
```

### 의미 ③ "멀티 에이전트 구조의 참고 모델" (⭐⭐⭐)

```
          ┌─ Designer Agent  (기본 빌드)   ← SKILL.md Step 0~7
Router ───┼─ Auditor Agent   (audit)      ← verbs/audit.md
  ↑       ├─ Refactor Agent  (redesign)   ← verbs/redesign.md
  │       └─ Analyst Agent   (study)      ← study.md
  └── 공유 메모리: .hallmark/log.json + design.md
```
→ **generator-critic 루프** 패턴. Designer가 만들고 Auditor가 채점, 3점 미만이면 재작업.

### 한계

| 한계 | 설명 |
|---|---|
| 프론트엔드 전용 | 백엔드/오케스트레이션/툴콜 설계엔 직접 도움 X |
| 검증이 자율적 | 58게이트를 모델이 스스로 체크. **코드로 강제 안 함** |
| 렌더 결과를 못 봄 | 실제 브라우저 화면 미확인 (← MCP 서버로 해결 가능) |
| 토큰 비용 | 에이전트 루프에 넣으면 호출마다 큰 프롬프트 |

---

## 14. React / PHP 로 만들 수 있는가

### 해석 A: "Hallmark로 React/PHP 코드를 만들 수 있나?" → **⭕ YES**

Step 0에서 프레임워크 자동 감지:
`Next.js(next) · Astro · Vue · Svelte/SvelteKit · Remix · Tailwind · 바닐라 HTML`

**React/Next.js**
- package.json 읽어 next/font, framer-motion 자동 감지
- 기존 팔레트/폰트 보존
- `app/globals.css` 는 append-only (@tailwind 지시문 보존)
- Tailwind v4 `@theme` 형태 토큰 발행 가능

**PHP (Laravel / WordPress)**
- 프레임워크 감지 목록에 없어 '바닐라 HTML' 폴백
- 산출물이 자체 완결 HTML+CSS → Blade / WP 테마에 그대로 투입
- Laravel: `resources/views/*.blade.php` + `public/css/tokens.css`
- WordPress: `wp-content/themes/내테마/` (style.css + header/footer.php)
- 💡 "이건 Laravel Blade 프로젝트야"를 먼저 말해주면 Blade 문법으로 뽑아줌

⚠️ **주의:** `site/examples/` 19개 전부 바닐라 HTML+CSS.
**React/Vue 완성 예제 0개** → 토큰 매핑 규칙은 있지만 검증된 결과물 예시는 없음.

### 해석 B: "Hallmark 같은 걸 React/PHP로 직접 만들 수 있나?" → **⭕ YES (수익화 포인트!)**

#### React로 (⭐⭐⭐⭐⭐)

**① 테마 플레이그라운드** — `site/css/tokens.css` 그대로 import 하면 21테마 즉시 동작
```jsx
function ThemePlayground() {
  const [theme, setTheme] = useState('specimen');
  const THEMES = ['specimen','midnight','brutal','garden','atelier','newsprint',
                  'terminal','manifesto','almanac','sport','studio','riso','bloom',
                  'coral','cobalt','aurora','editorial','carnival','lumen','hum','grid'];
  useEffect(() => { document.documentElement.dataset.theme = theme; }, [theme]);
  return (
    <>
      <select value={theme} onChange={e => setTheme(e.target.value)}>
        {THEMES.map(t => <option key={t} value={t}>{t}</option>)}
      </select>
      <PreviewCanvas />
    </>
  );
}
```

**② 슬롭 테스트 린터** — 58게이트 중 약 35개는 정적 검사 가능
```js
const GATES = [
  { id: 1,  name: 'Inter 폰트',        test: css => /font-family:[^;]*\b(Inter|Roboto|Poppins|Lato|Open Sans)\b/i.test(css) },
  { id: 2,  name: '보라→파랑 그라데',   test: css => /linear-gradient[^;]*(#6[0-9a-f]{5}|purple|violet)/i.test(css) },
  { id: 10, name: 'transition: all',   test: css => /transition:\s*all/i.test(css) },
  { id: 11, name: 'hover:scale-105',   test: css => /hover:scale-105/.test(css) },
  { id: 14, name: '레이아웃 애니메이션', test: css => /transition:[^;]*\b(width|height|top|left|margin|padding)\b/.test(css) },
  { id: 20, name: '도장 누락',          test: css => !/Hallmark · macrostructure:/.test(css) },
  { id: 22, name: 'chroma 0 회색',     test: css => /oklch\(\s*[\d.]+%?\s+0\s+/.test(css) },
  { id: 24, name: '스케일 밖 패딩',     test: css => /padding:\s*\d*[13579]px/.test(css) },
];
export function slopTest(css) {
  const fails = GATES.filter(g => g.test(css));
  return { score: `${GATES.length - fails.length}/${GATES.length}`, fails };
}
```

**③ 프롬프트 생성기** — 골격 21 × 테마 21 × 장르 4 = **1,764 조합** UI 선택기
**④ 갤러리** — examples 19개를 Next.js로 재구성

추천 스택: `Next.js 15 + TS + tokens.css import + Monaco Editor + Zustand + Vercel`

#### PHP로 (⭐⭐⭐)

**① WordPress 플러그인 "Hallmark Slop Checker"** 💰
```php
<?php
/** Plugin Name: Hallmark Slop Checker */
add_action('admin_menu', function () {
  add_menu_page('Hallmark', 'Hallmark', 'manage_options',
                'hallmark', 'hm_render_page', 'dashicons-art');
});
function hm_gates() {
  return [
    1  => ['name' => 'Inter 폰트',      're' => '/font-family:[^;]*\b(Inter|Roboto|Poppins)\b/i'],
    2  => ['name' => '보라 그라데이션',  're' => '/linear-gradient[^;]*(purple|violet|#6[0-9a-f]{5})/i'],
    10 => ['name' => 'transition: all', 're' => '/transition:\s*all/i'],
    22 => ['name' => 'chroma 0 회색',   're' => '/oklch\(\s*[\d.]+%?\s+0\s+/'],
  ];
}
function hm_scan($css) {
  $fails = [];
  foreach (hm_gates() as $id => $g)
    if (preg_match($g['re'], $css)) $fails[] = "게이트 {$id}: {$g['name']}";
  return $fails;
}
```
> WordPress는 전 세계 웹사이트의 **43%** → 플러그인 시장 거대

**② Laravel SaaS** — Cashier 구독 과금 + 팀 관리 + PDF 리포트
**③ WooCommerce 테마 마켓플레이스**

### 선택 가이드

| 만들 것 | React | PHP | 이유 |
|---|---|---|---|
| 테마 플레이그라운드 | ⭐⭐⭐⭐⭐ | ⭐ | 실시간 인터랙션 |
| 슬롭 테스트 웹도구 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | 클라이언트 검사 = 서버비 0 |
| WordPress 플러그인 | ❌ | ⭐⭐⭐⭐⭐ | WP는 PHP |
| 구독형 SaaS | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Laravel Cashier |
| 갤러리/쇼케이스 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | Next SSG 무료 배포 |
| CLI 도구 | Node ⭐⭐⭐⭐⭐ | ⭐⭐ | npx 배포 |

---

## 15. 유튜브 강의 제작 가능성

### 결론: **완전 가능. 소재가 이미 레포에 준비돼 있음.**

### 발견: `docs/talk-slides.md` = 발표 슬라이드 14장 원고

```
제목: "Stop letting your agents ship ugly UIs."

01 · 커버
02 · 문제        — "지금 네 에이전트가 뱉는 게 이거다"
03 · 약속        — "이걸 뱉을 수도 있었다"
04 · 왜          — "모델은 학습 데이터의 평균을 출력한다"
05 · 섹션 오프너  — "이걸 고치는 7가지"
06 · Fix 01     — 진짜 컴포넌트 라이브러리를 써라
07 · Fix 02     — 디자인 시스템을 고정하라
08 · Fix 03     — 기능 목록이 아니라 '형태'를 요청하라
09 · Fix 04     — 설명하지 말고 스크린샷을 붙여라
10 · Fix 05     — 하지 말 것을 알려줘라
11 · Fix 06     — 모든 인터랙티브 요소는 8개 상태를 가진다
12 · Fix 07     — 출력 전에 스스로 채점시켜라
13 · 전체 플레이북 — "한 단락에 다 들어간다" (system_prompt.md)
14 · 도구        — "무기를 골라라"
```
→ **그대로 영상 1편 대본.** 번역만 하면 됨.

### 추천 커리큘럼 10편

| 편 | 제목 | 길이 | 썸네일 후킹 |
|---|---|---|---|
| 00 | 【예고】AI가 만든 UI가 왜 다 똑같이 생겼을까? | 3분 | Before/After 나란히 |
| 01 | 보라색 그라데이션의 저주 — AI 티 7가지 해부 | 15분 | "이거 보이면 AI임" |
| 02 | Hallmark 설치 & 첫 빌드 (실습) | 12분 | 터미널 한 줄 → 결과 |
| 03 | 21개 골격 완전정복 — 왜 '편지' 랜딩페이지가 먹히나 | 20분 | 21개 썸네일 그리드 |
| 04 | 58개 슬롭테스트 전부 읽어보기 | 25분 | 체크리스트 스크롤 |
| 05 | `hallmark audit`으로 내 사이트 진단하기 | 15분 | 실제 사이트 처형 |
| 06 | `hallmark study` — 린어/스트라이프 DNA 뽑기 | 18분 | 유명 사이트 분해 |
| 07 | OKLCH 완전정복 — 왜 HEX를 버려야 하나 | 15분 | 색공간 비교 |
| 08 | 8개 상태 + 마이크로인터랙션 룰 | 18분 | 상태 데모 |
| 09 | 【고급】Hallmark 패턴으로 내 스킬 만들기 | 25분 | 12패턴 다이어그램 |
| 10 | 【고급】MCP 라이브 프리뷰 서버 직접 만들기 | 30분 | 자동 수정 루프 |

### 왜 강력한가 (5가지)

| 이유 | 설명 |
|---|---|
| ① 시각적 Before/After 압도적 | examples 19 + _tests 18 + 스크린샷 18 = **소재 55개 이상 준비됨** |
| ② "T키로 테마 21개 순환" | 영상에서 보여주면 임팩트 폭발 |
| ③ 즉시 재현 가능 | recipes.md 검증 프롬프트 9개 → 시청자 따라하기 = 체류시간 + 구독 |
| ④ 논쟁적 제목이 먹힘 | "너의 AI는 촌스럽다" → 클릭률 |
| ⑤ 한국어 콘텐츠 0개 | **현재 Hallmark 한국어 영상 전무.** 선점 효과 ⭐⭐⭐⭐⭐ |

### 법적 체크 (MIT)

| 항목 | 가능? | 조건 |
|---|---|---|
| 코드/문서 화면 노출 | ⭕ | MIT |
| 예제 사이트 시연 | ⭕ | MIT |
| talk-slides.md 내용 사용 | ⭕ | MIT (출처 표기 권장) |
| 영상 수익화 (광고/멤버십) | ⭕ | MIT는 상업적 사용 허용 |
| 강의 유료 판매 | ⭕ | MIT (단 "공식 강의" 사칭 ❌) |
| 개선 버전 배포 | ⭕ | MIT + 저작권 고지 포함 |

README 원문: **"MIT. Use it, fork it, ship it."**
⚠️ **"Powered by Together AI"** + 원작자 크레딧은 영상 설명란에 꼭 표기

### 제작 팁

| 팁 | 설명 |
|---|---|
| 화면 구성 | 왼쪽 터미널(Claude Code) + 오른쪽 브라우저(localhost:4173) 분할 |
| 킬러 장면 | ① T키 테마 순환 ② audit 펀치리스트 ③ Before/After 전환 |
| 챕터 마커 | 긴 영상 타임스탬프 → 체류시간 ↑ |
| 설명란 번들 | 번역 노션 + 프롬프트 모음 + 포크 링크 |
| 시리즈 브랜딩 | 「AI 티 벗기기」 같은 통일 네이밍 |
| 썸네일 공식 | 왼쪽=보라그라데(❌) / 오른쪽=Hallmark(⭕) + 큰 글씨 |

---

## 16. 수익화 아이디어 11개 상세

### 시장 기회

| 신호 | 근거 |
|---|---|
| ① AI 코딩 도구 폭발 | Claude Code, Cursor, Copilot, Windsurf... 사용자 수백만 |
| ② "AI 티"가 실제 비즈니스 문제 | 투자자/고객 신뢰 하락 |
| ③ 한국어 콘텐츠 공백 | Hallmark 한국어 자료 **현재 0개** |
| ④ MIT 라이선스 | 포크·개선·판매 전부 합법 |
| ⑤ 로드맵 미구현 다수 | MCP 서버, variant, data-viz → **선점 가능** |
| ⑥ 디자이너 고용 비용 | 랜딩페이지 외주 300~1,000만원 → 대체 수요 |

---

### Tier 1 — 지금 당장 (1~4주)

#### 💰 1. 한국어 완전판 + 한글 타이포 룰 ⭐⭐⭐⭐⭐ 【1순위】

난이도 최저 × 선점 효과 최대 × 다른 모든 수익화의 기반

```
hallmark-ko/
├── skills/hallmark-ko/
│   ├── SKILL.md                      ← 전체 한국어 번역
│   └── references/
│       ├── (107개 파일 번역)
│       ├── korean-typography.md       ⭐ 신규! 오리지널 가치
│       └── korean-anti-patterns.md    ⭐ 신규!
├── docs/ko/
└── README.ko.md
```

**`korean-typography.md` 초안 (진짜 차별점!)**

```markdown
# 한글 타이포그래피

## 금지 폰트 (한글판 "Inter-everywhere")
- 맑은 고딕 / 돋움 / 굴림 / 바탕 (시스템 기본 = AI 티)
- Noto Sans KR 단독 사용 (라틴의 Inter 포지션)

## 추천 페어링
| 디스플레이 | 본문 | 분위기 |
|---|---|---|
| 프리텐다드 800 | 프리텐다드 400 | 모던 미니멀 (가장 안전) |
| 나눔명조 | 프리텐다드 | 에디토리얼 |
| 에스코어드림 9 | IBM Plex Sans KR | 브루탈 |
| 잉크립퀴드 / 주아 | 고운돋움 | 플레이풀 |
| 리디바탕 | 프리텐다드 | 럭셔리 |
| GmarketSans Bold | 프리텐다드 | 스포츠/임팩트 |

## 한글 전용 규칙
- `word-break: keep-all` ⭐ 필수 (한글은 어절 단위로 끊어야 함)
- line-height: 라틴 1.5 → **한글 1.6~1.75** (받침 때문)
- letter-spacing: 한글은 **-0.01em ~ -0.02em**
- measure: 라틴 45~75ch → **한글 25~40ch** (글자 폭이 넓음)
- 한글 디스플레이는 **Bold 700 이상**에서만 임팩트
- 숫자는 라틴 폰트로 분리 권장 (font-feature-settings + 폴백 체인)

## 한글 안티패턴
- ❌ 한글에 text-transform: uppercase (효과 없음, 영문 혼용 시 참사)
- ❌ 한글 이탤릭 (가짜 기울임 → 깨짐) ⭐ 라틴보다 더 치명적
- ❌ 한글에 font-stretch (지원 폰트 거의 없음)
- ❌ 영/한 혼용 시 폰트 크기 미조정 (한글이 커 보임 → 한글만 0.95em)
- ❌ 자동 줄바꿈 방치 ("안녕하세"/"요" 깨짐 → keep-all 필수)
```

**실행 순서**
1. 포크에 `ko` 브랜치
2. SKILL.md 먼저 번역 (80% 가치)
3. `korean-typography.md` 작성 ← 차별점
4. anti-patterns.md, slop-test.md 번역
5. README.ko.md + 설치 가이드
6. 원작 레포에 PR 또는 별도 배포
7. 홍보: GeekNews · 디스콰이엇 · OKKY · velog

---

#### 💰 2. 유튜브 + 유료 강의 번들 ⭐⭐⭐⭐⭐

```
【무료】 유튜브 10편         → 인지도 + 신뢰
   ↓
【무료】 번역 노션 + 프롬프트팩 → 이메일 수집
   ↓
【유료】 심화 강의 + 커뮤니티   → 💰
```

| 상품 | 가격 | 내용 | 타깃 |
|---|---|---|---|
| 무료 | ₩0 | 유튜브 10편 + 번역 노션 | 전체 |
| 베이직 | ₩49,000 | 강의 5시간 + 프롬프트 50개 + 치트시트 | 개인 개발자 |
| 프로 | ₩149,000 | 베이직 + 실습 3개 + 디스코드 + Q&A | 프리랜서 |
| 팀 | ₩490,000 | 프로 + 2시간 워크샵 + design.md 1개 제작 | 스타트업 |

**보수적 시뮬레이션**
```
유튜브 10편 × 평균 5,000뷰 = 5만뷰
→ 노션 방문 3% = 1,500명
→ 이메일 전환 30% = 450명
→ 유료 전환 5% = 22명 × 평균 ₩80,000 = 💰 176만원
+ 유튜브 광고: 5만뷰 × CPM ₩3,000 = 💰 15만원
```
**낙관:** 1편 10만뷰 → 유료 100명+ → 💰 800만원+

| 플랫폼 | 수수료 | 장점 |
|---|---|---|
| 인프런/인클래스 | 30~50% | 트래픽 제공 |
| 패스트캠퍼스 | 협의 | 브랜드 신뢰 |
| Gumroad/Lemon Squeezy | 5~10% | 마진 최대 |
| 탈잉/클래스101 | 30~40% | 비개발자 접근 |

> 추천: 첫 상품은 인프런(검증) → 검증 후 자체 판매(마진)

---

#### 💰 3. 프리랜스 "AI 슬롭 제거" 서비스 ⭐⭐⭐⭐ 【현금 흐름 1순위】

| 패키지 | 가격 | 작업 | 소요 |
|---|---|---|---|
| 진단만 | ₩150,000 | audit + 등급 리포트(PDF) + 우선순위 | 2시간 |
| 1페이지 리디자인 | ₩800,000 | redesign + 수작업 폴리시 + 반응형 검증 | 2~3일 |
| 디자인 시스템 구축 | ₩2,500,000 | design.md + tokens.css + 4포맷 + 가이드 | 1~2주 |
| 전체 사이트 (5p) | ₩5,000,000 | 시스템 + 5페이지 + 일관성 검증 | 3~4주 |
| 월 리테이너 | ₩1,500,000/월 | 신규 2페이지 + 상시 audit + Slack 지원 | 월 |

**타깃:** AI로 MVP 만든 초기 스타트업 / 개발자 1인 창업자 / 에이전시 하청

**영업 멘트**
> "AI로 만든 랜딩페이지, 투자자가 'AI로 만드셨죠?' 라고 물어본 적 있으세요?
> 보라 그라데이션, Inter 폰트, 3칸 카드 그리드 — 이 3개만 바꿔도 완전히 달라집니다.
> 58개 체크리스트로 진단해드립니다. 진단 15만원, 리디자인 80만원부터."

**차별화:** "58개 게이트 통과 보증" = 측정 가능한 약속 / Before-After 리포트 /
design.md 납품 → 고객 자립 → 신뢰 ↑ → 리테이너 전환

**채널:** 크몽 · 위시켓 · 숨고 · 디스콰이엇 · 트위터/스레드 · 유튜브 설명란

---

#### 💰 4. 프롬프트 팩 / 템플릿 번들 ⭐⭐⭐

| 상품 | 가격 | 내용 |
|---|---|---|
| 한글 프롬프트 팩 50 | $19 | 업종별 검증 프롬프트 50개 (카페/병원/학원/쇼핑몰/SaaS/포트폴리오) |
| 테마 치트시트 PDF | $9 | 21테마 × 3축 비교표 + 골격 21개 선택 가이드 (A3) |
| 슬롭테스트 체크리스트 | $12 | 58게이트 노션 템플릿 (체크박스 + 수정법) |
| 한국형 랜딩 템플릿 10종 | $49 | 한글 최적화 HTML+CSS 10개 (keep-all, 프리텐다드) |
| 올인원 번들 | $79 | 전부 + 평생 업데이트 |

판매처: Gumroad · Lemon Squeezy · 크몽 · 자체
예상: 월 20~50건 × $30 = 💰 **월 60~150만원** (트래픽 확보 후)

---

### Tier 2 — 중기 (1~3개월, 개발 필요)

#### 💰 5. MCP 라이브 프리뷰 서버 ⭐⭐⭐⭐⭐ 【최고 임팩트·선점 가능】

로드맵 "Later"에 있고 **아직 아무도 안 만듦**

**해결하는 문제:** 58게이트를 실제 화면 안 보고 CSS만 보고 검사하는 약점

```
┌──────────────────────────────────────────────────┐
│  hallmark-preview-mcp  (Node + Playwright)       │
├──────────────────────────────────────────────────┤
│  ① render(path, widths=[320,375,414,768,1440])   │
│  ② slop_check(path)                              │
│     · 정적 35게이트 (정규식)                       │
│     · 동적 검사 — 실제 측정!                       │
│       가로 스크롤 / 클릭텍스트 2줄 / 대비 / 포커스링 │
│  ③ diff(before, after) → 시각 비교                │
│  ④ critique(path) → 스크린샷을 AI에 재입력         │
└──────────────────────────────────────────────────┘
          ↓
   Claude Code 자동 루프:
   빌드 → render → slop_check → 실패 → 수정 → 재검사
```

```js
// 핵심 로직 스케치
import { chromium } from "playwright";

async function slopCheck(path) {
  const browser = await chromium.launch();
  const results = [];
  for (const w of [320, 375, 414, 768]) {
    const page = await browser.newPage({ viewportSize: { width: w, height: 900 }});
    await page.goto(`file://${path}`);

    // 게이트 34: 가로 스크롤 — 실제 측정 (코드 검사로는 불가능!)
    const overflow = await page.evaluate(() =>
      document.documentElement.scrollWidth > window.innerWidth);
    if (overflow) results.push({ gate: 34, width: w, fail: true });

    // 게이트 49: 클릭 텍스트 2줄 — 실제 측정
    const twoLine = await page.evaluate(() =>
      [...document.querySelectorAll('a,button')].some(el => {
        const lh = parseFloat(getComputedStyle(el).lineHeight);
        return el.getBoundingClientRect().height > lh * 1.6;
      }));
    if (twoLine) results.push({ gate: 49, width: w, fail: true });
  }
  await browser.close();
  return results;
}
```

| 티어 | 가격 | 내용 |
|---|---|---|
| OSS | 무료 | 로컬 MCP 서버 (스타 수집, 신뢰 구축) |
| Pro | $19/월 | 클라우드 렌더 + 히스토리 + 팀 공유 + 비주얼 리그레션 |
| Team | $99/월 | CI 연동 + PR 코멘트 + 대시보드 + 커스텀 게이트 |
| Enterprise | 협의 | 온프레미스 + 사내 디자인 시스템 게이트 |

> 전략: OSS로 "Hallmark 생태계 핵심 도구" 포지션 → 클라우드 과금 (개발자 도구 정석)

---

#### 💰 6. "AI 티 진단" SaaS ⭐⭐⭐⭐⭐ 【바이럴 가능】

```
┌─────────────────────────────────────────────┐
│  🔍 Is Your Site AI-Generated?              │
│  [ https://example.com          ] [ SCAN ]  │
├─────────────────────────────────────────────┤
│  AI SLOP SCORE:  73 / 100   😬              │
├─────────────────────────────────────────────┤
│  🔴 CRITICAL (3)                            │
│  · 보라→파랑 그라데이션 히어로 (게이트 2)      │
│  · Inter 폰트 단독 사용 (게이트 1)            │
│  · 3등분 아이콘 카드 그리드 (게이트 3)         │
│  🟡 MAJOR (5)  · transition: all 17곳 ...    │
│  🔵 MINOR (4)  ...                          │
├─────────────────────────────────────────────┤
│  [ 상세 PDF — 무료 ] [ 수정 가이드 — Pro ]    │
│  [ 트위터에 점수 공유 🐦 ]  ← 바이럴 장치      │
└─────────────────────────────────────────────┘
```

**바이럴 설계:** 점수 공유 OG 이미지 자동생성 / "유명 사이트 랭킹" 페이지 / "경쟁사 점수 보기"

**스택:** `Next.js 15 + Vercel → /api/scan (Playwright/Browserless)
→ 정적 35 정규식 + 동적 10 측정 → @vercel/og → Supabase + Stripe`

| 티어 | 가격 | 내용 |
|---|---|---|
| Free | ₩0 | 월 3회, 점수 + critical만 |
| Pro | $12/월 | 무제한, 전체 리포트, 수정 가이드, PDF |
| Agency | $49/월 | 화이트라벨, 50사이트 모니터링, API |
| API | $0.05/스캔 | 개발자용 |

예상: 월 1만 스캔 → Pro 1% = 100명 × $12 = 💰 **월 $1,200 (약 170만원) MRR**

---

#### 💰 7. GitHub Action — PR 자동 슬롭 검사 ⭐⭐⭐⭐

```yaml
# .github/workflows/hallmark.yml
name: Hallmark Slop Check
on: [pull_request]
jobs:
  slop-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: bmshin94/hallmark-action@v1
        with:
          paths: 'src/**/*.{css,tsx,vue}'
          fail-on: critical
          comment: true
          baseline: .hallmark/baseline.json
```

PR 코멘트로 게이트별 위반 위치(파일:줄) 테이블 자동 게시

| 티어 | 가격 |
|---|---|
| OSS 레포 | 무료 (마케팅) |
| 프라이빗 레포 | $29/월 per org |
| Enterprise | $199/월 (커스텀 게이트 + SSO + 온프레미스) |

> GitHub Marketplace 등록 → 발견 가능성 공짜

---

#### 💰 8. React/Vue 컴포넌트 라이브러리 ⭐⭐⭐⭐

Hallmark 최대 공백 메우기 (examples 19개 전부 바닐라 = React 예제 0개)

```
@hallmark/react
├── tokens/        ← 21테마 CSS 변수 + TS 타입
├── primitives/    ← Button, Input, Card... (8상태 전부!)
├── sections/      ← Hero(9) Nav(14) Footer(8) Feature(6)
├── macros/        ← 21골격을 레이아웃 컴포넌트로
└── ThemeProvider  ← data-theme 스위처
```
```tsx
<ThemeProvider theme="lumen">
  <NavFloatingPill brand="Tally" links={[...]} />
  <MarqueeHero headline="Bill what your customers actually use" polish="HP1" />
  <FooterStatement statement="Metering, honestly." />
</ThemeProvider>
```

| 티어 | 가격 |
|---|---|
| Core (MIT) | 무료 — primitives + 5테마 |
| Pro (상용) | **$149 평생/개발자** — 21테마 + 50컴포넌트 + 21골격 |
| Team | **$599** — 5석 + Figma 파일 + 우선 지원 |

벤치마크: Tailwind UI $299, shadcn 블록 유료팩 $99~249 → $149 합리적
예상: 월 10~30건 × $149 = 💰 **월 200~600만원** (인지도 확보 후)

---

### Tier 3 — 장기 / 큰 베팅 (3~12개월)

#### 💰 9. 도메인 특화 스킬 시리즈 ⭐⭐⭐⭐

| 스킬명 | 도메인 | 왜 팔리나 |
|---|---|---|
| **Ledger** | 대시보드/차트 | Hallmark 로드맵 `data-viz.md` 미구현! 차트가 AI 티 1순위 |
| **Clinic** | 의료/병원 UI | 접근성 규제 + 신뢰감 → 돈 쓰는 업종 |
| **Vault** | 금융/핀테크 | 신뢰감 디자인 + 규제 준수 |
| **Hangeul** | 한글 타이포 전문 | Hallmark 미커버 영역 (아이디어 1 확장) |
| **Scribe** | 블로그/뉴스레터 | 읽기 경험 특화 |
| **Commerce** | 이커머스 | 전환율 패턴 + 상품 그리드 |
| **Deck** | 발표 슬라이드 | AI 슬라이드가 제일 촌스러움 |

스킬당 $29~79 또는 전체 번들 $199

#### 💰 10. Figma 플러그인 — 양방향 동기화 ⭐⭐⭐⭐

```
Figma 변수 ←──→ tokens.css ←──→ 코드
 (디자이너)      (Hallmark)      (개발자)
```
- Figma → tokens.css 익스포트 (21테마)
- tokens.css → Figma 변수 임포트
- Figma 프레임에 slop test (레이어 구조 분석)
- 21골격 Figma 템플릿

가격: $10~30/월 또는 일회성 $49 / 장점: Figma Community 발견 가능성 높음

#### 💰 11. 올인원 SaaS "Hallmark Studio" ⭐⭐⭐⭐⭐

```
① 브리프 입력 → AI 골격·테마 추천 (3안 비교)
② 라이브 프리뷰 (4뷰포트 동시 + T키 테마 순환)
③ 자동 슬롭 테스트 (실제 렌더 기반 58게이트)
④ 디자인 시스템 생성 → 4포맷 익스포트
⑤ 코드 익스포트: HTML / React / Vue / Next / Laravel
⑥ 팀 공유 + 버전 관리 + 코멘트
⑦ Figma 플러그인 연동
⑧ GitHub Action 연동
```
Free(3프로젝트) / Pro $29월 / Team $99월 / Enterprise 협의
목표: 유료 1,000명 × $29 = 💰 **월 $29,000 (약 4,000만원)**

⚠️ 큰 베팅. Tier 1·2로 수요 검증 후 진행

---

### 종합 비교표

| # | 아이디어 | 난이도 | 초기투자 | 수익시점 | 잠재력 | 순위 |
|---|---|---|---|---|---|---|
| 1 | 한국어판 + 한글 타이포 | ⭐ | 없음 | 간접 | ⭐⭐⭐⭐ | 🥇 1위 |
| 3 | 프리랜스 슬롭 제거 | ⭐ | 없음 | **즉시** | ⭐⭐⭐⭐ | 🥈 2위 |
| 2 | 유튜브 + 강의 | ⭐⭐ | 장비/시간 | 1~2개월 | ⭐⭐⭐⭐⭐ | 🥉 3위 |
| 4 | 프롬프트 팩 | ⭐ | 없음 | 1개월 | ⭐⭐⭐ | 4위 |
| 5 | MCP 프리뷰 서버 | ⭐⭐⭐⭐ | 개발시간 | 3개월 | ⭐⭐⭐⭐⭐ | 5위 ⭐선점 |
| 6 | AI 티 진단 SaaS | ⭐⭐⭐⭐ | 서버비 | 3~6개월 | ⭐⭐⭐⭐⭐ | 6위 💥바이럴 |
| 7 | GitHub Action | ⭐⭐⭐ | 개발시간 | 3개월 | ⭐⭐⭐⭐ | 7위 |
| 8 | React 컴포넌트 라이브 | ⭐⭐⭐ | 개발시간 | 3~4개월 | ⭐⭐⭐⭐ | 8위 |
| 9 | 도메인 특화 스킬 | ⭐⭐⭐ | 집필시간 | 4개월 | ⭐⭐⭐⭐ | 9위 |
| 10 | Figma 플러그인 | ⭐⭐⭐⭐ | 개발시간 | 4~6개월 | ⭐⭐⭐⭐ | 10위 |
| 11 | Hallmark Studio | ⭐⭐⭐⭐⭐ | 큼 | 6~12개월 | ⭐⭐⭐⭐⭐ | 11위 (최종) |

---

## 17. 추천 실행 로드맵

```
┌─ 1~2주 ──────────────────────────────────────────┐
│ ① 한국어 번역 (SKILL.md + 핵심 reference 10개)     │
│ ② korean-typography.md 작성 ⭐ 차별점              │
│ ③ 유튜브 1편 공개                                 │
│ 👉 목표: GitHub 스타 50 + 유튜브 3,000뷰           │
│ 💰 수익: 0 (투자 기간)                             │
└──────────────────────────────────────────────────┘
            ↓
┌─ 3~6주 ──────────────────────────────────────────┐
│ ④ 유튜브 2~5편 + 프롬프트 팩 50개                  │
│ ⑤ Gumroad 프롬프트 팩 판매 시작 ($19)             │
│ ⑥ 크몽/위시켓 "AI슬롭 제거" 서비스 등록            │
│ 💰 수익: 50~200만원                               │
└──────────────────────────────────────────────────┘
            ↓
┌─ 2~3개월 ────────────────────────────────────────┐
│ ⑦ MCP 라이브 프리뷰 서버 OSS 공개 ⭐ 선점!          │
│ ⑧ 유튜브 6~10편 완결 + 유료 강의 (인프런)          │
│ ⑨ React 컴포넌트 라이브러리 Core(MIT) 공개         │
│ 💰 수익: 200~500만원/월                            │
└──────────────────────────────────────────────────┘
            ↓
┌─ 4~6개월 ────────────────────────────────────────┐
│ ⑩ "AI 티 진단" SaaS 런치 (바이럴)                  │
│ ⑪ GitHub Action 마켓플레이스 등록                  │
│ ⑫ React 라이브러리 Pro 판매 ($149)                │
│ 💰 수익: 500~1,500만원/월                          │
└──────────────────────────────────────────────────┘
            ↓
┌─ 6~12개월 ───────────────────────────────────────┐
│ ⑬ Hallmark Studio SaaS (통합 플랫폼)              │
│ ⑭ 도메인 특화 스킬 시리즈                          │
│ ⑮ Figma 플러그인                                  │
│ 💰 목표: MRR $10,000+ (약 1,400만원/월)            │
└──────────────────────────────────────────────────┘
```

### 최종 추천 — 딱 3개만

1. **한국어판 + `korean-typography.md`** — 투자 0원, 선점 효과 최대
2. **유튜브 1편** 「AI가 만든 UI가 왜 다 똑같이 생겼을까?」 — talk-slides.md 번역만 하면 대본 완성
3. **크몽 "AI슬롭 진단 15만원"** — 현금 흐름 만들기

이 3개가 돌면 나머지는 자연스럽게 따라옴.
**MCP 프리뷰 서버**는 로드맵에 있고 아무도 안 만들었으니 여유 생기면 꼭.

---

## 18. 한계와 리스크

### Hallmark 자체의 한계

| 한계 | 설명 |
|---|---|
| **토큰 많이 먹음** | SKILL.md 67KB(약 9,400단어). reference 포함 980KB. 빌드당 5~8만 토큰 가능 |
| **마크다운 규칙일 뿐** | 코드로 강제 검증 X. **모델이 룰을 안 지키면 그냥 안 지켜짐** |
| **HTML/CSS 중심** | 예제 전부 바닐라. React/Vue 결과물 예시 0개 |
| **렌더 결과를 못 봄** | 실제 브라우저 화면 미확인, CSS 코드만 보고 판단 |
| **질문을 꼭 한 번 함** | Step 1 게이트 때문에 "바로 만들어"가 안 됨 ("go ahead"로 우회) |
| **Nanobanana 훅 미구현** | 로드맵 "Now"에 있음. 현재는 "직접 생성해서 가져와" 수준 |
| **한글 미지원** | 라틴 폰트 전용. 한글 타이포 룰 전무 ← **이게 기회!** |

### 수익화 리스크 & 대응

| 리스크 | 대응 |
|---|---|
| 원작자가 공식 한국어판 낼 수도 | **PR 보내서 공식 기여자 되기** → 오히려 신뢰도 ↑ |
| AI가 알아서 잘 디자인하게 됨 | 중요한 건 "스킬"이 아니라 **"안티패턴 지식"**. 지식은 안 썩음 |
| Hallmark 인기가 안 오름 | "AI 티 제거"라는 **문제**는 Hallmark보다 큼. 문제에 집중 |
| MIT 라이선스 신뢰 문제 | 원작 크레딧 + "Powered by Together AI" 표기 |
| 혼자 다 못함 | 아이디어 1·3부터. 둘 다 혼자 가능 + 투자 0원 |

---

## 19. 로드맵 (원작자 계획)

### Now
- **Nanobanana 훅** — 현재 recommend-only. 프롬프트 작성 → API 호출 → 이미지 수신 →
  빌드에 연결 (프롬프트 해시로 캐시). 이미지 중심 테마 *Plate* 추가 예정

### Next
- **Brand-first flow** — 짧은 제품 설명 → 팔레트·타입·보이스·커스텀 이미지 전체 생성 → design.md 고정
- **Theme-aware motion tokens** — 테마별 `--dur-micro/short/long` (Atelier는 Brutal보다 느리게)
- **`hallmark variant`** — 같은 브리프로 구조적으로 다른 3개 버전 동시 생성
- **Structural cookbook** — 12~20개 완성 지문 + HTML/CSS 스케치
- **Tactile-rebellion reference** — 통제된 불완전성 (손그림 텍스처, 0.5° 기울기)
- **Charts reference (`data-viz.md`)** — AI 차트 티 제거 (무지개 팔레트, 3D 도넛, 이중축 스파게티 금지)
- **Multi-page coherence** — 브랜드 축은 고정, 페이지 보이스 축만 변화
- **`study` 가 내 코드베이스도 읽기** — 세 번째 입력 모드

### Later
- **`hallmark explain`** — 축별로 선택 이유 서술 (스킬이 가르침)
- **Negative-capability rules** — 각 안티패턴이 왜 실패하는지의 지각·인지적 이유
- **Emotion-first prompting** — nostalgic · optimistic · sceptical
- **Sound + haptic policy**
- **Live preview as an MCP server** ⭐ — 파일 감시 → 샌드박스 렌더 → 스크린샷 →
  AI 재입력 자가비평. **생성과 감사의 루프를 닫음**

---

## 부록 · 빠른 참조

### 핵심 링크
- 내 포크: **https://github.com/bmshin94/hallmark**
- 원본: https://github.com/nutlope/hallmark
- 데모: https://www.usehallmark.com
- 설치: `npx skills add nutlope/hallmark`
- 로컬 실행: `npm run serve` → http://localhost:4173 (T키 = 테마 순환)

### 명령 치트시트
```
(기본)                            새 UI 빌드
hallmark audit <파일>             안티패턴 진단 (수정 안 함)
hallmark redesign <파일> [--mood] 구조만 새로
hallmark study <URL|스샷>         DNA 추출
```

### 꼭 읽어볼 파일 Top 5
1. `skills/hallmark/references/anti-patterns.md` — 70+ 안티패턴 (디자인 눈 트임!)
2. `skills/hallmark/references/slop-test.md` — 58게이트
3. `docs/talk-slides.md` — 발표 원고 14장 (유튜브 대본)
4. `docs/recipes.md` — 검증된 프롬프트 9개
5. `site/css/tokens.css` — 21테마 전체 토큰 (React에 그대로 import 가능)

---

*이 문서는 Claude Code(카리나)가 bmshin94/hallmark 레포 288개 파일을 전수조사하여 작성했습니다.*
*Hallmark는 MIT 라이선스이며, Together AI가 제작했습니다.* 💖
