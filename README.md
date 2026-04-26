# QM Slide Template 2026

Quad Miners 임직원 전용 공식 PowerPoint 슬라이드 AI 생성 스킬 패키지입니다.  
Claude Desktop · Claude Code · PowerPoint (Claude Add-in) 3가지 환경을 지원합니다.

---

## ⚠️ 현재 사용 가능 환경 안내 (2026-04 기준)

> **현재 Quad Miners 조직 설정상 Claude의 코드 실행(Code Execution) 기능이 비활성화되어 있습니다.**  
> 이에 따라 현재는 **Claude Code CLI 환경에서만 사용 가능**합니다.

| 환경 | 현재 사용 가능 여부 | 비고 |
|------|-------------------|----|
| **Claude Code CLI** | [OK] 사용 가능 | 아래 설치 절차 후 자연어로 요청 |
| **Claude Desktop 앱** | [--] 현재 제한 | 코드 실행 활성화 후 사용 가능 |
| **PowerPoint Add-in** | [--] 현재 제한 | 코드 실행 활성화 후 사용 가능 |

### 코드 실행이 비활성화된 이유

Claude Team/Enterprise 계정에서 **코드 실행 기능은 보안상의 이유로 기본값이 비활성화(OFF)** 되어 있습니다.  
이는 Anthropic의 의도적인 보안 설계로, 코드 실행 환경이 외부 네트워크 접속과 결합될 경우 데이터 유출·프롬프트 인젝션 등의 위험이 있기 때문입니다.  
Anthropic은 조직 관리자 활성화와 사용자 개인 opt-in, 두 단계 모두를 거치도록 권장하고 있습니다.

### Claude Desktop · PowerPoint Add-in 사용을 원하시는 경우

조직 내 코드 실행 기능 활성화는 IT/보안 담당자 및 조직 관리자(Organization Owner)의 검토와 승인이 필요합니다.  
**기능 활성화 시 전략기획팀에서 별도 공지 및 사용 가능 여부를 안내드릴 예정입니다.**  
현재는 아래 **Claude Code CLI** 방법을 통해 이용해 주세요.

---

## 다운로드

최신 버전은 **[Releases](https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026/releases/latest)** 페이지에서 다운로드하세요.

```
quad-miners-pptx-skill.skill  ← 이 파일 하나만 다운로드하면 됩니다 (약 118 MB)
```

---

## 설치 방법 (Claude Code CLI)

> Claude Code CLI가 설치되어 있어야 합니다.  
> 미설치 시: `npm install -g @anthropic-ai/claude-code` (Node.js 필요)

### Step 1 · 스킬 디렉토리 생성

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.claude\skills"
```

### Step 2 · 스킬 파일 압축 해제

다운로드한 `.skill` 파일이 있는 폴더에서 실행합니다.

```powershell
# .skill 파일을 zip으로 복사
Copy-Item "quad-miners-pptx-skill.skill" "$HOME\.claude\skills\quad-miners-pptx-skill.zip"

# 압축 해제 (반드시 skills\ 바로 아래로)
Expand-Archive -Path "$HOME\.claude\skills\quad-miners-pptx-skill.zip" `
               -DestinationPath "$HOME\.claude\skills\" -Force
```

### Step 3 · 설치 구조 확인

```powershell
ls "$HOME\.claude\skills\quad-miners-pptx-skill\"
```

아래 항목이 **직접** 보여야 정상입니다.

```
SKILL.md
VERSION
assets/
references/
scripts/
```

> [!] 위 항목들이 보이지 않고 `quad-miners-pptx-skill` 폴더만 보이면 **이중 중첩** 상태입니다.  
> 이 경우 폴더를 삭제하고 Step 2를 다시 실행하세요.

```powershell
# 이중 중첩 발생 시 재설치
Remove-Item -Recurse -Force "$HOME\.claude\skills\quad-miners-pptx-skill"
Expand-Archive -Path "$HOME\.claude\skills\quad-miners-pptx-skill.zip" `
               -DestinationPath "$HOME\.claude\skills\" -Force
