# 오늘의 타로 — 디자인 가이드 (DESIGN.md)

> 한밤의 남색 위에 촛불 같은 금빛 한 점.
> 깊은 미드나이트 잉크가 화면의 무게를 잡고, 금빛 하나가 "지금 이걸 누르세요"를 알려 줍니다. 카드 이름은 크고 굵게 외치듯 보여 줍니다.

**테마:** 라이트 (밝은 바탕 + 어두운 섹션 반전)
**기기:** 모바일 웹 우선 (360–430px 기준, 최대 너비 480px)
**참고 문서:** [TARO_01_PRD](TARO_01_PRD.md) · [TARO_02_기능명세서](TARO_02_기능명세서.md) · [TARO_03_유저플로우](TARO_03_유저플로우.md) · [TARO_04_와이어프레임](TARO_04_와이어프레임.md)
**구현 기준:** Tailwind CSS v4 (`@theme`, CSS 우선 설정) + shadcn/ui (시맨틱 토큰, 기본 컴포넌트 우선)

레퍼런스 가이드의 구조인 *진한 브랜드색 하나 + 기능용 강조색 하나 · 알약 모양 버튼 · 아주 굵은 큰 제목 · 장식 없는 평평한 화면*을 가져오고, 색과 글꼴과 컴포넌트는 타로 서비스에 맞게 새로 정했습니다.

---

## 1. 디자인 원칙

PRD의 원칙을 화면 규칙으로 옮겼습니다.

| # | 원칙 | 화면에서 지키는 법 | 근거 |
|---|---|---|---|
| 1 | **1분 안에 끝나는 흐름** | 한 화면에 할 일 하나. 주요 버튼은 화면마다 1개만 금빛으로. 화면은 S-01 → S-02 → S-03 세 장뿐 | PRD 1 · F-1~F-4 |
| 2 | **안심이 보이는 화면** | 🔒 개인정보 안내는 입력칸 바로 아래와 결과 화면에 *항상 보이게* 둔다. 접거나 작은 회색 글씨로 숨기지 않는다 | 원칙 1 · F-2 · F-4 |
| 3 | **카드가 주인공** | 결과 화면의 시선은 카드 그림 → 카드 이름 → 해석 3줄 순서. 나머지는 한 단계 물러난 색과 크기 | F-4 |
| 4 | **신비롭되 가볍게** | 어두운 남색과 금빛으로 분위기를 내고, 장식(그라데이션 · 반짝이 · 흐림 효과)은 쓰지 않는다. 문구는 "~해요"체로 친근하게 | PRD 배경 |
| 5 | **오락용임을 분명히** | "※ 오락용 타로 해석입니다"는 결과 카드 · 저장 이미지 · 공유 글에 빠짐없이 넣는다 | 원칙 4 |
| 6 | **그대로 저장되는 결과 카드** | 결과 카드 영역은 4:5 비율로 만들어 그대로 1080×1350 이미지가 되게 한다 | F-5 |

---

## 2. 색 (Colors)

### 2-1. 브랜드 팔레트

| 이름 | 값 | 토큰 | 역할 |
|---|---|---|---|
| Midnight Ink | `#1e1646` | `--color-midnight-ink` | **브랜드의 무게.** 제목 · 본문 강조 · 어두운 섹션 배경(시작 화면, 결과 카드) · 아이콘 · 테두리 강조. 순수한 검정 대신 늘 이 색을 쓴다 |
| Candle Gold | `#f4c95d` | `--color-candle-gold` | **유일한 강조색.** 주요 버튼 배경 · 선택된 주제 · 어두운 배경 위의 카드 이름. 한 화면 구역에 한 번만 |
| Deep Violet | `#3b2a7a` | `--color-deep-violet` | 보조 어두운 색. 카드 뒷면 무늬 · 어두운 섹션 안의 한 단계 밝은 면 · 눌렀을 때(pressed) 색 |
| Lavender Mist | `#efeaff` | `--color-lavender-mist` | 연한 보라 바탕. 개인정보 안내 상자 · 배지 · 주제 버튼에 마우스를 올렸을 때 |
| Moon Fog | `#f3f2f7` | `--color-moon-fog` | 회색빛 바탕. 입력 화면의 카드 면 · 구분 영역 |
| Paper | `#ffffff` | `--color-paper` | 페이지 바탕 · 어두운 카드 안의 흰 상자 |
| Night | `#0f0b24` | `--color-night` | 가장 진한 글자. 큰 제목(디스플레이)에만 |
| Ink Gray | `#3d3a4a` | `--color-ink-gray` | 기본 본문 글자. 흰 바탕에서 순수 검정보다 부드럽다 |
| Dusk | `#6b6878` | `--color-dusk` | 보조 글자 · 도움말 · 날짜 입력 예시 |
| Pebble | `#8a8699` | `--color-pebble` | 입력칸 테두리 · 비활성 아이콘 (흰 바탕 대비 3:1 이상) |
| Hairline | `#e2e0ea` | `--color-hairline` | 아주 옅은 구분선 · 카드 외곽선 |
| Ember Red | `#c2334b` | `--color-ember-red` | **오류에만.** "날짜를 다시 확인해 주세요" 같은 입력 오류 글자와 테두리 |
| Star Ivory | `#fdf6e3` | `--color-star-ivory` | 어두운 카드 위 본문 글자 (해석 3줄). 순백보다 따뜻하다 |

