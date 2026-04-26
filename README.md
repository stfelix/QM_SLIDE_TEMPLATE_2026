# QM SLIDE TEMPLATE 2026

> **[!] 현재 CLI 환경에서만 사용 가능합니다.**
>
> 조직(Organization) 수준에서 코드 실행 기능이 비활성화된 경우,
> Claude Desktop 및 PowerPoint Add-in에서는 슬라이드 생성 스킬이 동작하지 않습니다.
> 현재는 **Claude Code CLI**를 통해서만 사용 가능합니다.
>
> 코드 실행 기능 활성화 문의: **Quad Miners 전략기획팀**

---

**작성자**: Quad Miners 전략기획팀
**문의처**: 전략기획팀 (내부 채널 또는 담당자 직접 연락)
**버전**: v3.1.0
**최종 업데이트**: 2026-04-26 (v3.1.0 ZIP 구조 수정 — qmslide/ 래퍼 폴더 추가)

---

## 개요

Quad Miners 직원들이 공식 브랜드 가이드라인에 맞는 고품질 PowerPoint 프레젠테이션을
Claude Code CLI에서 자동으로 생성할 수 있는 스킬 패키지입니다.

### 지원 운영체제

| OS | 지원 여부 | 비고 |
|----|-----------|------|
| Windows 10 / 11 | 지원 | PowerShell 5.1 이상 |
| macOS 12 Monterey 이상 | 지원 | Homebrew 권장 |
| Ubuntu 20.04 / 22.04 / 24.04 | 지원 | apt 패키지 관리자 사용 |
| 기타 Linux (Debian 계열) | 지원 | apt 기반 동일 적용 |

### 특징

