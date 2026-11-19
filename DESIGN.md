# 오늘의 타로 — 디자인 가이드 (DESIGN.md)

> 연회색 바탕 위 흰 라운드 카드, 그리고 초록 한 점.
> 화면은 밝고 가볍게, 강조는 초록(#00D959) 하나로. 카드 그림이 주인공입니다.

**버전:** v2 — 「명지대학교 타로 디자인 팩」(2026-11-07) 기준으로 전면 개정
**테마:** 라이트 단일 (다크 모드 없음)
**기기:** 모바일 웹, 기준 화면 375 × 812 (좌우 여백 20 → 콘텐츠 폭 335)
**참고 문서:** [TARO_01_PRD](TARO_01_PRD.md) · [TARO_02_기능명세서](TARO_02_기능명세서.md) · [TARO_03_유저플로우](TARO_03_유저플로우.md) · [TARO_04_와이어프레임](TARO_04_와이어프레임.md)
**구현 기준:** Tailwind CSS v4 (`@theme`) + shadcn/ui (시맨틱 토큰, 기본 컴포넌트 우선)
**피그마:** 디자인 팩의 변수 `Taro` 컬렉션 · 텍스트 스타일 `Taro/*` · 컴포넌트 이름을 그대로 씁니다.

디자인 팩은 레퍼런스(uibowl 타로 화면)에서 *연회색 배경 + 흰 라운드 카드 + 연두 강조색*의 구조만 가져왔습니다. 레퍼런스의 카드 그림 · 캐릭터 · 브랜드 요소는 쓰지 않습니다.

### v1 → v2 바뀐 점

| 항목 | v1 (이전) | v2 (디자인 팩) |
|---|---|---|
| 분위기 | 한밤 남색 + 금빛 | 연회색 바탕 + 흰 카드 + 초록 |
| 강조색 | Candle Gold `#f4c95d` | Accent `#00D959` |
| 글꼴 | Pretendard + Nanum Myeongjo | **Noto Sans KR** 하나, 자간 -2% |
| 버튼 | 알약 모양, 높이 56/48/44 | 둥근 사각형, **L 335×56 (r16) · M 162×48 (r14)** |
| 결과 화면 강조 버튼 | [이미지 저장] | **[결과 공유]** |
| 결과 카드 | 남색 4:5 카드 | **흰 카드 335×534** (r24) |
| 카드 그림 | 직접 그린 임시 그림 | **Rider-Waite-Smith(1909) 메이저 아르카나 22장** |
| 카드 뽑기 | 버튼 → 바로 뒤집기 | 버튼 → **22장 부채꼴에서 스와이프 · 탭** → 뒤집기 |
| 토스트 | 화면 위쪽 | 화면 **아래쪽** |

---

## 1. 디자인 원칙

| # | 원칙 | 화면에서 지키는 법 | 근거 |
|---|---|---|---|
| 1 | **1분 안에 끝나는 흐름** | 화면마다 할 일 하나. 초록 Primary 버튼은 화면당 1개 | PRD 1 · F-1~F-4 |
| 2 | **안심이 보이는 화면** | 🔒 개인정보 안내는 입력칸 바로 아래와 결과 화면에 *항상 보이게* 고정 | 원칙 1 · F-2 · F-4 |
| 3 | **카드가 주인공** | 결과 화면 시선: 카드 그림 → 카드 이름(초록) → 해석 3줄. 나머지는 회색으로 물러남 | F-4 |
| 4 | **밝고 가볍게** | 연회색 바탕 · 흰 카드 · 그림자 없음. 장식은 카드 그림과 스와이프 안내뿐 | 디자인 팩 |
| 5 | **오락용임을 분명히** | "※ 오락용 타로 해석입니다"를 결과 카드 · 저장 이미지 · 공유 글에 빠짐없이 | 원칙 4 |
| 6 | **그대로 저장되는 결과 카드** | Result Card 영역 = 저장 이미지 (1080×1350 PNG) | F-5 |

---

## 2. 색 (Color)

디자인 팩의 피그마 변수 컬렉션 `Taro` (모드: Light) 값입니다. 레퍼런스 화면에서 실제 픽셀을 추출한 값이에요.

| 토큰 (피그마 변수) | 값 | 쓰는 곳 |
|---|---|---|
| `color/bg` | `#F3F3F5` | 화면 바탕 (모든 화면) |
| `color/surface` | `#FFFFFF` | 카드 · 입력칸 · 칩 · 버튼(Secondary) · 바텀시트 |
| `color/surface-sub` | `#F6F6F8` | 🔒 개인정보 안내 · 복사용 글 상자 |
| `color/text/primary` | `#000000` | 제목 · 입력값 · 해석 본문 |
| `color/text/secondary` | `#4D4D4E` | 소개 문구 · 라벨 · 칩 글자 · 안내문 |
| `color/text/tertiary` | `#979F9B` | 예시 글자(placeholder) · 오락용 안내 · 보조 설명 |
| `color/text/on-accent` | `#FFFFFF` | 초록 · 회색(Disabled) 버튼 위 글자, 토스트 글자 |
| `color/border` | `#DCDCDD` | 입력칸 · 칩 · Secondary 버튼 테두리 (1px) |
| `color/accent` | `#00D959` | **유일한 강조색.** Primary 버튼 · 선택된 칩 테두리 · 포커스 테두리 · 카드 테두리 |
| `color/accent-soft` | `#E6FAEF` | 선택된 칩 배경 · 카드 뒷면 원 · 공유 글 미리보기 상자 |
| `color/accent-strong` | `#00D959` | 초록 글자 (카드 이름 · 선택된 칩 글자). 현재 accent와 같은 값 |
| `color/accent-illust` | `#00DE00` | 스와이프 안내("Swipe!") 손글씨 · 화살표 |
| `color/disabled` | `#D7D7D7` | 비활성 버튼 배경 |
| `color/danger` | `#E5484D` | 입력 오류 테두리 · 오류 문구 |
| `color/inverse` | `#232427` | 토스트 배경 · 바텀시트 뒤 어둡게(55%) |

### 2-1. 대비 주의 (디자인 팩 값 그대로 사용)

디자인 팩 값을 바꾸지 않고 그대로 씁니다. 다만 아래 조합은 대비가 낮다는 것을 알고 씁니다.

| 조합 | 대비 | 팩의 규칙 |
|---|---|---|
| 흰 글자 / `#00D959` 버튼 | 약 1.9 : 1 | **16px Bold 이상**(Body Bold · Label)에만 씀. 작은 글자 금지 |
| `#00D959` 글자 / 흰 카드 | 약 1.9 : 1 | 카드 이름(Headline 18 Bold)처럼 큰 굵은 글자에만 |
| 흰 글자 / `#D7D7D7` (Disabled) | 약 1.5 : 1 | 비활성 상태라 읽히지 않아도 되는 경우만 |
| `#979F9B` 글자 / 흰색 | 약 2.6 : 1 | 예시 글자 · 오락용 안내 같은 보조 글자만 |
| `#000000` · `#4D4D4E` 글자 / 흰색 · `#F3F3F5` | 21 : 1 · 8.4 : 1 | 본문 OK |

> ⚠️ WCAG 기준(큰 글자 3 : 1, 본문 4.5 : 1)에는 못 미칩니다. 접근성 검수에서 지적되면 v3에서 accent-strong을 더 진한 초록(예: `#00873A`, 4.6 : 1)으로 바꾸는 안을 검토합니다. [검토]

### 2-2. shadcn 시맨틱 토큰 연결

컴포넌트에는 원색이 아니라 **시맨틱 토큰**만 씁니다 (`bg-primary` ○ / `bg-[#00d959]` ✕).

| shadcn 변수 | 디자인 팩 토큰 | 값 |
|---|---|---|
| `--background` | color/bg | `#F3F3F5` |
| `--foreground` | color/text/primary | `#000000` |
| `--card` / `--popover` | color/surface | `#FFFFFF` |
| `--card-foreground` / `--popover-foreground` | color/text/primary | `#000000` |
| `--primary` / `--primary-foreground` | color/accent / color/text/on-accent | `#00D959` / `#FFFFFF` |
| `--secondary` / `--secondary-foreground` | color/surface / color/text/primary | `#FFFFFF` / `#000000` |
| `--muted` / `--muted-foreground` | color/surface-sub / color/text/secondary | `#F6F6F8` / `#4D4D4E` |
| `--accent` / `--accent-foreground` | color/accent-soft / color/accent-strong | `#E6FAEF` / `#00D959` |
| `--destructive` | color/danger | `#E5484D` |
| `--border` / `--input` | color/border | `#DCDCDD` |
| `--ring` | color/accent | `#00D959` |
| `--disabled` *(추가)* | color/disabled | `#D7D7D7` |
| `--subtle-foreground` *(추가)* | color/text/tertiary | `#979F9B` |
| `--inverse` *(추가)* | color/inverse | `#232427` |
| `--illust` *(추가)* | color/accent-illust | `#00DE00` |

---

## 3. 글씨 (Typography)

**글꼴:** Noto Sans KR 하나만. **자간:** 모든 스타일 -2%. 줄바꿈은 `word-break: keep-all`.

| 피그마 스타일 | 굵기 | 크기 / 줄 높이 | Tailwind | 쓰는 곳 |
|---|---|---|---|---|
| `Taro/Display` | Bold | 28 / 38 | `text-display` | 시작 화면 타이틀 "오늘의 타로", 카드 고르기 안내 문장 |
| `Taro/Title` | Bold | 22 / 32 | `text-title` | 화면 질문 · "XIX 태양이 나왔어요" |
| `Taro/Headline` | Bold | 18 / 26 | `text-headline` | 카드 이름 · 앱바 제목 · "어떤 주제가 궁금한가요?" · 바텀시트 제목 |
| `Taro/Body` | Regular | 16 / 26 | `text-body` | **해석 본문 (가운데 정렬, 3줄 · 90자 이내)** · 입력값 · 소개 문구 |
| `Taro/Body Bold` | Bold | 16 / 24 | `text-body-bold` | L 버튼 라벨 |
| `Taro/Label` | Medium | 15 / 22 | `text-label` | M 버튼 · 칩 · 토스트 글자 (선택된 칩은 Bold) |
| `Taro/Caption` | Regular | 13 / 19 | `text-caption` | 개인정보 안내 · 오락용 안내 · 오류 문구 · 보조 설명 |
| `Taro/Caption Bold` | Bold | 13 / 19 | `text-caption-bold` | 입력 라벨 · 결과 카드 머리("지민님의 타로 · 커리어") |

- 입력값은 16px 아래로 줄이지 않습니다 (iOS 자동 확대 방지).
- "Swipe!" 손글씨 안내만 예외: Noto Sans KR Bold 18, `color/accent-illust`.

---

## 4. 간격 (Spacing)

디자인 팩에 간격 변수는 없어서, 팩의 화면 · 컴포넌트에 실제로 쓰인 값을 정리했습니다. **기본 단위 2px**, 주로 4의 배수.

| 값 | Tailwind | 쓰는 곳 |
|---|---|---|
| 2 | `gap-0.5` | 해석 3줄 사이 |
| 6 | `gap-1.5` | 버튼 아이콘 ↔ 라벨 |
| 8 | `gap-2` | 입력 라벨 ↔ 입력칸 ↔ 도움말, 앱바 요소 사이 |
| 10 | `gap-2.5` | 주제 칩 사이(가로 · 세로), 🔒 아이콘 ↔ 안내문 |
| 11 | `gap-[11px]` | M 버튼 두 개 사이 (162 + 11 + 162 = 335) |
| 12 | `gap-3` | 바텀시트 버튼 위 · 결과 카드 바깥 요소 |
| 14 | `gap-3.5` | 결과 화면 본문 요소 사이, 안내 상자 · 토스트 세로 안쪽 |
| 16 | `gap-4` | 입력 화면 본문 요소 사이, 결과 카드 안 요소 사이, 바텀시트 요소 사이 |
| 20 | `px-5` | **화면 좌우 여백**, 토스트 · 바텀시트 가로 안쪽 |
| 24 | `px-6` | 결과 카드 가로 안쪽, 바텀시트 위쪽 |
| 28 | `py-7` | 결과 카드 세로 안쪽 |
| 34 | `pb-[34px]` | 하단 홈 표시줄 여백 (CTA · 바텀시트 아래) |
| 44 | `pt-11` | 상단 상태 표시줄 높이 |

- 쌓을 때는 `flex flex-col gap-*`만 씁니다. `space-y-*`는 쓰지 않습니다 (shadcn 규칙).
- 하단 CTA 영역: 위 12 · 좌우 20 · 아래 34 (`pb-[max(34px,env(safe-area-inset-bottom))]`).

---

## 5. 모양 (Radius) · 깊이 (Elevation)

| 요소 | 모서리 |
|---|---|
| L 버튼 (335×56) | 16 |
| M 버튼 (162×48) | 14 |
| 입력칸 · 🔒 안내 상자 · 토스트 · 카드 뒷면 | 12 |
| 카드 앞면 (그림) | 10 |
| 주제 칩 (105×44) | 22 (완전한 알약) |
| 결과 카드 | 24 |
| 바텀시트 (위쪽 두 모서리) | 24 |

- **그림자는 쓰지 않습니다.** 면 구분은 바탕색 차이(`#F3F3F5` ↔ `#FFFFFF`)와 1px 테두리(`#DCDCDD`)로만.
- 바텀시트 뒤는 `color/inverse` 55% 불투명도로 어둡게.

---

## 6. 움직임 (Motion) — 카드 고르기 · 뒤집기 (F-3)

| 단계 | 동작 | 시간 |
|---|---|---|
| 진입 | 22장 뒷면이 아래→위로 펼쳐짐, 가운데부터 차례로 | stagger 0.02s |
| 펼침 | 부채꼴 반지름 430, 카드 간격 8° | — |
| 스와이프 | 휠 하나만 회전 (quickTo), 놓으면 속도 반영 후 8° 단위로 스냅 | 0.45s |
| 탭 | 고른 카드가 가운데로 올라오며 커짐 (scale 1.7) | 0.5s |
| 뒤집기 | rotateY 180°, 앞면은 22장 중 **무작위 · 정방향** (어떤 카드를 탭해도 결과는 무작위) | 0.6s |
| 결과로 | 0.4s 뒤 결과 화면 카드 자리로 이동 (FLIP) → 해석 줄이 차례로 나타남 | 0.5s · stagger 0.08s |

- `transform` · `opacity`만 애니메이션합니다.
- **움직임 줄이기 설정(`prefers-reduced-motion`)이면 4배속**으로 재생합니다.

---

## 7. 레이아웃 · 화면 흐름

- 화면 폭 375, 좌우 여백 20, 콘텐츠 폭 335. 데스크톱에서도 `max-w-[375px] mx-auto`.
- 위에서부터: 상태 표시줄 44 → 앱바 56 → 본문 → 하단 CTA(필요한 화면만).
- 최소 터치 영역 44×44.

| 화면 | 이름 | 구성 |
|---|---|---|
| S-01 | 시작 | Display "오늘의 타로" → 카드 3장 부채(앞면 17 · 19 · 18, ±14°) → 소개 2줄 → L Primary [타로 시작] → Caption 안내 |
| S-02 | 내 정보 · 주제 | 앱바 "나에 대해 알려 주세요" → 입력 3개 → Headline 질문 → 칩 3×2 → 🔒 안내 → 하단 L 버튼 (빈 상태 Disabled / 완료 Primary) |
| S-03-P | 카드 고르기 | 앱바 → Display "{주제}를 떠올리며 카드 한 장을 골라 주세요" → 22장 뒷면 부채꼴(108×180, -40°~+40°) → "Swipe!" 안내 → Caption "좌우로 넘기고, 끌리는 카드를 탭하세요" |
| S-03-P2 | 카드 선택됨 | 고른 카드가 가운데로 커짐(180×300) · Display "선택한 카드를 뒤집어 볼게요" |
| S-03-D | 카드 공개 | Title "XIX 태양이 나왔어요" → 카드 앞면 208×348 → Caption |
| S-03 | 맞춤 해석 결과 (375×876) | 앱바 "나의 타로 결과" → 결과 카드 335×534 → M 버튼 2×2 → 🔒 안내 |
| S-03-T | 저장 성공 | 결과 화면 + 아래쪽 토스트 "이미지를 저장했어요" |
| S-03-S | 저장 안 됨 | 결과 화면 + 어두운 막 + 바텀시트(제목 · 결과 이미지 축소 · [닫기]) |
| S-03-C | 자동 복사 | 결과 화면 + 아래쪽 토스트 "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요" |
| S-03-F | 복사 실패 | 결과 화면 + 어두운 막 + 바텀시트(제목 · 공유 글 상자 · [닫기]) |

```
S-01 → S-02 → (카드 한 장 뽑기) → S-03-P → (탭) → S-03-P2 → S-03-D → S-03
S-03 → [다시 뽑기] → S-02 주제 선택부터 (정보 유지)
S-03 → [처음으로] → 정보 삭제 후 S-01
```

> 카드 고르기(S-03-P · P2)는 디자인 팩에서 새로 추가된 단계입니다. 기획 문서(TARO_02 F-3 · TARO_03)는 "버튼 → 무작위 한 장"으로 되어 있어 다음 문서 개정 때 맞춰야 합니다. 결과가 무작위라는 점은 그대로입니다.

---

## 8. 컴포넌트

shadcn 원칙: **있는 컴포넌트 먼저, 기본 variant 먼저, 색은 시맨틱 토큰으로만.** `className`은 배치에만 씁니다.

| 디자인 팩 컴포넌트 | shadcn | 화면 |
|---|---|---|
| `Button` (Type × Size) | `Button` (variant · size) | 전체 |
| `Input` (State 4종) | `Field` + `FieldLabel` + `Input` + `FieldDescription` | S-02 |
| `Topic Chip` (Default · Selected) | `ToggleGroup type="single"` + `ToggleGroupItem` | S-02 |
| `Privacy Notice` | `Alert` | S-02 · S-03 |
| `App Bar` | 직접 (`header`) | S-02 · S-03 |
| `Tarot Card / Back` · `/ Front` · `/ 00 ~ 21` | 직접 (`img` + 3D transform) | S-01 · S-03 |
| `Result Card` | `Card` + `CardHeader` / `CardContent` / `CardFooter` | S-03 |
| `Toast` | `toast` (Base UI) 또는 `sonner` | S-03 |
| 바텀시트 | `Drawer` + `DrawerTitle` | S-03-S |
| 아이콘 7종 | lucide (chevron-left · download · share · refresh · home · lock · copy) | 전체 |

### 8-1. Button

| Type | 배경 | 글자 | 테두리 |
|---|---|---|---|
| Primary | `color/accent` | `color/text/on-accent` | 없음 |
| Secondary | `color/surface` | `color/text/primary` | 1px `color/border` |
| Disabled | `color/disabled` | `color/text/on-accent` | 없음 |

| Size | 크기 | 모서리 | 글자 |
|---|---|---|---|
| L | 335 × 56 | 16 | `Taro/Body Bold` |
| M | 162 × 48 | 14 | `Taro/Label` |

- 아이콘 20px, 라벨과 간격 6px. 아이콘은 `data-icon="inline-start"`, 크기 클래스 없음.
- **L Primary는 화면당 주요 행동 1개:** [타로 시작] · [카드 한 장 뽑기].
- **Disabled:** 이름 · 생년월일 · 주제 중 하나라도 비면 [카드 한 장 뽑기]가 Disabled.
- **결과 화면 2×2:** 윗줄 [이미지 저장 Secondary · download] [결과 공유 **Primary** · share], 아랫줄 [다시 뽑기 Secondary · refresh] [처음으로 Secondary · home]. **[결과 공유]만 Primary.**
- 바텀시트 닫기 · 복사 실패 시트의 버튼은 L Secondary.

### 8-2. Input

| State | 입력칸 테두리 | 값 글자 | 도움말 |
|---|---|---|---|
| Default | 1px `color/border` | 예시 글자 `color/text/tertiary` | 숨김 |
| Filled | 1px `color/border` | `color/text/primary` | 숨김 |
| Focused | **2px `color/accent`** | `color/text/primary` | 숨김 |
| Error | **1.5px `color/danger`** | `color/text/primary` | "날짜를 다시 확인해 주세요" `color/danger` |

- 335 × 52, 모서리 12, 안쪽 좌우 16, 배경 `color/surface`.
- 라벨 `Taro/Caption Bold` `color/text/secondary`, 값 `Taro/Body`, 도움말 `Taro/Caption`.
- 이름 최대 10자(닉네임 권장 — 이미지 · 공유에 들어감). 생년월일은 실제 날짜만, 아니면 Error. 전공은 선택, 6개 계열로 못 맞추면 해석 3줄째 생략.
- 오류 표시는 `Field data-invalid` + `Input aria-invalid`.

### 8-3. Topic Chip

| State | 배경 | 테두리 | 글자 |
|---|---|---|---|
| Default | `color/surface` | 1px `color/border` | `Taro/Label` `color/text/secondary` |
| Selected | `color/accent-soft` | **1.5px `color/accent`** | `Taro/Label` Bold `color/accent-strong` |

- 105 × 44, 모서리 22, 3열 × 2줄, 간격 10.
- 주제 6개: 커리어 · 재물 · 연애 · 건강 · 학업 · 종합. 단일 선택.
- 이모지 아이콘은 실제 구현 때 SVG 아이콘으로 바꿉니다 (디자인 팩 메모). 디자인 팩 칩은 글자만 씁니다.

### 8-4. Privacy Notice

- 335 폭, 배경 `color/surface-sub`, 모서리 12, 안쪽 16 / 14, 간격 10.
- 🔒 lock 아이콘 20 + `Taro/Caption` `color/text/secondary`.
- 문구 (입력 · 결과 화면 공통):
  > 입력한 이름 · 생년월일 · 전공은 해석을 만드는 데만 쓰고, 서버로 보내거나 저장하지 않아요. 창을 닫거나 [처음으로]를 누르면 바로 지워져요.
- 접기 · 툴팁으로 숨기지 않습니다.

### 8-5. App Bar

- 375 × 56, 좌우 16, 간격 8. 왼쪽 chevron-left 20 (터치 영역 44) · 가운데 제목 `Taro/Headline` (가운데 정렬) · 오른쪽 20px 빈칸으로 균형.
- 배경 없음(화면 바탕 그대로).

### 8-6. Tarot Card

| 종류 | 크기 | 모양 |
|---|---|---|
| Back | 120 × 200 (기본) | 흰 바탕 · 2px `color/accent` 테두리 · 모서리 12 · 안쪽 1px 초록 선 · 가운데 `accent-soft` 원 + 초록 별 |
| Front | 160 × 268 (기본) | 카드 그림 이미지 · 모서리 10 |
| 부채꼴 덱 카드 | 108 × 180 | Back을 0.9배 |
| 선택된 카드 | 180 × 300 | Back을 1.5배 |
| 공개된 카드 | 208 × 348 | Front를 1.3배 |

- **카드 그림:** Rider-Waite-Smith(1909) 메이저 아르카나 00 The Fool ~ 21 The World 22장 (디자인 팩 「78 Tarot Cards」 파일). 정방향만.
- 카드 비율 약 3 : 5 (500 × 836 원본).
- 대체 글: `alt="XIX 태양 카드"`.

### 8-7. Result Card (= 저장 이미지)

- 335 × 534, 흰 바탕, 모서리 24, 안쪽 가로 24 · 세로 28, 요소 간격 16, 가운데 정렬.
- 위에서부터:
  1. 머리 "지민님의 타로 · 커리어" — `Taro/Caption Bold` `color/text/secondary`
  2. 카드 앞면 160 × 268
  3. 카드 이름 "XIX 태양 · 사자자리" — `Taro/Headline` `color/accent-strong`
  4. 해석 3줄 — `Taro/Body` 가운데 정렬 `color/text/primary`, 줄 간격 2
     - 줄1 카드 × 주제 기본 문장(이름 포함) · 줄2 별자리 문장 · 줄3 전공 계열 문장
     - 전공 미입력 → 줄3 숨김 (`Show Major Line` 끄기)
  5. "※ 오락용 타로 해석입니다" — `Taro/Caption` `color/text/tertiary`
- 저장 이미지(1080 × 1350 PNG)에는 이름 · 주제 · 카드 · 별자리 · 해석 3줄 · 오락용 안내 · 서비스 이름. **생년월일 · 전공 원문은 넣지 않습니다.**
- 건강 · 재물 해석은 단정하지 않고 돌아볼 관점으로 씁니다.

### 8-8. 저장 · 공유 피드백 (F-5 · F-6)

| 상황 | 표시 |
|---|---|
| 이미지 저장 성공 | Toast "이미지를 저장했어요" |
| 이미지 저장 안 됨 (인앱 브라우저) | 바텀시트: 제목 "이미지를 길게 눌러 저장해 주세요" + 결과 이미지 + [닫기] |
| 공유 메뉴 열림 / 취소 | 결과 화면 그대로 |
| 공유 메뉴 없음 → 자동 복사 성공 | Toast "결과를 복사했어요. 원하는 앱에 붙여 넣어 주세요" |
| 복사도 실패 | 바텀시트: 제목 "아래 글을 길게 눌러 복사해 주세요" + 공유 글 상자(`surface-sub`, 모서리 12, 안쪽 14) + [닫기] |

- **Toast:** 배경 `color/inverse`, 모서리 12, 안쪽 20 / 14, 글자 `Taro/Label` 흰색. 위치는 **화면 아래 가운데**(좌우 21, 아래 CTA 위).
- **바텀시트:** 흰 바탕, 위 모서리 24, 안쪽 좌우 20 · 위 24 · 아래 34, 간격 16. 제목 `Taro/Headline`. 뒤는 `color/inverse` 55%.
- 공유 글 템플릿 (생년월일 · 전공 원문 없음, 링크는 시작 화면):
  > 🔮 {이름}님의 타로 · {주제}
  > {카드 이름} · {별자리}
  > {해석 3줄}
  > ※ 오락용 타로 해석입니다
  > 나도 한 장 뽑기 → {시작 링크}

---

## 9. 문구 톤

| 규칙 | ○ | ✕ |
|---|---|---|
| "~해요"체, 짧게 | 준비한 것을 드러낼 때예요. | 귀하의 노력이 결실을 맺을 것입니다. |
| 건강 · 재물은 단정하지 않기 | 지출 우선순위를 돌아볼 때예요 | 돈을 벌게 됩니다 |
| 버튼은 동작으로 | 카드 한 장 뽑기 | 확인 |
| 이름 뒤엔 "님" | 지민님의 타로 | 지민의 타로 |

---

## 10. 해야 할 것 · 하지 말 것

### 해야 할 것
- 화면 바탕은 `#F3F3F5`, 카드 · 입력칸은 흰색으로 면을 나눈다.
- 초록 `#00D959`는 Primary 버튼 · 선택 · 포커스 · 카드 이름 · 카드 테두리에만 쓴다.
- 초록 위 흰 글자는 16px Bold 이상으로만 쓴다.
- L Primary는 화면당 하나. 결과 화면에서는 [결과 공유]만 Primary.
- 🔒 개인정보 안내와 "오락용" 안내는 항상 보이게.
- 글꼴은 Noto Sans KR 하나, 자간 -2%.
- 색은 시맨틱 토큰으로만, 간격은 `flex` + `gap-*`.

### 하지 말 것
- 그림자 · 그라데이션을 넣지 않는다.
- 초록 버튼 두 개를 나란히 두지 않는다.
- 13px 글자를 초록 위나 초록 글자로 쓰지 않는다.
- 결과 카드 · 저장 이미지 · 공유 글에 생년월일 · 전공 원문을 넣지 않는다.
- 레퍼런스(uibowl)의 카드 그림 · 캐릭터 · 브랜드 요소를 쓰지 않는다.
- `space-y-*`, 원색 클래스(`bg-green-500`, `bg-[#...]`), 수동 `dark:` 색을 쓰지 않는다.

---

## 11. 빠른 시작 (Tailwind v4 + shadcn)

### 11-1. 글꼴

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;700&display=swap" />
```

### 11-2. `globals.css`

```css
@import "tailwindcss";

:root {
  --radius: 0.75rem;                /* 12px — 입력칸 · 안내 상자 */

  --background: #f3f3f5;            /* color/bg */
  --foreground: #000000;            /* color/text/primary */
  --card: #ffffff;                  /* color/surface */
  --card-foreground: #000000;
  --popover: #ffffff;
  --popover-foreground: #000000;

  --primary: #00d959;               /* color/accent */
  --primary-foreground: #ffffff;    /* color/text/on-accent */
  --secondary: #ffffff;
  --secondary-foreground: #000000;
  --muted: #f6f6f8;                 /* color/surface-sub */
  --muted-foreground: #4d4d4e;      /* color/text/secondary */
  --accent: #e6faef;                /* color/accent-soft */
  --accent-foreground: #00d959;     /* color/accent-strong */
  --destructive: #e5484d;           /* color/danger */

  --border: #dcdcdd;                /* color/border */
  --input: #dcdcdd;
  --ring: #00d959;

  --disabled: #d7d7d7;              /* color/disabled */
  --subtle-foreground: #979f9b;     /* color/text/tertiary */
  --inverse: #232427;               /* color/inverse */
  --illust: #00de00;                /* color/accent-illust */
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
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
  --color-disabled: var(--disabled);
  --color-subtle-foreground: var(--subtle-foreground);
  --color-inverse: var(--inverse);
  --color-illust: var(--illust);

  --radius-card: 10px;     /* 카드 앞면 */
  --radius-md: 12px;       /* 입력칸 · 안내 · 토스트 · 카드 뒷면 */
  --radius-btn-m: 14px;
  --radius-btn-l: 16px;
  --radius-chip: 22px;
  --radius-xl: 24px;       /* 결과 카드 · 바텀시트 */
}

@theme {
  --font-sans: "Noto Sans KR", system-ui, -apple-system, "Apple SD Gothic Neo", "Malgun Gothic", sans-serif;

  --text-display: 28px;      --text-display--line-height: 38px;      --text-display--font-weight: 700;
  --text-title: 22px;        --text-title--line-height: 32px;        --text-title--font-weight: 700;
  --text-headline: 18px;     --text-headline--line-height: 26px;     --text-headline--font-weight: 700;
  --text-body: 16px;         --text-body--line-height: 26px;
  --text-body-bold: 16px;    --text-body-bold--line-height: 24px;    --text-body-bold--font-weight: 700;
  --text-label: 15px;        --text-label--line-height: 22px;        --text-label--font-weight: 500;
  --text-caption: 13px;      --text-caption--line-height: 19px;
  --text-caption-bold: 13px; --text-caption-bold--line-height: 19px; --text-caption-bold--font-weight: 700;

  --animate-card-flip: card-flip 0.6s cubic-bezier(0.2, 0.8, 0.2, 1) both;
  @keyframes card-flip { from { transform: rotateY(0deg); } to { transform: rotateY(180deg); } }
}

@layer base {
  * { @apply border-border; }
  html { word-break: keep-all; }
  body { @apply bg-background font-sans text-body text-foreground antialiased; letter-spacing: -0.02em; }
}
```

### 11-3. 버튼 variant (CVA)

```tsx
const buttonVariants = cva(
  "inline-flex items-center justify-center gap-1.5 font-bold transition-transform active:scale-[0.98] focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:bg-disabled disabled:text-primary-foreground",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground",                       // Primary
        secondary: "border border-border bg-secondary text-secondary-foreground", // Secondary
      },
      size: {
        lg: "h-14 w-full rounded-btn-l text-body-bold",                       // L 335×56
        md: "h-12 rounded-btn-m text-label",                                  // M 162×48
      },
    },
    defaultVariants: { variant: "default", size: "lg" },
  }
)
```

### 11-4. shadcn 스타일 고르기

`npx shadcn@latest init` 때 스타일은 **`maia`** 를 권장합니다. 48–56px 높이 버튼, 12–24px 둥근 모서리, 넉넉한 여백, 그림자 없는 면 구분이 가장 가깝습니다. 설치 후 위 `globals.css`로 테마를 덮어씁니다.

---

## 12. 미정 · 확인할 것

- 초록 강조색 대비 (2-1) — 접근성 검수 결과에 따라 v3에서 accent-strong 조정 [검토]
- 카드 고르기 단계(S-03-P · P2)를 기획 문서 TARO_02 F-3 · TARO_03 유저플로우에 반영
- 주제 칩 SVG 아이콘 세트 확정 (현재 글자만)
- 카드 그림 사용 범위: RWS 1909 원본은 퍼블릭 도메인이지만, 배포 전 사용한 스캔 파일의 출처 · 라이선스 확인 [검토]