### 2-2. shadcn 시맨틱 토큰 연결

컴포넌트에는 원색 이름이 아니라 **시맨틱 토큰**만 씁니다 (`bg-primary` ○ / `bg-[#f4c95d]` ✕).

| shadcn 변수 | 값 | 쓰는 곳 |
|---|---|---|
| `--background` | Paper `#ffffff` | 페이지 바탕 |
| `--foreground` | Ink Gray `#3d3a4a` | 기본 글자 |
| `--card` / `--card-foreground` | Paper / Midnight Ink | 입력 화면 카드 |
| `--popover` / `--popover-foreground` | Paper / Midnight Ink | 토스트 · 드로어 |
| `--primary` / `--primary-foreground` | Candle Gold / Midnight Ink | 주요 버튼 ([타로 시작] · [카드 한 장 뽑기] · [이미지 저장]) |
| `--primary-active` *(추가)* | `#e5b43f` | 주요 버튼을 눌렀을 때 |
| `--secondary` / `--secondary-foreground` | Paper / Midnight Ink | 테두리 버튼 ([결과 공유]) |
| `--muted` / `--muted-foreground` | Moon Fog / Dusk | 옅은 바탕 · 보조 글자 |
| `--accent` / `--accent-foreground` | Lavender Mist / Midnight Ink | 고스트 버튼 hover · 안내 상자 · 배지 |
| `--destructive` | Ember Red | 입력 오류 |
| `--border` | Hairline `#e2e0ea` | 카드 외곽선 · 구분선 |
| `--input` | Pebble `#8a8699` | 입력칸 테두리 |
| `--ring` | Deep Violet `#3b2a7a` | 키보드 포커스 링 |
| `--mystic` / `--mystic-foreground` *(추가)* | Midnight Ink / Star Ivory | 어두운 섹션 (시작 화면 · 결과 카드) |
| `--mystic-accent` *(추가)* | Candle Gold | 어두운 섹션의 카드 이름 · 제목 |

### 2-3. 표면 단계 (Surfaces)

| 단계 | 이름 | 값 | 용도 |
|---|---|---|---|
| 0 | Paper | `#ffffff` | 기본 바탕 (S-02 입력 화면) |
| 1 | Moon Fog | `#f3f2f7` | 카드 면 · 옅은 구역 |
| 2 | Lavender Mist | `#efeaff` | 🔒 안내 상자 · 배지 · hover |
| 3 | Candle Gold | `#f4c95d` | 선택된 주제 · 주요 버튼 |
| 4 | Midnight Ink | `#1e1646` | 반전 구역 (S-01 시작 · S-03 결과 카드) |

### 2-4. 대비 규칙 (접근성)

| 조합 | 대비 | 판정 |
|---|---|---|
| Ink Gray 글자 / Paper | 약 11:1 | 본문 OK |
| Midnight Ink 글자 / Candle Gold | 약 11:1 | 버튼 글자 OK |
| Candle Gold 글자 / Midnight Ink | 약 11:1 | 어두운 카드의 카드 이름 OK |
| Star Ivory 글자 / Midnight Ink | 약 15:1 | 해석 본문 OK |
| Dusk 글자 / Paper | 약 5.5:1 | 보조 글자 OK |
| **Candle Gold 글자 / Paper** | 약 1.6:1 | **금지.** 금빛은 흰 바탕에서 글자로 쓰지 않는다 |

---

## 3. 글꼴 (Typography)

한글이 중심이라 레퍼런스의 영문 글꼴 대신 한글을 잘 지원하는 글꼴을 씁니다.

| 역할 | 글꼴 | 굵기 | 토큰 | 설명 |
|---|---|---|---|---|
| 본문 · UI | **Pretendard** | 400 · 500 · 600 · 700 | `--font-sans` | 입력칸 · 버튼 · 해석 · 안내 문구. 조용히 일하는 글꼴 |
| 디스플레이 | **Pretendard** | 800 · 900 | `--font-display` | "오늘의 타로" 큰 제목, 화면 첫 문장. 굵고 촘촘하게 외친다 |
| 카드 이름 · 숫자 | **Nanum Myeongjo** | 800 | `--font-serif` | "XIX 태양" 같은 카드 이름과 로마 숫자에만. 타로 카드다운 고전 느낌 |