- Quad Miners 공식 컬러 팔레트 (#00D8FF / #2F6BFF / #7A5CFF / #111827) 자동 적용
- Noto Sans CJK KR 폰트 전용 사용
- 26개 공식 로고 파일 포함
- 표지 / 목차 / 섹션간지 / 내용 / 비교표 / 마무리 등 8가지 슬라이드 타입
- 12개 슬래시 명령어로 세분화된 기능 제공
- `shared/references/brand-core.md` 단일 브랜드 정의 (Single Source of Truth)
- v3.0.0: Harness Engineering 완전 적용
- v3.1.0: ZIP 구조 수정 (qmslide/ 래퍼 폴더 제거 → skills/ 바로 아래에 명령어 폴더 직접 배치, Claude Code 명령어 인식 정상화)
  - Compressed DSL 지시어 — SKILL.md 1개당 평균 **48% 토큰 절감**
  - Output Schema Binding — `output-schema.md` 로 산출물 구조 고정, 환각 방지
  - Guard Clause First — 생성 명령어 실행 전 사전조건 자동 점검
  - Lazy Reference Pattern — 필요 시점에만 brand-core.md / output-schema.md 로드

---

## 설치 경로 구조 (v3.1.0)

설치 완료 후 아래 구조가 됩니다. OS별로 스킬 루트 경로만 다릅니다.

| OS | 스킬 루트 경로 |
|----|---------------|
| Windows | `C:\Users\<사용자명>\.claude\skills\` (shared/, qmslide-deck/ 등이 직접 위치) |
| macOS | `~/.claude/skills/` (shared/, qmslide-deck/ 등이 직접 위치) |
| Linux | `~/.claude/skills/` (shared/, qmslide-deck/ 등이 직접 위치) |

```
<스킬 루트>/
├── shared/                           <- 공유 에셋 (로고, 폰트, 스크립트, 레퍼런스)
│   ├── assets/
│   │   ├── fonts/                    <- NotoSansCJKkr .otf 9종
│   │   └── logos/                    <- 공식 로고 26종 + 배경/헤더/푸터
│   ├── references/                   <- brand-core.md, output-schema.md, commands.md 등 7종
│   ├── scripts/                      <- check.py, sample.py, autoupdate.py 등
│   └── VERSION
├── qmslide-deck/
│   └── SKILL.md                      <- /qmslide-deck 명령어
├── qmslide-slide/
│   └── SKILL.md                      <- /qmslide-slide 명령어
├── qmslide-build/
│   └── SKILL.md                      <- /qmslide-build 명령어
├── qmslide-template/
│   └── SKILL.md                      <- /qmslide-template 명령어
├── qmslide-check/
│   └── SKILL.md                      <- /qmslide-check 명령어
├── qmslide-sample/
│   └── SKILL.md                      <- /qmslide-sample 명령어
├── qmslide-update/
│   └── SKILL.md                      <- /qmslide-update 명령어
├── qmslide-version/
│   └── SKILL.md                      <- /qmslide-version 명령어
├── qmslide-font/
│   └── SKILL.md                      <- /qmslide-font 명령어
├── qmslide-logo/
│   └── SKILL.md                      <- /qmslide-logo 명령어
├── qmslide-color/
│   └── SKILL.md                      <- /qmslide-color 명령어
└── qmslide-qa/
    └── SKILL.md                      <- /qmslide-qa 명령어
```

---

## 설치 가이드 — Windows

### Step 1. Node.js 설치 (Windows)

> [!] **이미 Node.js가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: PowerShell에서 `node --version` 실행 시 버전이 출력되면 설치된 것입니다.

```powershell
# 버전 확인 (출력되면 Skip)
node --version
```

설치되어 있지 않은 경우: https://nodejs.org 에서 LTS 버전을 다운로드하여 설치하세요.

---

### Step 2. Claude Code CLI 설치 (Windows)

> [!] **이미 Claude Code CLI가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `claude --version` 실행 시 버전이 출력되면 설치된 것입니다.

```powershell
# 버전 확인 (출력되면 Skip)
claude --version

# 미설치 시 아래 실행
# npm install -g @anthropic-ai/claude-code
```

---

### Step 3. .skill 파일 다운로드 (Windows)

> [!] **이미 다운로드했다면 이 단계를 건너뛰세요.**

[Releases 페이지](https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026/releases)에서
최신 버전의 `quad-miners-pptx-skill-v3.skill` 파일을 다운로드하세요.

---

### Step 4. 스킬 폴더 생성 (Windows)

> [!] **이미 `.claude\skills` 폴더가 존재하면 이 단계를 건너뛰세요.**
> 확인 방법: `ls "$env:USERPROFILE\.claude\skills"` 실행 시 폴더가 보이면 존재합니다.

```powershell
# 폴더 존재 여부 확인 (폴더가 보이면 Skip)
ls "$env:USERPROFILE\.claude\skills" 2>$null

# 없을 경우 아래 실행
# mkdir "$env:USERPROFILE\.claude\skills" -Force
```

---

### Step 5. 스킬 압축 해제 및 설치 (Windows)

> [!] **이미 설치한 적이 있다면 기존 폴더를 백업 후 덮어쓰거나, 없는 경우만 실행하세요.**
> 확인 방법: `ls "$env:USERPROFILE\.claude\skills\qmslide-check"` 실행 시 폴더가 보이면 이미 설치된 것입니다.

```powershell
# 설치 여부 확인 (폴더가 보이면 Skip)
ls "$env:USERPROFILE\.claude\skills\qmslide-check" 2>$null

# -- 미설치 시 아래 실행 ------------------------------------------
# 1) .skill 파일을 .zip으로 복사
Copy-Item "$env:USERPROFILE\Downloads\quad-miners-pptx-skill-v3.skill" `
          "$env:USERPROFILE\.claude\skills\quad-miners-pptx-skill-v3.zip"

# 2) skills/ 폴더에 직접 압축 해제
# [!] 해제 후 shared/, qmslide-deck/ 등이 skills/ 바로 아래에 생성됩니다
Expand-Archive "$env:USERPROFILE\.claude\skills\quad-miners-pptx-skill-v3.zip" `
               "$env:USERPROFILE\.claude\skills" -Force

# 3) zip 파일 정리
Remove-Item "$env:USERPROFILE\.claude\skills\quad-miners-pptx-skill-v3.zip"
# ----------------------------------------------------------------
```

설치 결과 확인:

```powershell
ls "$env:USERPROFILE\.claude\skills"
# 아래 폴더들이 skills/ 바로 아래에 보여야 합니다:
# shared  qmslide-deck  qmslide-slide  qmslide-build  ...
```

---

### Step 6. Python 패키지 설치 (Windows)

> [!] **이미 python-pptx, Pillow 가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `pip show python-pptx` 실행 시 정보가 출력되면 설치된 것입니다.

```powershell
# 설치 여부 확인 (정보가 출력되면 Skip)
pip show python-pptx
pip show Pillow

# 미설치 시 아래 실행
# pip install python-pptx Pillow requests
```

---

### Step 7. 폰트 설치 (Windows)

> [!] **이미 Noto Sans CJK KR 폰트가 시스템에 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: PowerPoint를 열고 폰트 목록에서 "Noto Sans CJK KR"이 보이면 설치된 것입니다.

```powershell
# 방법 A — 자동 설치 스크립트 (소스 폴더에서 실행)
# cd C:\Users\Admin\Downloads\qm-skill-upload\QM_SLIDE_TEMPLATE_2026
# python scripts\install_fonts.py
```

방법 B — 수동 설치 (자동 설치가 안 될 경우):

1. `C:\Users\Admin\.claude\skills\shared\assets\fonts\` 폴더 열기
2. `.otf` 파일 전체 선택 -> 우클릭 -> **"모든 사용자를 위해 설치 (Install for all users)"**
3. PowerPoint 재시작

---

### Step 8. Claude Code CLI 실행 및 스킬 확인 (Windows)

```powershell
# 소스 폴더로 이동
cd C:\Users\Admin\Downloads\qm-skill-upload\QM_SLIDE_TEMPLATE_2026

# Claude Code 실행
claude

# Claude Code 채팅에서 설치 확인 (처음 설치 시 필수)
/qmslide-check
```

> [!] **`/qmslide-check` 후 모든 항목이 `[OK]`로 표시되면 설치 완료입니다.**
> 문제가 있는 항목은 `python scripts\check.py --fix` 로 자동 수정할 수 있습니다.

---

### Step 9. 샘플 슬라이드 생성으로 최종 검증 (Windows)

```
/qmslide-sample
```

현재 폴더에 `qm_sample.pptx` 파일이 생성됩니다.
PowerPoint로 열어 아래 항목을 확인하세요.

```
[OK] 모든 슬라이드 우상단에 Quad Miners 로고
[OK] 하단 푸터: QM 로고 + 저작권 + 페이지번호 + "Confidential"
[OK] 배경: 연청색 기하학 육각형 패턴
[OK] 폰트: Noto Sans CJK KR (한글 깨짐 없음)
[OK] 색상: 파랑 #2F6BFF, 다크 #111827
```

---

## 설치 가이드 — macOS

### Step 1. Homebrew 설치 (macOS)

> [!] **이미 Homebrew가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `brew --version` 실행 시 버전이 출력되면 설치된 것입니다.

```bash
# 버전 확인 (출력되면 Skip)
brew --version

# 미설치 시 아래 실행
# /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

---

### Step 2. Node.js 설치 (macOS)

> [!] **이미 Node.js가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `node --version` 실행 시 버전이 출력되면 설치된 것입니다.

```bash
# 버전 확인 (출력되면 Skip)
node --version

# 미설치 시 Homebrew로 설치
# brew install node
```

---

### Step 3. Claude Code CLI 설치 (macOS)

> [!] **이미 Claude Code CLI가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `claude --version` 실행 시 버전이 출력되면 설치된 것입니다.

```bash
# 버전 확인 (출력되면 Skip)
claude --version

# 미설치 시 아래 실행
# npm install -g @anthropic-ai/claude-code
```

---

### Step 4. Python 및 패키지 설치 (macOS)

> [!] **이미 python-pptx, Pillow 가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `pip3 show python-pptx` 실행 시 정보가 출력되면 설치된 것입니다.

```bash
# Python 버전 확인 (3.8 이상 필요)
python3 --version

# 설치 여부 확인 (정보가 출력되면 Skip)
pip3 show python-pptx

# 미설치 시 아래 실행
# pip3 install python-pptx Pillow requests
```

---

### Step 5. .skill 파일 다운로드 (macOS)

> [!] **이미 다운로드했다면 이 단계를 건너뛰세요.**

[Releases 페이지](https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026/releases)에서
최신 버전의 `quad-miners-pptx-skill-v3.skill` 파일을 다운로드하세요.

또는 터미널에서 직접 다운로드:

```bash
# 미다운로드 시 아래 실행
# curl -L -o ~/Downloads/quad-miners-pptx-skill-v3.skill \
#   https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026/releases/download/v3.1.0/quad-miners-pptx-skill-v3.skill
```

---

### Step 6. 스킬 설치 (macOS)

> [!] **이미 설치한 적이 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `ls ~/.claude/skills/qmslide-check` 실행 시 폴더가 보이면 이미 설치된 것입니다.

```bash
# 설치 여부 확인 (폴더가 보이면 Skip)
ls ~/.claude/skills/qmslide-check 2>/dev/null

# -- 미설치 시 아래 실행 ------------------------------------------
# 1) 스킬 폴더 생성
mkdir -p ~/.claude/skills

# 1) .skill 파일을 .zip으로 복사
cp ~/Downloads/quad-miners-pptx-skill-v3.skill \
   ~/Downloads/quad-miners-pptx-skill-v3.zip

# 2) skills/ 폴더에 직접 압축 해제
# [!] 해제 후 shared/, qmslide-deck/ 등이 skills/ 바로 아래에 생성됩니다
unzip ~/Downloads/quad-miners-pptx-skill-v3.zip \
      -d ~/.claude/skills/

# 3) zip 파일 정리
rm ~/Downloads/quad-miners-pptx-skill-v3.zip
# ----------------------------------------------------------------
```

---

### Step 7. 폰트 설치 (macOS)

> [!] **이미 Noto Sans CJK KR 폰트가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `fc-list | grep "Noto Sans CJK KR"` 실행 시 결과가 나오면 설치된 것입니다.

```bash
# 설치 여부 확인 (결과가 나오면 Skip)
fc-list | grep "Noto Sans CJK KR"

# 방법 A — 자동 설치 스크립트 (소스 폴더에서 실행)
# cd ~/Downloads/QM_SLIDE_TEMPLATE_2026
# python3 scripts/install_fonts.py

# 방법 B — Homebrew로 설치
# brew install --cask font-noto-sans-cjk-kr
```

방법 C — 수동 설치:

1. `~/.claude/skills/shared/assets/fonts/` 폴더 열기
2. `.otf` 파일 전체를 **서체 관리자 (Font Book)** 에 드래그하여 설치
3. 설치 완료 후 LibreOffice 또는 PowerPoint 재시작

---

### Step 8. Claude Code CLI 실행 및 스킬 확인 (macOS)

```bash
# 소스 폴더로 이동 (다운로드한 소스 위치에 맞게 변경)
cd ~/Downloads/QM_SLIDE_TEMPLATE_2026

# Claude Code 실행
claude

# Claude Code 채팅에서 설치 확인 (처음 설치 시 필수)
/qmslide-check
```

> [!] **`/qmslide-check` 후 모든 항목이 `[OK]`로 표시되면 설치 완료입니다.**
> 문제가 있는 항목은 `python3 scripts/check.py --fix` 로 자동 수정할 수 있습니다.

---

### Step 9. 샘플 슬라이드 생성으로 최종 검증 (macOS)

```
/qmslide-sample
```

현재 폴더에 `qm_sample.pptx` 파일이 생성됩니다.
LibreOffice Impress 또는 PowerPoint로 열어 아래 항목을 확인하세요.

```
[OK] 모든 슬라이드 우상단에 Quad Miners 로고
[OK] 하단 푸터: QM 로고 + 저작권 + 페이지번호 + "Confidential"
[OK] 배경: 연청색 기하학 육각형 패턴
[OK] 폰트: Noto Sans CJK KR (한글 깨짐 없음)
[OK] 색상: 파랑 #2F6BFF, 다크 #111827
```

---

## 설치 가이드 — Linux (Ubuntu / Debian 계열)

### Step 1. 시스템 패키지 업데이트 (Linux)

> [!] **최근에 apt update를 실행한 적이 있다면 이 단계를 건너뛰세요.**

```bash
# 최근에 업데이트했으면 Skip
sudo apt update && sudo apt upgrade -y
```

---

### Step 2. Node.js 설치 (Linux)

> [!] **이미 Node.js 18 이상이 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `node --version` 실행 시 v18 이상이면 설치된 것입니다.

```bash
# 버전 확인 (v18 이상이면 Skip)
node --version

# 미설치 또는 구버전인 경우 NodeSource 저장소로 설치
# curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
# sudo apt install -y nodejs
```

---

### Step 3. Claude Code CLI 설치 (Linux)

> [!] **이미 Claude Code CLI가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `claude --version` 실행 시 버전이 출력되면 설치된 것입니다.

```bash
# 버전 확인 (출력되면 Skip)
claude --version

# 미설치 시 아래 실행
# npm install -g @anthropic-ai/claude-code
```

---

### Step 4. Python 및 패키지 설치 (Linux)

> [!] **이미 python-pptx, Pillow 가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `pip3 show python-pptx` 실행 시 정보가 출력되면 설치된 것입니다.

```bash
# Python 버전 확인 (3.8 이상 필요)
python3 --version

# pip3 없으면 먼저 설치
# sudo apt install -y python3-pip

# 설치 여부 확인 (정보가 출력되면 Skip)
pip3 show python-pptx

# 미설치 시 아래 실행
# pip3 install python-pptx Pillow requests
```

---

### Step 5. .skill 파일 다운로드 (Linux)

> [!] **이미 다운로드했다면 이 단계를 건너뛰세요.**

```bash
# 미다운로드 시 아래 실행
# curl -L -o ~/Downloads/quad-miners-pptx-skill-v3.skill \
#   https://github.com/stfelix/QM_SLIDE_TEMPLATE_2026/releases/download/v3.1.0/quad-miners-pptx-skill-v3.skill

# 다운로드 폴더가 없으면 생성
# mkdir -p ~/Downloads
```

---

### Step 6. 스킬 설치 (Linux)

> [!] **이미 설치한 적이 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `ls ~/.claude/skills/qmslide-check` 실행 시 폴더가 보이면 이미 설치된 것입니다.

```bash
# 설치 여부 확인 (폴더가 보이면 Skip)
ls ~/.claude/skills/qmslide-check 2>/dev/null

# -- 미설치 시 아래 실행 ------------------------------------------
# 1) 스킬 폴더 생성
mkdir -p ~/.claude/skills

# 2) .skill 파일을 .zip으로 복사 후 압축 해제
cp ~/Downloads/quad-miners-pptx-skill-v3.skill \
   ~/Downloads/quad-miners-pptx-skill-v3.zip

# 3) skills/ 폴더에 직접 압축 해제
# [!] 해제 후 shared/, qmslide-deck/ 등이 skills/ 바로 아래에 생성됩니다
unzip ~/Downloads/quad-miners-pptx-skill-v3.zip \
      -d ~/.claude/skills/

# 4) zip 파일 정리
rm ~/Downloads/quad-miners-pptx-skill-v3.zip
# ----------------------------------------------------------------
```

---

### Step 7. 폰트 설치 (Linux)

> [!] **이미 Noto Sans CJK KR 폰트가 설치되어 있다면 이 단계를 건너뛰세요.**
> 확인 방법: `fc-list | grep "Noto Sans CJK KR"` 실행 시 결과가 나오면 설치된 것입니다.

```bash
# 설치 여부 확인 (결과가 나오면 Skip)
fc-list | grep "Noto Sans CJK KR"

# 방법 A — apt로 설치 (Ubuntu/Debian)
# sudo apt install -y fonts-noto-cjk

# 방법 B — 자동 설치 스크립트 (소스 폴더에서 실행)
# cd ~/Downloads/QM_SLIDE_TEMPLATE_2026
# python3 scripts/install_fonts.py

# 방법 C — 수동 설치
# cp ~/.claude/skills/shared/assets/fonts/*.otf ~/.fonts/
# fc-cache -fv
```

---

### Step 8. Claude Code CLI 실행 및 스킬 확인 (Linux)

```bash
# 소스 폴더로 이동 (다운로드한 소스 위치에 맞게 변경)
cd ~/Downloads/QM_SLIDE_TEMPLATE_2026

# Claude Code 실행
claude

# Claude Code 채팅에서 설치 확인 (처음 설치 시 필수)
/qmslide-check
```

> [!] **`/qmslide-check` 후 모든 항목이 `[OK]`로 표시되면 설치 완료입니다.**
> 문제가 있는 항목은 `python3 scripts/check.py --fix` 로 자동 수정할 수 있습니다.

---

### Step 9. 샘플 슬라이드 생성으로 최종 검증 (Linux)

```
/qmslide-sample
```

현재 폴더에 `qm_sample.pptx` 파일이 생성됩니다.
LibreOffice Impress로 열어 아래 항목을 확인하세요.

```bash
# LibreOffice가 없으면 설치
# sudo apt install -y libreoffice

# 파일 열기
libreoffice --impress qm_sample.pptx
```

```
[OK] 모든 슬라이드 우상단에 Quad Miners 로고
[OK] 하단 푸터: QM 로고 + 저작권 + 페이지번호 + "Confidential"
[OK] 배경: 연청색 기하학 육각형 패턴
[OK] 폰트: Noto Sans CJK KR (한글 깨짐 없음)
[OK] 색상: 파랑 #2F6BFF, 다크 #111827
```

---

## 명령어 목록

> **참고**: `/qm` 은 과거 별칭(Alias)으로, 현재는 사용을 **비권장**합니다.
> (`/qmslide-deck` 을 사용하세요.)
> <!-- deprecated: /qm alias, use /qmslide-deck instead -->

### 슬라이드 생성

| 명령어 | 설명 |
|--------|------|
| `/qmslide-deck` | **전체 덱 생성** — 표지~마무리 완전한 덱 자동 생성 |
| `/qmslide-slide` | **단일 슬라이드** — 슬라이드 1장 생성 또는 수정 |
| `/qmslide-build` | **구성 지정 생성** — 슬라이드 타입 구성을 직접 지정 |
| `/qmslide-template` | **빈 템플릿** — 지정 타입의 편집 가능한 빈 양식 |

### 관리 및 확인

| 명령어 | 설명 |
|--------|------|
| `/qmslide-check` | **설치 확인** — 9가지 항목 전체 점검 (처음 설치 후 필수) |
| `/qmslide-sample` | **샘플 생성** — 6종 타입 완성 샘플 덱 즉시 생성 |
| `/qmslide-update` | **자동 업데이트** — GitHub 최신 버전 확인 및 적용 |
| `/qmslide-version` | **버전 확인** — 현재 버전 및 최신 버전 비교 |

### 브랜드 리소스

| 명령어 | 설명 |
|--------|------|
| `/qmslide-font` | **폰트 관리** — 설치, 확인, 웨이트 목록 |
| `/qmslide-logo` | **로고 조회** — 26개 공식 로고 파일 정보 |
| `/qmslide-color` | **컬러 조회** — 팔레트 코드 및 사용 가이드 |
| `/qmslide-qa` | **품질 검사** — .pptx 브랜드 가이드라인 준수 검사 |

---

## 사용 예시

### Claude Code CLI에서

```
/qmslide-deck Network Blackbox 2026 제품 소개서 만들어줘

/qmslide-slide compare NDR vs Network Blackbox 비교표

/qmslide-build title+toc(5)+section+content(3)+compare+closing  NDR 제안서

/qmslide-sample

/qmslide-qa output.pptx
```

### 자연어로도 동작합니다

슬래시 명령어 없이 자연어 요청도 스킬이 적용됩니다.

```
"Quad Miners 공식 스타일로 NDR 제안서 슬라이드 만들어줘"
"Network Blackbox 소개 발표 자료 10장으로 생성해줘"
```

### Python CLI로 직접 실행 (소스 폴더에서)

```bash
# 설치 확인
python3 scripts/check.py

# 샘플 생성 (qm_sample.pptx)
python3 scripts/sample.py

# 업데이트 확인
python3 scripts/autoupdate.py --check-only
```

> Windows에서는 `python3` 대신 `python` 을 사용하세요.

---

## 브랜드 가이드라인 요약

### 컬러 팔레트

| 색상명 | 코드 | 주요 용도 |
|--------|------|-----------|
| Cyan | `#00D8FF` | 구분선 accent, 데이터 시각화 |
| Blue | `#2F6BFF` | CTA, 섹션번호, 강조 텍스트 |
| Purple | `#7A5CFF` | 보조 강조색 |
| Dark | `#111827` | 메인 텍스트, 헤더 |
| White | `#FFFFFF` | 슬라이드 배경 |

### 폰트

- **전용 폰트**: `Noto Sans CJK KR` (다른 폰트 사용 절대 금지)
- **최소 크기**: 12pt 이상
- **웨이트**: Black / Bold / Medium / Regular / DemiLight / Light / Thin

### 슬라이드 규격

- **크기**: 16:9 (33.87cm × 19.05cm)
- **EMU**: 12,192,000 × 6,858,000
- **배경**: 흰색 (`#FFFFFF`)

### 슬라이드 타입

| 타입 | 이름 | 용도 |
|------|------|------|
| TYPE 1 | 표지 (title) | 프레젠테이션 첫 장 |
| TYPE 2 | 목차 (toc) | 섹션 목차 2×N 그리드 |
| TYPE 3 | 섹션간지 (section) | 섹션 구분 페이지 |
| TYPE 4 | 2열 본문 (split) | 텍스트 + 이미지 |
| TYPE 5 | 데이터 시각화 (data-viz) | 차트 3열 패널 |
| TYPE 6 | 이미지 (image-layout) | 1/2/3-Up 레이아웃 |
| TYPE 7 | 타이포그래피 | 폰트/컬러 가이드 슬라이드 |
| TYPE 8 | 마무리 (closing) | Thank You + QR코드 |

---

## 자주 발생하는 문제

### 슬래시 명령어가 "Unknown command"로 표시되는 경우

Claude Code CLI에서 `/qmslide-deck` 등 명령어가 인식되지 않으면:

1. 스킬 디렉토리 위치 확인:

```bash
# macOS / Linux
ls ~/.claude/skills
# shared, qmslide-deck, qmslide-slide 등 폴더가 바로 보여야 합니다

# Windows (PowerShell)
# ls "$env:USERPROFILE\.claude\skills"
```

2. Claude Code 재시작 (새 탑레벨 디렉토리는 재시작 필요):

```bash
# Claude Code 종료 후 재실행
claude
```

### 한글이 깨지는 경우 (네모 또는 물음표로 표시)

Noto Sans CJK KR 폰트가 설치되지 않은 경우입니다.
각 OS별 Step 7을 다시 실행하거나 수동으로 설치하세요.

```bash
# macOS / Linux — 자동 수정
python3 scripts/install_fonts.py

# Linux — apt로 설치
# sudo apt install -y fonts-noto-cjk

# Windows — 수동 설치
# .claude\skills\shared\assets\fonts\ 에서 .otf 파일 우클릭 -> 설치
```

### 설치 확인 항목 중 일부가 실패하는 경우

```bash
python3 scripts/check.py --fix
# Windows: python scripts\check.py --fix
```

자동으로 Python 패키지 재설치, 폰트 복사, 디렉토리 생성 등을 수행합니다.

---

## 스킬 업데이트

### 자동 업데이트 (Claude Code에서)

```
/qmslide-update
```

### 수동 업데이트 (GitHub에서)

> [!] **v1.x, v2.x, v3.0.0에서 v3.1.0으로 업그레이드하는 경우, 기존 폴더명이 다를 수 있습니다.**
> 기존에 `quad-miners-pptx-skill/` 이름으로 설치한 경우 아래처럼 백업 후 새로 설치하세요.

```bash
# macOS / Linux
# 1) 기존 스킬 백업 (이미 설치한 적 없으면 Skip)
# mv ~/.claude/skills/quad-miners-pptx-skill \
#    ~/.claude/skills/quad-miners-pptx-skill.bak

# 2) Releases 페이지에서 최신 .skill 다운로드 후 Step 6 재실행
```

```powershell
# Windows
# 1) 기존 스킬 백업 (이미 설치한 적 없으면 Skip)
# Rename-Item "$env:USERPROFILE\.claude\skills\quad-miners-pptx-skill" `
#             "quad-miners-pptx-skill.bak"

# 2) Releases 페이지에서 최신 .skill 다운로드 후 Step 5 재실행
```

---

## GitHub 저장소 업데이트 방법

```bash
# 1) 현재 상태 확인
git status

# 2) 변경 파일 전체 추가
git add -A

# 3) 커밋
git commit -m "feat: v3.0.0 — Harness Engineering 완전 적용 (DSL 지시어 + Output Schema Binding + Guard Clause)

주요 변경사항:
- 스킬 루트 폴더명 변경: skill_rebuilt -> qmslide
- 스킬 구조를 명령어별 개별 디렉토리로 분리 (12개)
- 명령어명 언더스코어->하이픈 수정 (Claude Code 규격 준수)
  예: /qmslide_deck -> /qmslide-deck
- /qm alias 제거 (비권장 처리)
- shared/ 폴더로 공유 assets/scripts/references 통합
- README.md 전면 재작성 (Windows/macOS/Linux 설치 가이드 분리, Skip 안내 포함)
- PDF 가이드 재생성"

# 4) 푸시
git push origin main
```

새 `.skill` 파일은 GitHub -> **릴리즈 (Releases) -> 새 릴리즈 (New release)** 에서
`v3.1.0` 태그로 업로드하세요.

---

## 문의

**Quad Miners 전략기획팀**으로 문의하세요.

이 스킬의 기능 개선 요청, 버그 제보, 브랜드 가이드라인 관련 질문은
모두 전략기획팀을 통해 접수됩니다.