```

---

## 사용 방법 (실제 검증된 절차)

### Step 1 · Claude Code 실행

PowerShell에서 슬라이드를 저장할 폴더로 이동 후 실행합니다.

```powershell
cd C:\Users\사용자명\Documents\QM_Slides   # 원하는 저장 폴더로 이동
claude
```

### Step 2 · 스킬 활성화

Claude Code 대화창에서 아래와 같이 입력합니다.

```
다음 파일을 읽어서 스킬로 활성화해줘: C:\Users\사용자명\.claude\skills\quad-miners-pptx-skill\SKILL.md
```

> 실제 경로에서 `사용자명` 부분을 본인의 Windows 계정명으로 변경하세요.  
> (예: `C:\Users\Admin\.claude\skills\quad-miners-pptx-skill\SKILL.md`)

아래와 같은 응답이 오면 스킬 활성화 완료입니다.

```
SKILL.md 파일을 성공적으로 읽었습니다. 스킬이 활성화되었으며,
Quad Miners PPTX 슬라이드 생성 스킬의 모든 가이드라인이 로드되었습니다.
```

### Step 3 · 슬라이드 생성 요청

**슬래시 명령어(/qmslide_deck 등)는 사용하지 않습니다.**  
스킬 활성화 후 자연어로 바로 요청합니다.

```
2026년 글로벌 NDR 동향 슬라이드를 10장으로 만들어줘
```

```
Network Blackbox 제품 소개서 8장, 한국어, 비교표 포함해서 만들어줘
```

```
인도네시아 파트너사 제출용 NDR 사업 제안서, 영어, 총 12장으로 만들어줘
```

### Step 4 · 생성 결과 확인

생성된 `.pptx` 파일은 **Claude Code를 실행한 현재 폴더**에 저장됩니다.

```powershell
# PowerShell에서 파일 확인
ls *.pptx

# 바로 열기
Invoke-Item *.pptx
```

---

## 매 세션마다 스킬 활성화가 필요한 이유

현재 Claude Code CLI는 `~/.claude/skills/` 폴더의 스킬을 **자동으로 인식하지 않습니다** (알려진 제한 사항).  
따라서 Claude Code를 새로 실행할 때마다 Step 2의 스킬 활성화를 반복해야 합니다.

> 이 제한은 향후 Claude Code 업데이트에서 해결될 예정입니다.  
> 개선 시 전략기획팀에서 공지 예정입니다.

---

## 샘플 슬라이드 생성

스킬 활성화 후 아래와 같이 요청합니다.

```
샘플 슬라이드 만들어줘
```

6종 슬라이드 타입(표지·목차·간지·2열 콘텐츠·비교표·마무리)이 포함된 `qm_sample.pptx`가 현재 폴더에 생성됩니다.

---

## 지원 슬라이드 타입

| 타입 | 설명 | 요청 예시 |
|------|------|----------|
| **표지 (title)** | 발표 표지 슬라이드 | `표지 슬라이드 만들어줘` |
| **목차 (toc)** | 6섹션 2×3 그리드 목차 | `목차 슬라이드 만들어줘` |
| **간지 (section)** | 섹션 구분 슬라이드 | `"01 제품 소개" 간지 만들어줘` |
| **2열 본문 (content-split)** | 불릿+이미지 레이아웃 | `2열 본문 슬라이드 만들어줘` |
| **비교표 (compare)** | 제품 비교 테이블 | `NDR vs 일반 방화벽 비교표 만들어줘` |
| **데이터 시각화 (data-viz)** | 차트·그래프 슬라이드 | `분기별 위협 탐지 건수 차트 슬라이드 만들어줘` |
| **마무리 (closing)** | Thank You 슬라이드 | `마무리 슬라이드 만들어줘` |

---

## 브랜드 가이드라인 요약

| 항목 | 규격 |
|------|------|
| **슬라이드 크기** | 16:9 — 33.87cm × 19.05cm (EMU: 12,192,000 × 6,858,000) |
| **폰트** | Noto Sans CJK KR 전용 (다른 폰트 사용 금지) |
| **최소 폰트 크기** | 12pt (절대 미만 금지) |
| **주요 색상** | Cyan `#00D8FF` · Blue `#2F6BFF` · Purple `#7A5CFF` · Dark `#111827` |
| **배경** | 흰색 `#FFFFFF` |
| **로고 파일** | assets/logos/ 내 26종만 사용 |

---

## 스킬 패키지 구성

```
quad-miners-pptx-skill/
├── SKILL.md                    ← 스킬 핵심 정의 파일 (매 세션 로드 필요)
├── VERSION                     ← 현재 버전 (1.0.0)
├── references/
│   ├── commands.md             ← 명령어 전체 레퍼런스
│   ├── creation-guide.md       ← 슬라이드 생성 가이드 (PptxGenJS)
│   ├── slide-specs.md          ← 슬라이드 타입별 EMU 좌표 스펙
│   ├── font-setup.md           ← 폰트 설치 가이드
│   └── brand-assets.md         ← 브랜드 로고 사용 가이드
├── scripts/
│   ├── check.py                ← 설치 확인 (9항목 27개 검사)
│   ├── sample.py               ← 샘플 슬라이드 생성
│   ├── autoupdate.py           ← GitHub 자동 업데이트 확인
│   ├── pptx_command.py         ← 명령어 처리 보조 스크립트 (Claude 내부 사용)
│   ├── install_fonts.py        ← 폰트 자동 설치 (Python)
│   └── install_fonts.sh        ← 폰트 자동 설치 (Shell)
├── assets/
│   ├── fonts/                  ← Noto Sans CJK KR 7종 (.otf)
│   └── logos/                  ← Quad Miners 공식 로고 26종 (.png)
```