- Pretendard는 jsDelivr CDN (`pretendard@1.3.9`)으로, Nanum Myeongjo는 Google Fonts로 불러온다.
- 대체 글꼴: `system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif`
- 한글은 자간을 영문보다 덜 줄인다. 큰 제목에서도 `-0.02em`을 넘지 않는다 (글자가 붙어 읽기 어려워짐).
- 줄바꿈은 `word-break: keep-all`로 단어 중간에서 끊지 않는다.

### 3-1. 글자 크기 단계 (모바일 기준)

| 역할 | 글꼴 | 굵기 | 크기 | 줄 간격 | 자간 | Tailwind | 쓰는 곳 |
|---|---|---|---|---|---|---|---|
| micro | sans | 500 | 12px | 1.5 | 0 | `text-micro` | 오락용 안내 · 배지 |
| caption | sans | 400 | 14px | 1.55 | 0 | `text-caption` | 🔒 안내 · 도움말 · 오류 |
| body | sans | 400 | 16px | 1.6 | -0.01em | `text-body` | 입력값 · 버튼 · 일반 본문 |
| body-lg | sans | 500 | 18px | 1.6 | -0.01em | `text-body-lg` | **해석 3줄** |
| title | sans | 700 | 22px | 1.35 | -0.015em | `text-title` | 화면 제목 ("나에 대해 알려 주세요") |
| card-name | serif | 800 | 28px | 1.2 | 0 | `text-card-name` | "XIX 태양" |
| heading | display | 800 | 36px | 1.15 | -0.02em | `text-heading` | 결과 카드 머리 ("지민님의 타로") |
| display | display | 900 | 48px | 1.05 | -0.02em | `text-display` | 시작 화면 "오늘의 타로" |

- 화면 너비 400px 이상에서는 display를 `56px`까지 키운다 (`min-[400px]:text-[56px]`).
- 해석 3줄은 18px · 줄 간격 1.6으로, 90자가 결과 카드 안에서 3–4줄로 끝나게 한다.

---

## 4. 간격 (Spacing)

**기본 단위:** 4px (Tailwind 기본 `--spacing: 0.25rem`을 그대로 씀) · **밀도:** 넉넉함

| 이름 | 값 | Tailwind | 쓰는 곳 |
|---|---|---|---|
| 1 | 4px | `gap-1` | 아이콘과 글자 사이 |
| 2 | 8px | `gap-2` | 라벨 ↔ 입력칸, 배지 안쪽 |
| 3 | 12px | `gap-3` | 주제 버튼 사이, 버튼 2개 사이 |
| 4 | 16px | `gap-4` / `px-4` | **화면 좌우 여백**, 입력 묶음 사이 |
| 5 | 20px | `gap-5` | 결과 카드 안 요소 사이 |
| 6 | 24px | `p-6` | 카드 안쪽 여백 |
| 8 | 32px | `gap-8` | 화면 안의 큰 구역 사이 (입력 ↔ 주제 ↔ 버튼) |
| 10 | 40px | `py-10` | 어두운 섹션 위아래 여백 |
| 16 | 64px | `pt-16` | 시작 화면 맨 위 여백 |

- 쌓을 때는 `flex flex-col gap-*`만 쓴다. `space-y-*` · `space-x-*`는 쓰지 않는다 (shadcn 규칙).
- 가로세로가 같으면 `size-*`를 쓴다 (`size-10` ○ / `w-10 h-10` ✕).
- 화면 아래 주요 버튼은 아이폰 홈 표시줄을 피해 `pb-[max(1rem,env(safe-area-inset-bottom))]`.

---

## 5. 모양 (Radius)

| 요소 | 값 | 토큰 / Tailwind |
|---|---|---|
| 버튼 · 주제 선택 · 배지 | 9999px (알약) | `rounded-full` |
| 입력칸 | 12px | `rounded-xl` (`--radius-input`) |
| 입력 화면 카드 · 안내 상자 · 토스트 | 16px | `rounded-2xl` (`--radius-card`) |
| 결과 카드 (어두운 섹션) | 28px | `rounded-[28px]` (`--radius-card-lg`) |
| 타로 카드 그림 | 14px | `rounded-[14px]` (`--radius-tarot`). 실제 카드처럼 살짝 둥근 직사각형 |

- 버튼 · 배지 · 주제 선택에 0–4px의 각진 모서리는 쓰지 않는다.
- shadcn 기본 `--radius`는 `1rem`(16px)로 둔다.

---

## 6. 깊이 (Elevation)

기본은 **평평하게**. 그림자는 두 곳에만 씁니다.

| 이름 | 값 | 쓰는 곳 |
|---|---|---|
| hairline | `0 0 0 1px rgba(30, 22, 70, 0.12)` | 입력 화면 카드 외곽 |
| tarot | `0 12px 32px rgba(15, 11, 36, 0.35)` | **타로 카드 그림** (어두운 배경에서 카드가 떠 보이게) |
| float | `0 6px 20px rgba(15, 11, 36, 0.10)` | 토스트 · 하단 드로어 |

