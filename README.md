# QM Slide Template 2026

Quad Miners 임직원 전용 공식 PowerPoint 슬라이드 AI 생성 스킬 패키지입니다.  
Claude Desktop · Claude Code · PowerPoint (Claude Add-in) 3가지 환경을 지원합니다.

---

## ⚠️ 현재 사용 가능 환경 안내 (2026-04 기준)

> **현재 Quad Miners 조직 설정상 Claude의 코드 실행(Code Execution) 기능이 비활성화되어 있습니다.**  
> 이에 따라 현재는 **Claude Code CLI 환경에서만 사용 가능**합니다.

| 환경 | 현재 사용 가능 여부 | 비고 |
|------|-------------------|---------|
| **Claude Code CLI** | ✅ 사용 가능 | 조직 설정과 무관하게 독립 동작 |
| **Claude Desktop 앱** | ⏸️ 현재 제한 | 코드 실행 활성화 후 사용 가능 |
| **PowerPoint Add-in** | ⏸️ 현재 제한 | 코드 실행 활성화 후 사용 가능 |

### 코드 실행이 비활성화된 이유

Claude Team/Enterprise 계정에서 **코드 실행 기능은 보안상의 이유로 기본값이 비활성화(OFF)** 되어 있습니다.  
이는 Anthropic의 의도적인 보안 설계로, 코드 실행 환경이 외부 네트워크 접속과 결합될 경우 데이터 유출·프롬프트 인젝션 등의 위험이 있기 때문입니다.  
Anthropic은 조직 관리자 활성화와 사용자 개인 opt-in, 두 단계 모두를 거치도록 권장하고 있습니다.

### Claude Desktop · PowerPoint Add-in 사용을 원하시는 경우

조직 내 코드 실행 기능 활성화는 IT/보안 담당자 및 조직 관리자(Organization Owner)의 검토와 승인이 필요합니다.  
**기능 활성화 시 전략기획팀에서 별도 공지 및 사용 가능 여부를 안내드릴 예정입니다.**  
현재는 CLI 설치 방법(아래 **B. Claude Code CLI** 항목)을 통해 이용해 주세요.

---

## 다운로드

최신 버전은 **[Releases](https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026/releases/latest)** 페이지에서 다운로드하세요.

```
quad-miners-pptx-skill.skill  ← 이 파일 하나만 다운로드하면 됩니다 (약 118 MB)
```

---

## 설치 방법

### A. Claude Desktop / Claude.ai 웹 (권장 · 설치 불필요)

> Claude Team 또는 Enterprise 계정이 필요합니다.

1. `설정 (Settings)` → `기능 (Capabilities)` → **코드 실행 (Code execution)** 켜기
2. 좌측 사이드바 `개인설정 (Customize)` → `스킬 (Skills)` 탭 클릭
3. **`+` 버튼** → `스킬 업로드 (Upload skill)` 선택
4. 다운로드한 `quad-miners-pptx-skill.skill` 파일 업로드 (1~3분 소요)
5. 내 스킬 (My Skills) 목록에 **quad-miners-pptx** 표시되면 완료

### B. Claude Code CLI

```powershell
# Windows PowerShell 기준

# 1. 저장소 복제
git clone https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026.git
cd QM_SLIDE_TEMPLATE_2026

# 2. Claude 스킬 디렉토리에 설치
New-Item -ItemType Directory -Force -Path "$HOME\.claude\skills"
Copy-Item "quad-miners-pptx-skill.skill" "quad-miners-pptx-skill.zip"
Expand-Archive -Path "quad-miners-pptx-skill.zip" `
               -DestinationPath "$HOME\.claude\skills\" -Force
```

```bash
# macOS / Linux 기준
git clone https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026.git
cd QM_SLIDE_TEMPLATE_2026

