# OZ Calendar — Antigravity 설치 가이드

> 사이드바에 달력 + 날짜별 문서 + Google Calendar + 커맨드 바를 표시하는 확장

---

## 호환성

| 항목 | 지원 |
|------|------|
| **플랫폼** | Windows / macOS / Linux |
| **IDE** | Antigravity (VS Code 호환 IDE) |
| **엔진** | VS Code ^1.80.0 이상 |
| **의존성** | 없음 (순수 JavaScript, 빌드 불필요) |

### 플랫폼별 자동 처리

| 항목 | Windows | macOS / Linux |
|------|---------|---------------|
| gogcli 경로 | `%HOME%/AppData/Local/gogcli/gog.exe` | `/usr/local/bin/gog` |
| 단축키 | `Ctrl+Alt+B` | `Cmd+Alt+B` |
| 파일 경로 구분자 | `\` → `/` 자동 변환 | `/` 네이티브 |
| Obsidian URI | `obsidian://open` (동일) | `obsidian://open` (동일) |

`extension.js`에서 `process.platform`으로 OS를 감지하여 자동 분기하므로 별도 설정 불필요.

---

## 설치 파일

**`oz-calendar-vscode-1.0.0.vsix`** (14KB)

소스 폴더(`10-projects/oz-calendar-vscode/`)에 포함되어 있음.

### VSIX 직접 빌드 (선택)

```bash
cd oz-calendar-vscode
npx @vscode/vsce package --allow-missing-repository
```

---

## 설치 방법

### 방법 1 — GUI (권장)

1. `.vsix` 파일을 대상 PC로 전송 (USB, AirDrop, 클라우드 등)
2. Antigravity 실행
3. `Ctrl+Shift+P` (Mac: `Cmd+Shift+P`) → **"Extensions: Install from VSIX..."** 선택
4. `oz-calendar-vscode-1.0.0.vsix` 파일 선택
5. IDE 재시작

### 방법 2 — 터미널

```bash
antigravity --install-extension oz-calendar-vscode-1.0.0.vsix
```

### 방법 3 — 수동 복사

```bash
# 확장 폴더 생성
mkdir -p ~/.antigravity/extensions/rockuen.oz-calendar-vscode-1.0.0

# 소스 파일 복사
cp extension.js package.json ~/.antigravity/extensions/rockuen.oz-calendar-vscode-1.0.0/
```

IDE 재시작 후 적용.

---

## 설치 후 설정

### 필수 사항

- 없음. 설치만 하면 달력 + 파일 탐색 + 커맨드 바는 바로 동작함.

### 권장 사항

#### Obsidian 연동

md/canvas 파일 클릭 시 Obsidian에서 열려면:

1. Obsidian 설치
2. Obsidian에서 워크스페이스 폴더를 Vault로 등록
3. **Vault 이름이 워크스페이스 폴더명과 일치**해야 함

예: 워크스페이스 폴더가 `iloom-workspace`이면 Obsidian Vault 이름도 `iloom-workspace`

> Obsidian이 없으면 md/canvas 파일은 IDE 에디터에서 열림 (기능 저하 없음)

#### Google Calendar 연동

사이드바에 일정을 표시하려면:

1. gogcli 바이너리 설치

| OS | 설치 경로 |
|----|----------|
| Windows | `%HOME%/AppData/Local/gogcli/gog.exe` |
| macOS / Linux | `/usr/local/bin/gog` |

2. Google 계정 인증 (최초 1회)

```bash
gog auth login
```

> gogcli가 없어도 달력 + 파일 탐색 + 커맨드 바는 정상 동작함. 캘린더 일정만 표시되지 않음.

---

## 설치 확인

1. IDE 좌측 Activity Bar에 달력 아이콘(📅)이 표시되는지 확인
2. `Ctrl+Alt+B` (Mac: `Cmd+Alt+B`)로 사이드바 토글
3. 워크스페이스에 `YYMMDD` 접두사 파일이 있으면 달력에 컬러 도트 표시

---

## 문제 해결

| 증상 | 원인 | 해결 |
|------|------|------|
| 달력 아이콘이 안 보임 | 확장 미설치 또는 비활성 | Extensions에서 "Calendar" 검색하여 활성화 |
| 사이드바가 왼쪽에 표시됨 | 기본 위치가 Activity Bar | 달력 탭을 드래그하여 오른쪽 사이드바로 이동 (최초 1회) |
| md 파일이 IDE에서 열림 | Obsidian 미설치 또는 Vault 이름 불일치 | Vault 이름을 워크스페이스 폴더명과 일치시키기 |
| Google 일정이 안 보임 | gogcli 미설치 또는 인증 만료 | `gog auth login`으로 재인증 |
| 일정 로딩이 느림 | 네트워크 지연 (타임아웃 15초) | 네트워크 상태 확인 |

---

## 제거

### GUI

`Ctrl+Shift+P` → **"Extensions: Uninstall"** → "Calendar" 선택

### 수동

```bash
rm -rf ~/.antigravity/extensions/rockuen.oz-calendar-vscode-1.0.0
```

---

## 파일 구성

```
oz-calendar-vscode/
├── extension.js       # 확장 메인 코드 (~950 lines)
├── package.json       # 확장 매니페스트
├── README.md          # 확장 설명
├── INSTALL.md         # 이 문서
└── oz-calendar-vscode-1.0.0.vsix  # 배포용 패키지
```