- 그라데이션 · 빛 번짐(glow) · 흐림(blur) 효과는 쓰지 않는다.
- 포커스는 그림자 대신 `ring-2 ring-ring ring-offset-2`로 보여 준다.

---

## 7. 움직임 (Motion)

| 이름 | 길이 | 이징 | 쓰는 곳 |
|---|---|---|---|
| card-flip | **800ms** | `cubic-bezier(0.2, 0.8, 0.2, 1)` | 카드 뽑기 뒤집기 (F-3: 1초 이내) |
| fade-in | 200ms | `ease-out` | 해석 3줄이 카드 뒤집힌 뒤 나타날 때 |
| press | 100ms | `ease-out` | 버튼 누를 때 `scale-[0.98]` |

- 뒤집기: 카드 뒷면(Deep Violet 무늬) → `rotateY(180deg)` → 앞면. `transform-style: preserve-3d`, `backface-visibility: hidden`.
- **움직임 줄이기 설정 존중:** `motion-reduce:` 에서는 뒤집기 대신 200ms 페이드로 바꾼다.
- 같은 화면에서 반짝이 · 떠다니는 별 같은 반복 애니메이션은 쓰지 않는다.

---

## 8. 레이아웃 (Layout)

- **화면 폭:** 가운데 정렬 `mx-auto w-full max-w-[480px] px-4`. 데스크톱에서도 휴대폰 폭 그대로 보여 준다.
- **화면 리듬:** S-01 어두운 시작 → S-02 밝은 입력 → S-03 밝은 바탕 위 어두운 결과 카드. 밝음과 어두움이 번갈아 화면 전환을 느끼게 한다.
- **주요 버튼 위치:** S-01 · S-02의 주요 버튼은 화면 아래 고정(`sticky bottom-0`), 손가락이 닿기 쉬운 곳.
- **최소 터치 영역:** 44×44px 이상. 주요 버튼 높이 56px, 일반 버튼 48px.

| 화면 | 구조 |
|---|---|
| S-01 시작 | 전체 Midnight Ink 배경 · 가운데 쌓기: 🔮 + "오늘의 타로"(display, Star Ivory) → 카드 뒷면 그림 → 소개 2줄 → [타로 시작] → 오락용 · 저장 안 함 안내 |
| S-02 내 정보 · 주제 | Paper 배경 · 상단 뒤로가기 + 제목 → 입력 3개 → 주제 3×2 → 🔒 안내 → 하단 고정 [카드 한 장 뽑기] |
| S-03 결과 | Paper 배경 · 어두운 결과 카드(4:5) → 버튼 2×2 → 🔒 안내 |

---

## 9. 컴포넌트 규칙

shadcn 원칙대로 **이미 있는 컴포넌트를 먼저 쓰고, 기본 variant를 먼저 쓰고, 색은 시맨틱 토큰으로만** 지정합니다. `className`은 배치(크기 · 간격 · 위치)에만 쓰고 색과 글꼴을 덮어쓰지 않습니다.

### 컴포넌트 고르기

| 필요한 것 | 쓰는 컴포넌트 | 화면 |
|---|---|---|
| 버튼 | `Button` (variant: `default` · `outline` · `ghost` · `link`) | 전체 |
| 입력 묶음 | `FieldGroup` + `Field` + `FieldLabel` + `Input` + `FieldDescription` | S-02 |
| 주제 6개 고르기 | `ToggleGroup` + `ToggleGroupItem` (선택지 2–7개 → ToggleGroup) | S-02 |
| 🔒 개인정보 안내 | `Alert` (variant `mystic-soft`) | S-02 · S-03 |
| 결과 카드 | `Card` + `CardHeader` / `CardTitle` / `CardDescription` / `CardContent` / `CardFooter` | S-03 |
| 주제 · 별자리 표시 | `Badge` | S-03 |
| 저장 · 복사 알림 | `toast` (Base UI) 또는 `sonner` (Radix) | S-03 |
| 길게 눌러 저장 · 복사 | `Drawer` + `DrawerTitle` (아래에서 올라오는 시트) | S-03 |
| 구분선 | `Separator` | S-03 |
| 이미지 만드는 중 | `Button` + `Spinner` + `disabled` (`isLoading` 속성 없음) | S-03 |

### 9-1. 버튼 (Button)

| variant | 모양 | 높이 · 여백 | 글자 | 쓰는 곳 |
|---|---|---|---|---|
| `default` (주요) | Candle Gold 채움 · 테두리 없음 · 그림자 없음 | 56px (`h-14 px-6`) | 17px · 600 · Midnight Ink | [타로 시작] · [카드 한 장 뽑기] · [이미지 저장] |
| `outline` (보조) | Paper 채움 · 1.5px Midnight Ink 테두리 | 48px (`h-12 px-5`) | 16px · 600 · Midnight Ink | [결과 공유] |
| `ghost` | 배경 없음 · hover 시 Lavender Mist | 48px | 16px · 500 · Midnight Ink | [다시 뽑기] |
| `link` | 밑줄 글자 · 배경 없음 | 44px | 15px · 500 · Dusk | [처음으로] |
| `mystic-outline` *(추가)* | 투명 · 1.5px Star Ivory 테두리 | 48px | 16px · 600 · Star Ivory | 어두운 섹션 안 보조 버튼 |