mkdir -p ~/.claude/skills
cp quad-miners-pptx-skill.skill quad-miners-pptx-skill.zip
unzip quad-miners-pptx-skill.zip -d ~/.claude/skills/
```

---

## 처음 설치 후 필수 절차

### 1단계 · 설치 확인

```
/qmslide_check
```

9가지 항목(폰트·로고·패키지 등) 전체를 자동 점검합니다.  
정상이면 `✅ 설치 완료! 모든 검사 통과 (27/27)` 메시지가 표시됩니다.

문제가 발견된 경우 자동 수정:

```bash
python scripts/check.py --fix
```

### 2단계 · 샘플 생성으로 동작 확인

```
/qmslide_sample
```

6종 슬라이드 타입이 포함된 완성 샘플 덱(`qm_sample.pptx`)이 즉시 생성됩니다.  
PowerPoint에서 열어 폰트·로고·배경·색상이 올바르게 표시되는지 확인하세요.

---

## 명령어 레퍼런스

### 슬라이드 생성

| 명령어 | 설명 | 예시 |
|--------|------|------|
| `/qmslide_deck <요청>` | **전체 덱 생성** — 표지·목차·간지·내용·마무리 자동 구성 | `/qmslide_deck NDR 제품 소개 자료 8장` |
| `/qmslide_slide <요청>` | **단일 슬라이드** 생성 또는 수정 | `/qmslide_slide compare NDR 비교표` |
| `/qmslide_build <구성>` | **구성 직접 지정** 생성 | `/qmslide_build title+toc(5)+section+content(3)+closing` |
| `/qmslide_template <타입>` | **빈 템플릿** 슬라이드 반환 | `/qmslide_template section` |

> ⚠️ **`/qm` alias 사용 비권장**  
> 현재 버전(v1.0.0)에는 `/qmslide_deck`의 단축 alias로 `/qm`이 존재하지만, 향후 추가될 다른 스킬들과의 명령어 충돌·혼동 방지를 위해 **사용을 권장하지 않습니다.**  
> 다음 릴리즈부터 해당 alias는 삭제될 예정입니다. 지금부터 `/qmslide_deck`을 사용해주세요.

### 설치 및 관리

| 명령어 | 설명 |
|--------|------|
| `/qmslide_check` | 스킬 설치 전체 점검 (9항목 27개 검사) |
| `/qmslide_sample` | 6종 완성 샘플 덱 생성 |
| `/qmslide_update` | GitHub 최신 버전 수동 확인 및 적용 |
| `/qmslide_version` | 현재 설치 버전 확인 |
| `/qmslide_font install` | Noto Sans CJK KR 폰트 설치 |
| `/qmslide_qa <파일명>` | 생성된 슬라이드 품질 검사 |

### 조회

| 명령어 | 설명 | 예시 |
|--------|------|------|
| `/qmslide_logo <제품명>` | 사용 가능한 로고 파일 조회 | `/qmslide_logo network blackbox` |
| `/qmslide_color <색상명>` | 컬러 팔레트 코드 조회 | `/qmslide_color cyan` |

---

## 사용 예시

### 전체 발표 자료 만들기

```
/qmslide_deck Network Blackbox 2026 제품 소개서, 목차 5섹션, 한국어, 총 12장
```

```
/qmslide_deck 인도네시아 파트너사 제출용 NDR 사업 제안서, 영어, 비교표 포함
```

### 슬라이드 타입 지정 생성

```
/qmslide_slide compare  일반 NDR vs Network Blackbox 4행 비교표
/qmslide_slide section  03 "Key Solutions" 섹션 간지
/qmslide_slide chart    분기별 위협 탐지 건수 막대 차트
```

### 구성 직접 지정

```
/qmslide_build title+toc(5)+section+split+content(3)+compare+closing  NDR 제안서
/qmslide_build title+compare+chart+closing  경쟁사 비교 보고서
```

### 샘플 특정 타입만 보기

```
/qmslide_sample title      ← 표지만
/qmslide_sample toc        ← 목차만
/qmslide_sample section    ← 간지만
/qmslide_sample compare    ← 비교표만
/qmslide_sample closing    ← 마무리만
```

---

## CLI 직접 실행 (Python)

Claude 없이 Python 스크립트를 직접 실행할 수도 있습니다.

```bash
# 설치 확인
python scripts/check.py
python scripts/check.py --verbose   # 상세 출력
python scripts/check.py --fix       # 문제 자동 수정