> [!] `scripts/pptx_command.py`는 Claude가 내부적으로 호출하는 보조 스크립트입니다.  
> PowerShell에서 단독으로 실행해도 실제 슬라이드가 생성되지 않습니다.

---

## 자동 업데이트

스킬 활성화 시 자동으로 GitHub 최신 버전을 확인합니다.

| 상태 | 표시 메시지 |
|------|------------|
| 최신 버전 | `[OK] 스킬 최신 버전(v1.x.x) 확인 완료` |
| 업데이트 있음 | `[OK] 스킬이 v1.x → v1.y로 업데이트되었습니다` |
| 연결 30초 초과 | `[!] GitHub 연결 시간 초과 — 현재 버전으로 진행` |

---

## PowerPoint — Claude Add-in 연동

> **사전 조건:** Claude for PowerPoint Add-in 설치 필요  
> 지원 플랜: Pro · Max · **Team · Enterprise** (Quad Miners 임직원 대상)  
> **현재 조직 코드 실행 비활성화로 인해 사용 불가. 활성화 시 별도 공지 예정.**

### Add-in 설치

#### 개인 설치 (Windows / Mac / Web)

1. PowerPoint 열기
2. **홈 (Home) 탭** → `추가 기능 (Add-ins)` 클릭  
   *(Mac: 메뉴바 `도구 (Tools)` → `추가 기능 (Add-ins)`)*
3. 검색창에 **`Claude by Anthropic`** 입력 → **추가 (Add)** 클릭
4. Anthropic 계정으로 로그인 (Team / Enterprise 계정)
5. PowerPoint 우측에 **Claude 사이드바** 표시되면 완료

> Microsoft Marketplace 직접 설치:  
> [https://marketplace.microsoft.com/en-us/product/office/wa200010001](https://marketplace.microsoft.com/en-us/product/office/wa200010001)

#### 조직 일괄 배포 (IT 관리자)

1. [Microsoft 365 관리 센터 (Admin Center)](https://admin.microsoft.com) → `설정 (Settings)` → `통합 앱 (Integrated Apps)`
2. 검색창에 **`Claude by Anthropic`** 입력
3. `배포 (Deploy)` → 배포 대상(전체 조직 또는 그룹) 선택 후 확인
4. 배포 완료 후 사용자 PowerPoint에 자동 적용 (최대 24시간 소요)

---

## 버전 이력

| 버전 | 날짜 | 내용 |
|------|------|------|
| v1.0.0 | 2026-04 | 최초 배포 — Claude Desktop / Code / PowerPoint (Claude Add-in) 지원 |

---

## 알려진 제한 사항

| 항목 | 내용 |
|------|------|
| 스킬 자동 인식 불가 | Claude Code CLI는 `~/.claude/skills/` 폴더를 자동으로 인식하지 않음. 매 세션마다 SKILL.md 수동 로드 필요 |
| 슬래시 명령어 미동작 | `/qmslide_deck` 등 슬래시 명령어는 CLI에서 동작하지 않음. 자연어 요청 사용 |
| Desktop/PowerPoint 미지원 | 조직 코드 실행 비활성화로 인해 현재 사용 불가 |

> [!] `/qm` alias: 현재 버전(v1.0.0)에 `/qmslide_deck`의 단축 alias로 `/qm`이 정의되어 있으나,  
> CLI 환경에서는 슬래시 명령어 자체가 동작하지 않으며, 향후 다른 스킬들과의 충돌 방지를 위해 **사용을 권장하지 않습니다.**  
> 다음 릴리즈부터 해당 alias는 삭제될 예정입니다.

---

## 문의

Quad Miners 내부 사용자 전용입니다.  
스킬 관련 문의 및 피드백은 **전략기획팀**으로 연락해 주세요.

---

## 작성자

| 항목 | 내용 |
|------|------|
| **작성팀** | Quad Miners 전략기획팀 |
| **최초 작성일** | 2026-04 |
| **문서 버전** | v1.0.0 |