- 모두 `rounded-full`.
- **금빛 버튼은 한 화면에 하나.** 금빛 버튼 두 개를 나란히 두지 않는다.
- S-03 버튼 4개: 윗줄 [이미지 저장 `default`] [결과 공유 `outline`], 아랫줄 [다시 뽑기 `ghost`] [처음으로 `link`]. 와이어프레임의 2×2 배치를 유지하면서 강조는 하나만.
- **비활성:** [카드 한 장 뽑기]는 이름 · 생년월일 · 주제가 모두 채워지기 전엔 `disabled` → Moon Fog 배경 · Pebble 글자 · `cursor-not-allowed`. 투명도만 낮추지 않는다 (금빛이 흐려져도 눌러질 것처럼 보임).
- **눌림:** `active:bg-primary-active active:scale-[0.98]`.
- 아이콘은 `data-icon="inline-start"`로 넣고 크기 클래스를 주지 않는다.

```tsx
<Button size="lg" className="w-full" disabled={!isReady}>
  <SparklesIcon data-icon="inline-start" />
  카드 한 장 뽑기
</Button>
```

### 9-2. 입력칸 (Input · Field)

| 속성 | 값 |
|---|---|
| 높이 · 여백 | 52px · `px-4` |
| 모양 | `rounded-xl` (12px) · 1px Pebble 테두리 · Paper 배경 |
| 글자 | 16px · 400 · Midnight Ink (16px 미만이면 iOS가 화면을 확대하므로 줄이지 않는다) |
| 예시 글자 | Dusk |
| 포커스 | 테두리 Midnight Ink + `ring-2 ring-ring/30`. 빛 번짐 없음 |
| 오류 | `Field data-invalid` + `Input aria-invalid` → 테두리 · 안내 글자 Ember Red |
| 라벨 | 14px · 600 · Midnight Ink. 선택 항목은 라벨 옆에 "(선택)" Dusk |

입력 3개 규칙 (F-2):

| 칸 | 라벨 | 규칙 |
|---|---|---|
| 이름 | 이름 (닉네임 OK) | 최대 10자 (`maxLength={10}`), 글자 수 `3/10` 표시 |
| 생년월일 | 생년월일 | `type="date"` 또는 `YYYY . MM . DD` 마스크 · 실제 날짜만 · 오류 시 "날짜를 다시 확인해 주세요" |
| 전공 | 전공 (선택) | 빈칸 허용 · 예시 "경영학과" |

```tsx
<FieldGroup>
  <Field>
    <FieldLabel htmlFor="name">이름 (닉네임 OK)</FieldLabel>
    <Input id="name" maxLength={10} placeholder="지민" />
  </Field>
  <Field data-invalid={birthError}>
    <FieldLabel htmlFor="birth">생년월일</FieldLabel>
    <Input id="birth" type="date" aria-invalid={birthError} />
    {birthError && <FieldDescription>날짜를 다시 확인해 주세요</FieldDescription>}
  </Field>
</FieldGroup>
```

### 9-3. 주제 선택 (ToggleGroup)

- `ToggleGroup type="single"`, 3열 × 2줄 그리드 (`grid grid-cols-3 gap-3`).
- 각 항목: 높이 48px · `rounded-full` · 이모지 + 글자 (💼 커리어 · 💰 재물 · 💕 연애 · 🌿 건강 · 📚 학업 · ✨ 종합).
- 선택 안 됨: Paper 배경 · 1px Hairline 테두리 · Ink Gray 글자.
- 선택됨 (`data-[state=on]`): **Candle Gold 배경** · Midnight Ink 글자 · 600. 금빛 강조가 버튼과 겹치므로, 주제를 고르기 전에는 [카드 한 장 뽑기]가 비활성(회색)이라 한 화면에 금빛이 둘이 되는 순간을 줄인다.
- 한 줄 제목: "어떤 주제가 궁금한가요?" (title 22px).

### 9-4. 개인정보 안내 (Alert)

- 문구 (기능명세서 공통 문구 그대로):
  > 🔒 입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요.
- 모양: Lavender Mist 배경 · `rounded-2xl` · `p-4` · 14px · Midnight Ink · 자물쇠 아이콘.
- 위치: S-02는 입력칸 묶음 바로 아래, S-03은 버튼 아래. **접기 · 툴팁으로 숨기지 않는다.**

### 9-5. 타로 카드 (Tarot Card)