# 샘플 생성
python scripts/sample.py                           # 전체 6장
python scripts/sample.py --type title              # 표지만
python scripts/sample.py --output my_deck.pptx     # 출력 파일명 지정

# 버전 및 업데이트 확인
python scripts/autoupdate.py
python scripts/autoupdate.py --check-only          # 확인만

# 명령어 직접 실행
python scripts/pptx_command.py "/qmslide_version"
```

---

## 스킬 패키지 구성

```
quad-miners-pptx-skill/
├── SKILL.md                    ← 스킬 핵심 정의 파일
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
│   ├── pptx_command.py         ← 명령어 처리 엔진
│   ├── install_fonts.py        ← 폰트 자동 설치 (Python)
│   └── install_fonts.sh        ← 폰트 자동 설치 (Shell)
├── assets/
│   ├── fonts/                  ← Noto Sans CJK KR 7종 (.otf)
│   └── logos/                  ← Quad Miners 공식 로고 26종 (.png)
```

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

## 자동 업데이트

슬라이드 생성 요청 시마다 스킬이 **자동으로 GitHub 최신 버전을 확인**합니다.

| 상태 | 표시 메시지 |
|------|------------|
| 최신 버전 | `✅ 스킬 최신 버전(v1.x.x) 확인 완료` |
| 업데이트 있음 | `✅ 스킬이 v1.x → v1.y로 업데이트되었습니다` |
| 연결 30초 초과 | `⚠️ GitHub 연결 시간 초과 — 현재 버전으로 진행` |

수동 업데이트: `/qmslide_update`

---

## PowerPoint — Claude Add-in 연동

> **사전 조건:** Claude for PowerPoint Add-in 설치 필요  
> 지원 플랜: Pro · Max · **Team · Enterprise** (Quad Miners 임직원 대상)

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

### QM 스킬 불러오기 (Add-in 설치 후)

1. **QM 템플릿 파일**(`quad-miners-pptx-skill.skill`)을 Claude Desktop에 사전 설치
2. PowerPoint에서 QM 템플릿 파일(`.pptx`) 열기
3. 우측 Claude 사이드바 → `스킬 (Skills)` 탭 → **quad-miners-pptx** 선택
4. 또는 사이드바 하단 `지침 (Instructions)` 필드에 Quad Miners 브랜드 가이드 붙여넣기

---

### PowerPoint 내 명령어 사용

Claude 사이드바 입력창에 아래 명령어를 그대로 입력합니다.

| 입력 예시 | 결과 |
|-----------|------|
| `/qmslide_deck NDR 제품 소개서 8장` | 표지~마무리 전체 덱 생성 |
| `/qmslide_slide compare NDR 비교표` | 현재 덱에 비교표 슬라이드 추가 |
| `/qmslide_template section` | 빈 간지 슬라이드 삽입 |
| `/qmslide_qa 현재파일` | 열린 파일 품질 검사 |

> Claude Add-in은 현재 열린 `.pptx` 파일의 **슬라이드 마스터·레이아웃·폰트·색상**을 자동으로 읽어  
> QM 브랜드 가이드라인에 맞는 슬라이드를 생성합니다.

---

### 주요 기능

| 기능 | 설명 |
|------|------|
| 템플릿 인식 | 열린 파일의 슬라이드 마스터·레이아웃 자동 반영 |
| 핀포인트 편집 | 특정 슬라이드만 지정하여 수정 가능 |
| 다이어그램 변환 | 불릿 목록 → 네이티브 다이어그램/차트 자동 변환 |
| 덮어쓰기 방지 | 기존 슬라이드 보호 옵션 내장 |
| 지침 (Instructions) | 브랜드 지침·선호도를 사이드바에 영구 저장 |
| Skills 연동 | quad-miners-pptx 스킬 로드 시 `/qmslide_*` 명령 인식 |

---

## 버전 이력

| 버전 | 날짜 | 내용 |
|------|------|------|
| v1.0.0 | 2026-04 | 최초 배포 — Claude Desktop / Code / PowerPoint (Claude Add-in) 지원 |

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