| 속성 | 값 |
|---|---|
| 비율 | 7:12 (실제 타로 카드 비율에 가깝게) |
| 크기 | 결과 카드 안에서 너비 160px, 시작 화면 140px |
| 모양 | `rounded-[14px]` · 그림자 `tarot` · 2px Candle Gold 안쪽 테두리 |
| 뒷면 | Deep Violet 바탕 + 금빛 선으로 그린 단순한 별 · 달 무늬 (SVG) |
| 앞면 | 직접 만들었거나 사용 허가가 분명한 그림만 (PRD 리스크) |
| 뒤집기 | `card-flip` 800ms, 움직임 줄이기 설정 시 페이드 |
| 대체 글 | `alt="XIX 태양 카드"` |

### 9-6. 결과 카드 (Result Card · 어두운 섹션)

저장 이미지와 같은 영역입니다 (F-5).

| 속성 | 값 |
|---|---|
| 비율 | `aspect-[4/5]` → 그대로 1080×1350 PNG |
| 배경 | Midnight Ink · `rounded-[28px]` · `p-6` |
| 머리 (`CardHeader`) | "지민님의 타로" heading 36px Star Ivory + 주제 `Badge` |
| 카드 그림 | 가운데 · 너비 160px |
| 카드 이름 (`CardTitle`) | "XIX 태양" serif 28px **Candle Gold** + 별자리 `Badge` (♌ 사자자리) |
| 해석 (`CardContent`) | 3줄 · body-lg 18px · Star Ivory · 가운데 정렬 · 90자 이내 |
| 아래 (`CardFooter`) | "※ 오락용 타로 해석입니다" micro 12px · Star Ivory 70% + 서비스 이름 "오늘의 타로" |
| 넣지 않는 것 | 생년월일 · 전공 원문 (원칙 2) |

```tsx
<Card className="aspect-[4/5] rounded-[28px] bg-mystic text-mystic-foreground">
  <CardHeader className="items-center gap-2">
    <CardDescription>{name}님의 타로</CardDescription>
    <Badge variant="mystic">{topic}</Badge>
  </CardHeader>
  <CardContent className="flex flex-col items-center gap-5">
    <TarotCard card={card} />
    <CardTitle className="font-serif text-card-name text-mystic-accent">{card.number} {card.name}</CardTitle>
    <p className="text-body-lg text-center">{lines.join("\n")}</p>
  </CardContent>
  <CardFooter className="justify-between text-micro">
    <span>※ 오락용 타로 해석입니다</span>
    <span>오늘의 타로</span>
  </CardFooter>
</Card>
```

> 결과 카드는 브랜드 반전 섹션이라 `bg-mystic` 같은 **추가 시맨틱 토큰**으로 색을 정합니다. 원색 클래스(`bg-[#1e1646]`)는 쓰지 않습니다.

### 9-7. 배지 (Badge)

| variant | 모양 | 쓰는 곳 |
|---|---|---|
| `secondary` | Lavender Mist 배경 · Midnight Ink 글자 | 밝은 바탕의 주제 표시 |
| `mystic` *(추가)* | Deep Violet 배경 · Candle Gold 글자 | 결과 카드 안 주제 · 별자리 |

- 모두 `rounded-full` · `px-3 py-1` · 12px · 500.

### 9-8. 알림 · 대체 화면 (Toast · Drawer)

| 상황 (기능명세서) | 컴포넌트 | 문구 |
|---|---|---|
| 이미지 저장 성공 | toast | 이미지를 저장했어요 |
| 이미지 저장 안 됨 | Drawer (이미지 크게 표시) | 이미지를 길게 눌러 저장해 주세요 |
| 자동 복사 성공 | toast | 결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요 |
| 복사 실패 | Drawer (공유 글 표시, `select-all`) | 아래 글을 길게 눌러 복사해 주세요 |

- toast: 화면 위쪽 가운데 · Midnight Ink 배경 · Star Ivory 글자 · `rounded-2xl` · 2.5초.
- Drawer에는 꼭 `DrawerTitle`을 넣는다 (화면엔 안 보여도 `sr-only`로).

### 9-9. 시작 화면 큰 제목 (Display Headline)

- "오늘의 타로": display 48–56px · 900 · Star Ivory · 가운데.
- 그 아래 소개: "내 정보를 넣고 카드 한 장으로 / 나만의 해석을 받아 봐요" body 16px · Star Ivory 80%.
- 큰 제목은 화면마다 한 번만. 60px이 넘는 글자를 본문 글꼴 400으로 쓰지 않는다.

---

## 10. 문구 톤

| 규칙 | ○ | ✕ |
|---|---|---|
| "~해요"체, 짧게 | 준비한 것을 드러낼 때예요. | 귀하의 노력이 결실을 맺을 것입니다. |
| 건강 · 재물은 단정하지 않기 (원칙 4) | 지출 우선순위를 돌아볼 때예요 | 돈을 벌게 됩니다 |
| 버튼은 동작으로 | 카드 한 장 뽑기 | 확인 |
| 이름 뒤엔 "님" | 지민님의 타로 | 지민의 타로 |

---

## 11. 이미지 (Imagery)

- **주인공은 타로 카드 그림 하나.** 사진 · 스톡 이미지는 쓰지 않는다.
- 카드 뒷면 · 시작 화면 장식은 금빛 선으로 그린 단순한 별 · 달 · 눈 모양 SVG. 색은 Candle Gold와 Deep Violet 두 가지만.
- 카드 앞면 그림은 저작권이 분명한 것만 (직접 제작 또는 사용 허가) — PRD 미정 항목 "카드 그림 출처" 확정 후 반영.
- 주제 아이콘은 와이어프레임의 이모지를 그대로 쓴다 (💼 💰 💕 🌿 📚 ✨). 별도 아이콘 세트를 만들지 않는다.
- UI 아이콘은 프로젝트에 설정된 아이콘 라이브러리 (lucide 등) 한 종류만.

### 저장 이미지 · 공유 글

| 항목 | 규칙 |
|---|---|
| 저장 이미지 | 결과 카드 영역을 2배 이상 해상도로 그려 1080×1350 PNG. 바깥 Paper 여백 없이 Midnight Ink 카드만 |
| 공유 글 | 와이어프레임의 공유 메시지 형식 그대로. 생년월일 없음, 링크는 시작 화면 |

---

## 12. 해야 할 것 · 하지 말 것

### 해야 할 것
- 큰 제목은 Pretendard 900으로 굵게. 700으로 약하게 바꾸지 않는다.
- Candle Gold는 **주요 버튼 · 선택 상태 · 어두운 바탕의 카드 이름**에만 쓴다.
- 버튼 · 배지 · 주제 선택은 모두 알약 모양(`rounded-full`).
- 글자와 어두운 면은 순수 검정 대신 Midnight Ink.
- 주요 버튼 옆의 보조 동작은 `outline` · `ghost` · `link`로 한 단계씩 약하게.
- 🔒 개인정보 안내와 "오락용" 안내는 항상 보이게.
- 색은 시맨틱 토큰(`bg-primary`, `text-muted-foreground`, `bg-mystic`)으로만.
- 간격은 `flex` + `gap-*`, 정사각형은 `size-*`.
- 버튼 로딩은 `Spinner` + `disabled`로.

### 하지 말 것
- 흰 바탕 위에 Candle Gold 글자를 쓰지 않는다 (대비 부족).
- 금빛 버튼 두 개를 나란히 두지 않는다.
- 그라데이션 · 빛 번짐 · 흐림 · 반짝이는 반복 애니메이션을 넣지 않는다.
- 버튼 · 배지에 각진 모서리(0–4px)를 쓰지 않는다.
- 입력칸 글자를 16px보다 작게 하지 않는다.
- 결과 카드 · 저장 이미지 · 공유 글에 생년월일 · 전공 원문을 넣지 않는다.
- 비활성 버튼을 투명도만 낮춘 금빛으로 두지 않는다.
- `space-y-*`, 원색 클래스(`bg-yellow-400`, `bg-[#...]`), 수동 `dark:` 색 덮어쓰기를 쓰지 않는다.
- 다크 모드는 MVP에서 만들지 않는다. 어두운 분위기는 `mystic` 섹션으로만 낸다.

---

## 13. 빠른 시작 (Tailwind v4 + shadcn)

### 13-1. 글꼴 불러오기

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css" />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Nanum+Myeongjo:wght@800&display=swap" />
```

### 13-2. `globals.css`

```css
@import "tailwindcss";

/* shadcn 시맨틱 변수 — 값은 hex 그대로 둔다 */
:root {
  --radius: 1rem;

  --background: #ffffff;           /* Paper */
  --foreground: #3d3a4a;           /* Ink Gray */
  --card: #ffffff;
  --card-foreground: #1e1646;      /* Midnight Ink */
  --popover: #ffffff;
  --popover-foreground: #1e1646;

  --primary: #f4c95d;              /* Candle Gold */
  --primary-foreground: #1e1646;
  --primary-active: #e5b43f;

  --secondary: #ffffff;
  --secondary-foreground: #1e1646;
  --muted: #f3f2f7;                /* Moon Fog */
  --muted-foreground: #6b6878;     /* Dusk */
  --accent: #efeaff;               /* Lavender Mist */
  --accent-foreground: #1e1646;
  --destructive: #c2334b;          /* Ember Red */

  --border: #e2e0ea;               /* Hairline */
  --input: #8a8699;                /* Pebble */
  --ring: #3b2a7a;                 /* Deep Violet */

  /* 타로 전용 반전 섹션 */
  --mystic: #1e1646;
  --mystic-foreground: #fdf6e3;    /* Star Ivory */
  --mystic-accent: #f4c95d;
  --mystic-muted: #3b2a7a;         /* Deep Violet */
}

@theme inline {
  /* 색 — shadcn 변수를 Tailwind 유틸리티로 연결 */
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-primary-active: var(--primary-active);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-mystic: var(--mystic);
  --color-mystic-foreground: var(--mystic-foreground);
  --color-mystic-accent: var(--mystic-accent);
  --color-mystic-muted: var(--mystic-muted);

  /* 모양 */
  --radius-sm: calc(var(--radius) - 8px);   /* 8px */
  --radius-md: calc(var(--radius) - 4px);   /* 12px — 입력칸 */
  --radius-lg: var(--radius);               /* 16px — 카드 */
  --radius-xl: calc(var(--radius) + 4px);   /* 20px */
}

@theme {
  /* 브랜드 원색 (시맨틱 토큰을 만들 때만 참조) */
  --color-midnight-ink: #1e1646;
  --color-candle-gold: #f4c95d;
  --color-deep-violet: #3b2a7a;
  --color-lavender-mist: #efeaff;
  --color-moon-fog: #f3f2f7;
  --color-night: #0f0b24;
  --color-star-ivory: #fdf6e3;

  /* 글꼴 */
  --font-sans: "Pretendard Variable", Pretendard, system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;
  --font-display: var(--font-sans);
  --font-serif: "Nanum Myeongjo", "AppleMyungjo", serif;

  /* 글자 크기 단계 */
  --text-micro: 12px;      --text-micro--line-height: 1.5;
  --text-caption: 14px;    --text-caption--line-height: 1.55;
  --text-body: 16px;       --text-body--line-height: 1.6;
  --text-body-lg: 18px;    --text-body-lg--line-height: 1.6;
  --text-title: 22px;      --text-title--line-height: 1.35;  --text-title--letter-spacing: -0.015em;
  --text-card-name: 28px;  --text-card-name--line-height: 1.2;
  --text-heading: 36px;    --text-heading--line-height: 1.15; --text-heading--letter-spacing: -0.02em;
  --text-display: 48px;    --text-display--line-height: 1.05; --text-display--letter-spacing: -0.02em;

  /* 그림자 */
  --shadow-hairline: 0 0 0 1px rgba(30, 22, 70, 0.12);
  --shadow-tarot: 0 12px 32px rgba(15, 11, 36, 0.35);
  --shadow-float: 0 6px 20px rgba(15, 11, 36, 0.10);

  /* 움직임 */
  --animate-card-flip: card-flip 0.8s cubic-bezier(0.2, 0.8, 0.2, 1) both;
  --animate-fade-in: fade-in 0.2s ease-out both;

  @keyframes card-flip {
    from { transform: rotateY(0deg); }
    to   { transform: rotateY(180deg); }
  }
  @keyframes fade-in {
    from { opacity: 0; transform: translateY(4px); }
    to   { opacity: 1; transform: translateY(0); }
  }
}

@layer base {
  * { @apply border-border; }
  html { word-break: keep-all; }
  body { @apply bg-background font-sans text-body text-foreground antialiased; }
}
```

### 13-3. 버튼 variant (CVA)

shadcn `button.tsx`의 기존 variant 색만 위 토큰으로 바뀌므로 `default` · `outline` · `ghost` · `link`는 그대로 쓰고, 아래만 손봅니다.

```tsx
const buttonVariants = cva(
  "inline-flex items-center justify-center gap-2 rounded-full font-semibold transition-[background-color,transform] duration-100 active:scale-[0.98] focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:bg-muted disabled:text-input",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground active:bg-primary-active",
        outline: "border-[1.5px] border-card-foreground bg-secondary text-secondary-foreground hover:bg-accent",
        ghost: "text-card-foreground hover:bg-accent",
        link: "text-muted-foreground underline underline-offset-4",
        "mystic-outline": "border-[1.5px] border-mystic-foreground text-mystic-foreground hover:bg-mystic-muted",
      },
      size: {
        default: "h-12 px-5 text-body",
        lg: "h-14 px-6 text-[17px]",
        sm: "h-11 px-4 text-caption",
      },
    },
    defaultVariants: { variant: "default", size: "default" },
  }
)
```

### 13-4. shadcn 스타일 고르기

`npx shadcn@latest init` 때 스타일은 **`maia`** 를 권장합니다. 이 가이드는 48–56px 높이의 버튼, 16px 이상 둥근 카드, 넉넉한 여백을 쓰므로 "부드럽고 둥글고 여유 있는" maia가 가장 가깝습니다. 설치 후 위 `globals.css`로 테마를 덮어씁니다.

---

## 14. 미정 · 확인할 것

- 카드 앞면 그림 출처 확정 후 카드 그림 규칙(9-5) 보완 — PRD 8
- 주제를 3개로 줄이면 주제 선택을 3×1로 바꿈 — PRD 8
- 개인정보 동의 체크가 필요하면 `Checkbox` + `Field` 규칙 추가 — PRD 8
- Candle Gold / Midnight Ink 대비 수치는 실제 화면에서 대비 검사 도구로 다시 확인
