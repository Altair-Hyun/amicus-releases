# Amicus Releases

**Desktop AI Agent — 대화만으로 컴퓨터의 모든 작업을 수행합니다.**

최신 버전은 [Releases](https://github.com/Altair-Hyun/amicus-releases/releases)에서 내려받으세요.

| Platform | File |
|----------|------|
| **macOS** (Universal) | `Amicus-<version>-universal.dmg` |
| **Windows** (x64) | `Amicus Setup <version>.exe` |

---

## 시작하기 (사전 작업)

### macOS — 서명 안 된 앱 실행
Amicus는 코드 서명이 없어 첫 실행 시 "알 수 없는 개발자" 경고가 뜹니다. 설치 후 아래를 실행하세요:

```sh
xattr -cr /Applications/Amicus.app
```

### Python 3.11 이상 (필수)
Amicus는 Python을 번들하지 않습니다. 백엔드가 Python 사이드카로 동작하므로, Python이 없으면 앱은 켜지되 자동화·세션·에이전트 루프가 동작하지 않습니다.

| OS | 설치 |
|----|------|
| **Windows** | `winget install Python.Python.3.12` (또는 [python.org](https://www.python.org/downloads/windows/)에서 설치 시 **"Add python.exe to PATH"** 체크) |
| **macOS** | `brew install python@3.12` |

> 3.11 미만은 지원하지 않습니다. Python 패키지는 첫 실행 시 `~/.amicus/amicus`에 **자동 설치**됩니다(사용자 조치 불필요).

### Windows — Git Bash 필수
Amicus의 셸 도구는 Windows에서 Git Bash로 Unix 명령(`cat`·`grep`·`sed` 등)을 실행합니다. [Git for Windows](https://gitforwindows.org/)를 설치하세요. (없으면 PowerShell로 제한 동작합니다.)

---

## 패치노트

<!-- AUTO-APPEND: 태그 push마다 이 줄 바로 아래에 최신 릴리스 섹션이 추가됩니다. -->
### v1.9.7-smoke.41 — 2026-10-30

**추가**
- User Prompt를 표로 바꿔 규칙마다 **Global · Chat · Workflow · Notification** 네 칸을 체크합니다. Global·Chat은 자동으로 들어가고, Workflow·Notification은 그 화면의 목록에만 보입니다. 여러 칸을 함께 켤 수 있고, Global을 켜면 나머지 칸이 잠기며 끄면 이전 체크로 돌아옵니다. 화면은 와처·워크플로우와 같은 패널 형식입니다.
**변경**
- 일반 채팅에는 Global·Chat 규칙이, 알림 분석 채팅에는 Global 규칙만, 워크플로우 AI 단계에는 Global 규칙과 그 단계에서 고른 규칙이 들어갑니다.
- 업데이트 전에 켜 둔 규칙은 Chat, 꺼 둔 규칙은 미사용으로 옮겨집니다. 그래서 업데이트 직후 알림 분석 채팅에는 기존에 켜 둔 규칙이 들어가지 않으니, 필요하면 Global이나 Notification을 켜세요. 이전 버전 앱으로 돌아가도 채팅 규칙은 같게 동작합니다.
- 워크플로우 단계와 알림 상세 목록에는 그 칸을 체크한 규칙과 이미 고른 규칙만 보이고, Global 규칙은 체크된 채 잠깁니다. 해제한 행은 화면을 보는 동안 남아 다시 체크할 수 있습니다. 새 규칙은 미사용으로 추가됩니다.
- 앱 도움말의 알림 분석·워크플로우 AI 단계·설정 안내를 새 칸 기준으로 고쳤습니다.
**수정**
- 8초 뒤 실행 배너의 650ms 직선 이동을 OS 동작 줄이기 설정에서도 유지합니다. 상단 현재 작업 오버레이가 이동 중 배너를 잘라 가리던 문제도 고쳤습니다. 긴 작업 목록은 기존 내부 영역에서 스크롤하며, STOP·종료·채팅/실행 변경·분할 크기 변경 시 이동 정리는 유지합니다.
- 다른 애니메이션의 동작 줄이기 정책은 이번에 바꾸지 않았습니다.

### v1.9.7-smoke.40 — 2026-10-30

**추가**
- 알림 상세에서 AI 분석 요청에 쓸 User Prompt를 고를 수 있고, 아무것도 고르지 않으면 기존 기본 분석 지시로 보냅니다.
- 고른 프롬프트는 와처별로 기억되어 같은 와처의 다음 알림을 열면 미리 체크됩니다.
- 패널이 넓으면 오른쪽에 실제로 보낼 내용이 그대로 미리 보입니다.
**변경**
- User Prompt에서 켜 둔 항목은 알림 목록에서 "항상 적용"으로 체크된 채 잠기며 메시지에 다시 들어가지 않습니다.

### v1.9.7-smoke.39 — 2026-10-29

**추가**
- 관리자가 이메일로 직접 등록한 사용자도 Google 로그인 버튼으로 첫 로그인부터 들어올 수 있습니다.
**수정**
- 로그인 계정 확인 과정의 보안 문제를 수정했습니다.

### v1.9.7-smoke.38 — 2026-10-29

**변경**
- 채팅 목록의 완료·중지 표시가 이미 확인했고 어느 창에도 열려 있지 않은 지난 세션에서는 흐린 색으로 보입니다.
- 도우미 카드의 요약 줄이 맡긴 일을 글로 보여줍니다.
**수정**
- 다시 열었을 때 도우미가 부른 도구 카드가 도우미 카드 밖에 따로 쌓이던 문제를 고쳤습니다.

### v1.9.7-smoke.37 — 2026-10-29

**추가**
- Codex 구독 대화에서 도우미(서브에이전트)를 쓸 수 있으며, 도우미의 작업이 카드 안에 표시되고 승인도 도우미 이름과 함께 뜹니다.
- 채팅창 위쪽에 지금 진행 중인 작업만 겹쳐 보이는 오버레이를 추가했습니다.
**변경**
- 도우미가 부른 도구 카드가 실행 중 그 도우미 카드 밑에 붙어 표시됩니다.
**수정**
- 진행 배너와 미확인 완료 채팅의 순환 테두리가 화면을 부드럽게 그리도록 개선해 부하를 줄였습니다.

### v1.9.7-smoke.36 — 2026-10-29

**변경**
- Claude 구독 대화에서 실패하거나 중지한 뒤 다음 메시지를 보내면 같은 세션을 이어받아, 이미 한 조회를 처음부터 다시 하지 않습니다.
- 백그라운드 도우미가 도구를 여러 번 부르면 하나의 메시지로 묶이고 "Agent 작업" 배지가 붙습니다.
**수정**
- 본문 없이 끝난 작업의 도구 카드가 앱을 다시 열면 사라지던 문제를 고쳤습니다.
- 도우미 호출마다 본문 없는 메시지가 하나씩 생기던 화면을 고쳤습니다.

### v1.9.7-smoke.35 — 2026-10-28

**변경**
- AI가 여러 파일·대상을 다룰 때 호출을 반복하지 않고 스크립트 한 번으로 처리하도록 지침을 정리했습니다.
- Explore 도우미가 셸과 Python으로 여러 대상을 한 번에 읽고, 모호한 점은 메인에 보고해 질문 카드로 묻습니다.
**수정**
- 메인 답이 끝난 뒤 백그라운드 도우미가 부른 도구가 조용히 실패하던 문제를 고쳤습니다.
- 도우미 호출이 남아 실행이 실패하고 같은 대화가 잠기던 문제를 막았습니다.
- "전체 승인"이 턴이 끝난 뒤에도 남아 백그라운드 도우미의 도구가 묻지 않고 실행되던 문제를 고쳤습니다.
- Claude 구독의 일시적인 서버 장애는 첫 출력 전이면 자동으로 다시 시도합니다.

### v1.9.7-smoke.34 — 2026-10-28

**수정**
- 응답 없는 실행 상태 조회가 채팅창마다 대기를 계속 쌓던 문제를 막아 메모리 사용을 줄였습니다.
- 채팅을 삭제하거나 초기화할 때 백그라운드 작업과 읽음 위치가 함께 정리됩니다.
- 채팅 완료·미확인 표시가 재진입과 앱 재시작 뒤에도 복원됩니다.
- 와처 이력에서 같은 항목이 중복 표시되던 문제를 막았습니다.

### v1.9.7-smoke.33 — 2026-10-28

**수정**
- OS의 동작 줄이기 설정에서도 진행·미확인 완료 애니메이션이 속도를 낮춰 계속 움직이며 상태를 알립니다.
- 와처 소스 버튼과 상세 액션 버튼에 동작 줄이기 전환 제한이 적용되지 않던 문제를 고쳤습니다.

### v1.9.7-smoke.32 — 2026-10-28

**변경**
- 와처 생성·편집 화면을 소스·조건·알림 섹션으로 나누고 명령·URL·파일·Slack을 버튼으로 선택합니다.
- 와처 상세의 소스·조건·동작·이력·원본 데이터를 같은 열에 정렬하고 이력·원본·AI 결과를 접고 펼 수 있으며, 정확한 확인·매치 시각을 상단 통계에 표시합니다.
- 워크플로우 생성·편집도 같은 섹션 구조로 바뀌어 단계 유형 선택, 스텝별 번호, Shell 줄 번호를 제공하고 상세는 통계·실행 단계·실행 이력으로 정리됩니다.

### v1.9.7-smoke.31 — 2026-10-27

**변경**
- 채팅 진행 배너가 8초 뒤 하단에서 상단으로 자연스럽게 이동하고 메시지 영역도 함께 자리를 조정합니다.

### v1.9.7-smoke.30 — 2026-10-27

**변경**
- 와처 편집 화면의 "전체 페이지 수집"을 토글로 표시하고, 요청 파라미터·응답 경로·페이지당 건수를 2열로 배치하며 실제 요청 모양을 안내 표로 보여줍니다.
- "종료 중 이벤트 복구" 라벨과 이력 조회 입력(시작 시각·기간·쿼리 이름)의 배치를 다른 필드와 맞췄습니다.

### v1.9.7-smoke.29 — 2026-10-27

**변경**
- 진행 배너에 순환 테두리와 회전 링을 적용하고 중지 버튼을 진한 빨강 "STOP"으로 강조했습니다.
- 채팅 목록에서 세션별 진행중·완료·실패·중지 상태를 표시하고, 아직 확인하지 않은 완료는 초록색 빛이 테두리를 돌다가 채팅을 열면 멈춥니다.
- 백그라운드 배너의 기본 제목에 "Amicus AI Agent"를 표시합니다.

### v1.9.7-smoke.28 — 2026-10-27

**수정**
- 와처 상세의 "이전 이력 더 보기" 버튼을 없애고 이력 끝에서 이전 페이지를 자동으로 불러오며, 조건·아웃풋을 항목별 세로 배치로 표시합니다.
- 채팅창에 마우스를 올리기만 해도 Process 출력이 바뀌던 동작을 채팅창을 클릭할 때 전환되도록 고쳤습니다.

### v1.9.7-smoke.27 — 2026-10-26

**추가**
- 채팅창에 마우스를 올리면 공용 Process가 해당 채팅의 출력으로 전환되고, 출력 제목 옆 핀 버튼으로 대상을 고정할 수 있습니다.
**변경**
- 번들 Codex를 0.164.0으로 올리고, OpenAI (ChatGPT)도 채팅별 모델과 Effort를 선택할 수 있습니다.
- Claude/OpenAI의 BOM 인증 탭과 커스텀 경로 저장을 제거했으며, 공식 API 연결에는 새 키 입력이 필요합니다.
- Claude/OpenAI 인증 탭은 처음에 OAuth를 보여주고 이후 마지막으로 선택한 탭을 기억합니다.
**수정**
- Codex 초기화가 응답 없이 멈추면 30초 뒤 정리하고, 모델 조회만 실패한 경우 재시도를 안내합니다.

### v1.9.7-smoke.26 — 2026-10-26

**변경**
- 채팅의 추론 수준 선택기 앞에 "Effort:" 라벨을 표시합니다.
- AI 제공자를 설정에서 공통으로 선택하도록 하고 채팅 상단의 제공자 선택기를 제거했으며, 모델과 추론 수준은 채팅별로 유지됩니다.

### v1.9.7-smoke.25 — 2026-10-23

**변경**
- 전역 화면 분할·채팅 추가 툴바를 없애고 각 채팅 헤더에 출력 버튼을 두어, 공용 Process에 선택한 채팅의 로그와 실행 상태만 표시합니다.
- 셸·Python 출력과 Claude 내장 도구 로그를 채팅별로 보존하고, 채팅을 삭제하면 해당 출력도 정리됩니다.
**수정**
- 출력 전환 뒤 이전 채팅 로그가 다시 나타나던 문제를 고쳤습니다.
- 800×600 최소 화면에서도 출력 닫기와 각 채팅의 출력 버튼·입력창을 조작할 수 있게 했습니다.

### v1.9.7-smoke.24 — 2026-10-23

**추가**
- 채팅을 화면·좌우·상하·최대 4개 배치로 분할해 열고, 경계 크기 조절과 확대·복원을 지원합니다. 창을 닫아도 실행은 중지되지 않습니다.
**변경**
- 자동 요약 제목의 글자 수 제한을 없애고 6단어 이하로 생성합니다.
**수정**
- 채팅 자동 제목 생성이 동작하지 않아 첫 질문 앞 30자가 그대로 남던 문제를 고쳤습니다.

### v1.9.7-smoke.23 — 2026-10-21

**추가**
- 계정별로 보여줄 AI 제공자를 관리자가 설정할 수 있습니다.
**수정**
- H-Chat 저장 키가 입력칸에 복원되고 Show/Hide로 확인할 수 있습니다.
- H-Chat에서 현재 제공자·모델을 선택하면 "Use this provider" 버튼 대신 ACTIVE가 표시됩니다.
- Claude가 커밋하거나 PR을 만들 때 자동으로 붙던 공동 작성자·생성 문구를 끄도록 고쳤습니다.

### v1.9.7-smoke.22 — 2026-10-21

**수정**
- 채팅 실행 상태 조회가 같은 이벤트를 중복 전송하던 경로를 줄여 메모리 사용을 낮췄습니다.
- 완료된 답변이 저장된 뒤에는 화면의 이벤트 데이터를 회수해 메모리를 줄였습니다.
- 긴 도구 출력은 미리보기만 먼저 보여주고, 도구 카드를 펼칠 때 나눠서 불러오며 접으면 해제합니다.

### v1.9.7-smoke.21 — 2026-10-20

**변경**
- H-Chat Claude에서 Save할 때마다 키를 다시 검증하고 확인 중·완료·실패·미확인 상태를 표시합니다.
- H-Chat 신규 설정에 문서 주소·모델이 기본 입력되고 Claude 인증 방식 선택을 없앴으며, 키 검증과 자동 설정을 Save 시 수행합니다.

### v1.9.7-smoke.20 — 2026-10-20

**추가**
- Processes 출력에서 드래그 선택을 마치면 선택한 텍스트가 자동으로 클립보드에 복사됩니다.

### v1.9.7-smoke.19 — 2026-10-20

**추가**
- URL 와처에서 선택형 페이지 수집(기본 50건)을 지원하며, 전체 병합 후 조건을 검사하고 불완전 수집은 실패로 처리합니다.
**수정**
- URL 와처의 응답 크기 제한을 8 MiB로 확대했습니다.

### v1.9.7-smoke.18 — 2026-10-20

**변경**
- H-Chat이 Claude/Codex 에이전트 엔진을 쓰도록 바뀌었으며, 전용 설정 화면과 저장·해제 기능을 제공합니다.
- Claude/OpenAI OAuth 게이트웨이는 새로 설정할 때 사용 꺼짐·빈 주소로 시작하고, 이미 저장한 설정은 업데이트 뒤에도 유지됩니다.

### v1.9.7-smoke.17 — 2026-10-19

**추가**
- 와처 수집 이력을 저장하고, 원본이 과거 조회를 제공하면 앱이 꺼져 있던 동안의 이벤트를 복구하는 설정을 추가했습니다.
- 작업 상태·실패를 보여주고 명시적으로 재시도하는 화면을 추가했으며, 앱 종료 시 실행 중이던 작업은 자동 반복하지 않고 실패로 보존합니다.
- 앱 활성화·잠금 해제·절전 복귀 시 프로세스와 메모리 상태를 진단합니다.
**수정**
- 여러 워크플로우가 연결된 와처의 실행 순서와 동시 실행 경합을 고치고, 실패가 완료로 기록되거나 반복되던 문제를 수정했습니다.
- 앱이 종료되는 순간 와처 이벤트가 유실될 수 있던 문제를 고쳤습니다.

### v1.9.7-smoke.16 — 2026-10-07

**수정**
- 채팅 상단 작업 목록이 쌓여 본문을 밀어내던 문제를 고쳐, 목록 높이 제한과 내부 스크롤, 상태별 개수, 접기·펼치기를 제공합니다.

### v1.9.7-smoke.15 — 2026-10-06

**추가**
- 게이트웨이 테스트와 연동 검증을 보강했습니다.
**수정**
- Claude 인증 프로세스 종료 실패 뒤 Login이 계속 막히던 문제를 고쳤습니다.
- 자동 상태 조회나 정리 실패가 최초 로그인 오류를 덮어쓰던 문제를 고쳤습니다.
- Claude Remote Control 연결이 거절되면 원인 진단을 보강하고, 서버에서 사라진 세션만 저장된 연결 정보를 해제합니다.
- Claude 로그인 주소가 허용 목록 불일치로 거부되던 문제를 고쳤습니다.

### v1.9.7-smoke.14 — 2026-09-21

**수정**
- AWS SSO 로그인에서 브라우저가 열리지 않고 주소만 출력되던 문제를 고쳤습니다.

### v1.9.7-smoke.13 — 2026-09-21

**수정**
- 로그인되어 있어도 접힌 제공자 카드의 표시등이 빨간 불로 보이던 문제를 고쳤습니다.
- 아직 확인하지 못한 상태를 실패 색 대신 회색으로 표시합니다.

### v1.9.7-smoke.12 — 2026-09-21

**추가**
- 턴이 끝난 뒤 확정된 백그라운드 도구의 결과도 대화 기록에 저장됩니다.
**변경**
- 도구 카드는 그 안에 아직 실행 중인 작업이 있는지에 따라 접히고, 직접 누른 선택은 유지됩니다.
- 모델 목록을 한 시간 동안 재사용하고, 로그인 직후에는 목록을 새로 읽습니다.
**수정**
- 도구가 끝났는데도 진행 배너가 계속 돌던 문제를 고쳤습니다.
- "결과 없음" 카드가 터미널 패널과 세션 잠금에서는 실행 중으로 취급되던 문제를 고쳤습니다.
- 이미 끝난 도구가 실행 중으로 되돌아가던 문제를 고쳤습니다.
- 카탈로그 조회 실패로 모델 목록이 비고 대화가 막히던 문제를 고쳤습니다.
- 프로세스를 종료하는 중에 새로 생긴 하위 프로세스가 남아 모델 목록과 대화를 막던 문제를 고쳤습니다.

### v1.9.7-smoke.11 — 2026-09-19

**추가**
- Claude 내장 도구(Bash, Read, Grep 등)의 시작과 결과 요약이 프로세스(Output) 탭에 표시됩니다.
**변경**
- 도구 카드 라벨에서 명령어 종류를 나타내던 접미사를 없앴습니다.
- 인증 복구 안내를 특정 명령에 고정하지 않고, 자격 증명이 실제로 쓰는 갱신 방법을 따르게 했습니다.
- 로그인 명령을 모양으로 알아봐 긴 대기 시간을 적용합니다.
**수정**
- 프로세스 탭의 줄 수가 항상 1줄씩 많게 표시되던 문제를 고쳤습니다.

### v1.9.7-smoke.10 — 2026-09-18

**추가**
- 지난 대화를 다시 열면 도구 카드가 복원되고, 카드에 실행한 명령어가 표시됩니다.
**변경**
- 채팅 본문과 도구 카드를 저장소 기준으로 표시하며, 결론(Summary/Result)은 실행이 끝났을 때만 나옵니다.
- 타자기 효과를 속도 상한 방식으로 바꿔 분량이 많아도 끝까지 자연스럽게 출력됩니다.
**수정**
- 백그라운드 위임이 끝난 뒤 이어지는 본문이 화면에 닿지 않던 문제를 고쳤습니다.
- Claude 도구 카드가 저장에서 빠지거나 명령어가 비어 있던 문제를 고쳤습니다.
- 스트리밍 중 라벨이 중간에서 끊겨 반쪽으로 그려지던 문제를 고쳤습니다.
- 완료가 기록되지 않은 위임 카드를 Done으로 표시하던 문제를 고쳐 "결과 없음"으로 보여줍니다.
- 위임 카드의 실행 내용과 결과가 뒤바뀌어 저장되던 문제를 고쳤습니다.

### v1.9.7-smoke.10 — 2026-09-18

**추가**
- 지난 대화를 다시 열면 도구 카드가 복원되고, 카드에 실행한 명령어가 표시됩니다.
**변경**
- 채팅 본문과 도구 카드를 저장소 기준으로 표시하며, 결론(Summary/Result)은 실행이 끝났을 때만 나옵니다.
- 타자기 효과를 속도 상한 방식으로 바꿔 분량이 많아도 끝까지 자연스럽게 출력됩니다.
**수정**
- 백그라운드 위임이 끝난 뒤 이어지는 본문이 화면에 닿지 않던 문제를 고쳤습니다.
- Claude 도구 카드가 저장에서 빠지거나 명령어가 비어 있던 문제를 고쳤습니다.
- 스트리밍 중 라벨이 중간에서 끊겨 반쪽으로 그려지던 문제를 고쳤습니다.
- 완료가 기록되지 않은 위임 카드를 Done으로 표시하던 문제를 고쳐 "결과 없음"으로 보여줍니다.
- 위임 카드의 실행 내용과 결과가 뒤바뀌어 저장되던 문제를 고쳤습니다.

### v1.9.7-smoke.9 — 2026-09-18

**추가**
- Claude 구독에서 서브에이전트를 다룰 수 있으며, 서브에이전트의 도구가 그것을 띄운 카드 안에 묶여 표시되고 질문·중단도 지원합니다.
- 진행 중임을 움직임으로 보여주고, 도구 카드가 사용자를 기다리는 중임도 표시합니다.
**변경**
- Claude 네이티브 도구 카드에 색을 주고 흐린 글자의 대비를 높였습니다.
- 사이드바 패널을 열면 설정 오버레이가 닫히고 설정 닫기 버튼을 없앴습니다.
**수정**
- 진행 중인 로그인이 설정 화면·상태 표시줄·모델 선택기의 연결 상태 조회를 모두 멈추게 하던 문제를 고쳤습니다.
- 앱을 다시 켜면 로그인이 풀린 것처럼 보이거나 확인 전 상태가 "연결 필요"로 표시되던 문제를 고쳤습니다.
- 제공자 카드 전체가 10초마다 회색이 되던 문제와 연결 상태·모델 목록을 불필요하게 자주 다시 조회하던 동작을 고쳤습니다.
- 끊긴 도구를 실패 대신 중단으로 표시합니다.

### v1.9.7-smoke.8 — 2026-09-16

**추가**
- 설정에 Plugins·Skills·MCP Servers를 추가해 설치한 확장을 모든 AI가 공통으로 쓸 수 있습니다.
- 공식 마켓플레이스 4곳을 기본 제공하며 폴더·owner/repo·저장소 주소로 직접 추가할 수 있습니다.
- MCP Servers에서 공식 레지스트리를 탐색하고 고른 서버를 바로 추가할 수 있습니다.
- 설정을 왼쪽 카테고리 탐색과 넓은 본문으로 개편했습니다.
**변경**
- Plugins·Skills·MCP Servers가 탭·검색·카드 목록·상세 패널의 같은 화면 규칙을 쓰고, 꺼진 플러그인의 MCP 서버는 "꺼짐"으로 남깁니다.
**수정**
- 스킬 호출이 "Unknown command"로 끝나던 문제를 고쳤고, 손으로 입력한 스킬 이름도 바꿔 보냅니다.
- 공식 마켓플레이스 카탈로그를 읽지 못하던 문제와 일부 플러그인이 설치되지 않던 문제를 고쳤습니다.
- Claude·Codex 연결이 끊긴 뒤 저장된 공식 로그인으로 연결을 복구하고, 확인 오류를 로그아웃으로 단정하지 않습니다.

### v1.9.7-smoke.7 — 2026-09-16

**변경**
- 탐색기의 파일 변경 알림이 보이는 폴더와 영향받은 Git 저장소만 갱신하도록 바뀌어 조회·감시 부담이 줄었습니다.
- 사용하지 않는 루트의 파일 감시를 해제하고 중복 감시를 공유합니다.
- 에디터는 변경된 탭만 확인하며 미저장 내용과 충돌 경고를 보존합니다.

### v1.9.7-smoke.6 — 2026-09-16

**추가**
- 설정에서 앱 버전과 새 버전을 확인하며, Windows는 앱 안에서 다운로드·설치·재시작하고 Mac은 DMG를 내려받아 수동 설치합니다.
**변경**
- 채팅·와처·워크플로우·템플릿·알림 등 저장 목록이 변경 알림으로 즉시 갱신됩니다.
**수정**
- 다른 사이드바를 다녀와야 파일 추가·삭제와 Git 색상·배지가 반영되던 문제를 고쳤습니다.
- 오래된 캐시가 최신 목록을 덮어쓰거나 삭제한 항목을 다시 보여주던 문제를 고쳤습니다.

### v1.9.7-smoke.5 — 2026-09-16

**변경**
- 앱의 게이트웨이 HTTPS 연결을 로그인 세션별로 재사용해 반복 요청의 응답이 빨라집니다.
- 게이트웨이의 브라우저 관리와 중계 기능을 분리해 안정성을 높였습니다.
**수정**
- 게이트웨이의 소유권 갱신을 분리해 일시적인 저장소 오류에서 자동으로 복구됩니다.

### v1.9.7-smoke.4 — 2026-09-14

**변경**
- 저장된 앱 로그인 세션이 없으면 자동으로 브라우저를 열지 않고 "Google 계정으로 계속" 버튼을 누를 때까지 기다립니다.
- 로그인 화면을 "Google 계정으로 계속" 버튼 하나로 통합했고, 대기·거부 후에도 버튼으로 다시 인증할 수 있으며 실패 안내가 한 줄로 줄었습니다.

### v1.9.7-smoke.3 — 2026-09-14

**변경**
- Integrations의 Google을 Google Workspace로 변경했으며, Workspace 인증은 Login 버튼에서 선택적으로 시작합니다.
**수정**
- 앱을 실행하거나 재시작할 때마다 브라우저 인증을 자동으로 시작하고, 계정 확인에 성공한 뒤에만 앱에 들어갑니다.
- 허용되지 않은 계정이나 인증 거부 뒤에도 앱이 종료되지 않고 로그인 화면에서 다시 요청할 수 있습니다.
- Claude Remote Control이 지정한 프록시와 신뢰 인증서 설정을 따르도록 고쳤습니다.

### v1.9.7-smoke.2 — 2026-09-14

**수정**
- 장기간 실행할 때 불필요하게 쌓이던 메모리를 정리합니다. 저장하지 않은 내용과 진행 중인 작업은 보존됩니다.
- Claude 구독 답변이 스트리밍 중 중복 표시되던 문제를 수정했습니다.
- 도구 없이 Summary/Result만 있는 답변도 공통 카드로 표시됩니다.
- Plan Stage 구분이 Step 본문에 붙어 있어도 올바르게 구분해 표시합니다.
- Windows PowerShell에서 BOM, UTF-8, CP949 파일을 올바르게 읽습니다.
- 앱 재실행·업데이트 후 이전 백엔드의 응답을 새 기동 성공으로 오인하지 않도록 수정했습니다.

### v1.9.7-smoke.1 — 2026-09-14

**수정**
- Claude Gateway 사용 중 일반 채팅은 되지만 Remote Control 연결이 실패하던 문제를 수정했습니다.

### v1.9.7 — 2026-09-12

**추가**
- OpenAI ChatGPT와 Claude 구독 로그인으로 채팅할 수 있고, 기본 도구와 Amicus 도구, 실행 모드별 승인 처리를 지원합니다.
- Gateway를 통한 원격 브라우저 로그인, 세션 공유, 장애 시 인계와 자동 재연결을 지원합니다.
- H-Chat의 GPT·Claude·Gemini 제공자와 Claude 대화별 Remote Control을 사용할 수 있습니다.
- Windows 기본 채팅에서 PowerShell을 실행할 수 있고, Python 전용 환경, 영역별 글자 크기와 공통 단축키가 추가됩니다.
**변경**
- PATH 새로고침을 Settings 하단의 CLI 실행 환경으로 옮기고, 세션 검색의 이모지를 아이콘으로 교체했습니다.
- 글자 크기 설정을 Font Size로 바꾸고, 프롬프트 프리셋 버튼을 제거했으며 Remote Control을 첨부 버튼 옆으로 옮겼습니다.
**수정**
- 구독 상태 갱신 중 앱이 잠시 멈춰 Settings 등 버튼 반응이 늦던 문제를 수정했습니다.
- 에디터의 Close 툴팁, 찾기 창 표시 위치, 아이콘 문제를 수정했습니다.

### v1.9.6-smoke.9 — 2026-09-11

**추가**
- H-Chat 제공자에서 Personal/Project API Key와 환경, GPT/Claude/Gemini 모델을 선택해 사용할 수 있습니다.
- Claude 구독 입력창에 대화별 Remote Control 버튼이 추가되어 원격에서 같은 대화를 이어갈 수 있습니다.

### v1.9.6-smoke.8 — 2026-09-11

**추가**
- Settings에서 탐색기·에디터·프로세스·터미널·채팅별 기본 글자 크기(10-32px)를 정할 수 있습니다.
- Cmd/Ctrl +/- 단축키로 다섯 영역의 글자 크기를 각각 1px씩 조절할 수 있습니다.

### v1.9.6-smoke.7 — 2026-09-11

**추가**
- Windows 기본 채팅에서 PowerShell을 실행할 수 있습니다.
**변경**
- Gateway 세션 공유와 서버 장애 시 인계, 자동 재연결을 지원하며 여러 서버로 나누어 운영할 수 있습니다.
**수정**
- 셸 실행이 취소되거나 종료 코드 없이 실패했을 때 성공으로 오인하던 문제를 수정했습니다.
- Amicus Python 도구가 앱 관리 환경만 사용하도록 했고, 관리 환경을 쓸 수 없으면 실행 전에 실패합니다.
- OS PATH를 앱 시작 시 한 번 수집해 모든 로컬 도구와 터미널에 반영하고 Windows PATH 문제를 수정했습니다.
- Codex·Claude 구독 기본 도구도 Amicus의 Approve·Auto·Bypass 승인 설정을 따르도록 수정했습니다.
- Gateway 로그인 팝업의 오른쪽과 아래가 잘리던 문제를 수정했습니다.

### v1.9.6-smoke.6 — 2026-09-10

**추가**
- OpenAI와 Claude의 Gateway 사용을 지원하며, 기본 브라우저에서 Gateway의 원격 로그인 화면을 열 수 있습니다.
- Gateway 설정을 저장하고 토큰 입력 없이 접속 화면을 열 수 있으며, 로그인과 연결 시험을 구분해 보여줍니다.
**변경**
- Gateway 브라우저의 추가 보안 설정을 제거하고 기본값을 사용하도록 변경했습니다.
**수정**
- Gateway 세션 정리에 한 번 실패하면 이후 로그인이 계속 막히던 문제를 수정했습니다.
- Gateway 원격 브라우저에서 계정 인증 후 로컬 콜백이 차단되던 문제를 수정했습니다.
- Gateway 브라우저 준비 확인 때문에 정상 서버도 시작 실패로 처리되던 문제를 수정했습니다.
- 로컬 Podman 브라우저 실행이 실패하던 문제를 수정했습니다.

### v1.9.6-smoke.5 — 2026-09-10

**추가**
- Claude OAuth의 로그인, 계정 상태, 취소, 연결 해제를 지원하며 공식 Claude Agent SDK로 채팅합니다.
- OpenAI OAuth 로그인으로 ChatGPT 구독 채팅을 사용할 수 있고 모델은 인증된 계정의 목록에서 선택합니다.
- 질문 카드에서 여러 항목을 체크한 뒤 답변으로 제출하고 추가 설명도 함께 보낼 수 있습니다.
- Claude 대화를 공식 SDK 세션으로 이어가며, 다른 제공자에서 전환하면 저장된 대화를 참고 자료로 전달합니다.
**변경**
- AI 제공자 설정에 Claude/OpenAI의 OAuth, API-Key, BOM 탭을 추가하고 Proxy 표시를 Gateway로 바꿨습니다.
- Claude·OpenAI·Gemini·Ollama 설정 카드를 Bedrock과 같은 공통 스타일로 통일했습니다.
**수정**
- 분리된 프로세스에서 부모가 먼저 종료되어도 Stop을 성공으로 판단하던 문제를 수정했습니다.
- OpenAI 인증이 성공해도 설정 화면에서 계정 조회 실패로 표시되던 문제를 수정했습니다.

### v1.9.6-smoke.4 — 2026-09-08

**추가**
- 창으로 돌아올 때 열려 있는 파일의 외부 변경을 반영합니다. 저장하지 않은 탭은 탭바에 경고만 표시합니다.
**변경**
- 도구를 셸 실행, Python 실행, HTTP 요청 세 가지로 줄였고, 파일 읽기·쓰기·데이터 처리는 셸과 Python 안에서 수행합니다.
- Collector Pipeline과 Plan 카드를 제거했고, 큰 도구 출력은 파일로 저장하며 미리보기를 보여줍니다.
**수정**
- CP949·UTF-16 파일을 열고 저장할 때 원래 인코딩을 유지해 글자가 깨지던 문제를 수정했습니다.
- 다른 곳에서 바뀐 파일을 경고 없이 덮어쓰던 문제를 수정했고, 덮어쓰기 여부를 묻습니다.
- 새로고침이나 테마 전환 시 저장하지 않은 편집이 사라지던 문제를 수정했습니다.
- Windows 저장 실패 재시도, 끊긴 심볼릭 링크 저장, 저장 중 이름 변경 시 충돌 오인 문제를 수정했습니다.
- 환경 변수 차단 설정이 셸 실행에 적용되지 않던 문제와 메모리 적립이 영어 문장을 잘못 저장하던 문제를 수정했습니다.

### v1.9.6-smoke.3 — 2026-09-08

**변경**
- 항상 0으로 표시되던 Tool Calls 현황 숫자를 제거했습니다.
- 계획만 세우고 도구를 숨기던 plan-first 단계와 Collector Pipeline Plan 카드를 제거했습니다.
**수정**
- 모델이 사용자에게 질문하는 기능이 실제로 노출되지 않던 문제를 수정했습니다.
- 대화 복원 시 도구 카드가 사라지던 문제를 수정했습니다.
- Python 실행을 취소할 수 있도록 수정했고, 작업 마감이 도구 실행 중에도 적용되도록 했습니다.

### v1.9.6-smoke.2 — 2026-09-07

**추가**
- 탐색기에서 연 파일을 탭·편집·저장이 되는 중앙 에디터에서 열 수 있고, 가운데 영역을 터미널과 에디터 두 모드로 전환합니다.
- 탐색기가 워크스페이스 루트 기준으로 동작하며, git 상태 색과 배지, 미저장 표시, 숨김 파일·새로고침 버튼을 제공합니다.
- 탐색기 우클릭으로 새 파일·폴더를 만들고 경로를 복사할 수 있으며, 사이드 패널 폭을 끌어서 조절할 수 있습니다.
- 저장하지 않은 편집이 있으면 앱 종료 전에 확인하고, JSON 문법 강조를 지원합니다.
**수정**
- 에디터가 CP949·UTF-16 파일을 원래 인코딩으로 저장하고, 다른 곳에서 바뀐 파일을 덮어쓰지 않도록 수정했습니다.
- 파일 이름 변경·삭제를 탭이 따라가며, 이름 변경이 기존 파일을 덮어쓰지 않도록 했습니다.
- 사내 TLS 검사 장비 뒤에서도 연결이 깨지지 않도록 OS 신뢰 저장소를 사용합니다.
- 앱 종료 시 백엔드가 확실히 종료되도록 수정했습니다.

### v1.9.6-smoke.1 — 2026-09-02

**추가**
- 와처와 워크플로우를 YAML로 내보내고 가져올 수 있으며, 내보낼 때 비밀값과 로컬 경로는 참조로 치환됩니다.
**변경**
- 동작하지 않던 명령 승인 연결 경로와 사용되지 않던 중복 구성 요소를 제거했습니다.
**수정**
- GitLab/GitHub 토큰이 빈 값으로 저장되던 문제를 수정했습니다.
- 사용할 수 없는 자격증명이 연결됨으로 표시되던 문제를 수정했습니다.
- 인증 실패 시 원인 없이 500 오류만 보이던 문제를 수정해 정확한 원인을 안내합니다.
- 보안 문제를 수정했습니다. 오류 메시지에서 GitLab 인증 정보가 가려지지 않던 부분입니다.

### v1.9.6 — 2026-09-01

**변경**
- Claude 웹 세션(구독) 경로를 제거했고, Claude는 API로만 등록합니다. 무료 대안으로 Ollama를 사용할 수 있습니다.
- 사용자 문장의 키워드로 요청 성격과 셸 타임아웃을 추측하던 동작을 제거하고 넉넉한 고정 타임아웃을 사용합니다.
- 키워드로 대량 작업을 판단해 프롬프트를 바꾸던 동작을 제거해 프롬프트를 줄였습니다.
**수정**
- 로컬 경로를 지정한 요청에서 파일을 읽지 못하던 문제를 수정했습니다.
- 단어 때문에 정상 명령이 짧은 타임아웃으로 중단되던 문제를 수정했습니다.

### v1.9.5-smoke.1 — 2026-09-01

**변경**
- 사용자 문장에서 조사 방식과 타임아웃을 추측하던 동작과 대량 작업 키워드 판단을 제거하고 프롬프트를 줄였습니다.

### v1.9.5 — 2026-09-01

**변경**
- 키워드만으로 통합 연동을 요구하며 요청을 차단하던 동작을 제거했습니다. 미연결 상태는 도구 호출 시점에 안내됩니다.
- 특정 단어로 파일 읽기 도구가 제외되던 동작을 제거해 로컬 경로 요청에서도 파일을 읽을 수 있습니다.
- 프롬프트 형식 규칙을 줄여 길이를 줄였습니다.
**수정**
- 채팅 본문이 중복되거나 소실되던 문제와 Step 라벨이 줄 중간에 붙던 문제를 수정했습니다.
- 응답 생성 중 Stop이나 세션 삭제가 데이터베이스 잠금으로 실패하던 문제를 수정했습니다.
- 도구 카드의 인자가 비어 있던 문제와 같은 Step 라벨 배지가 중복 표시되던 문제를 수정했습니다.
- 이전 저장소 마이그레이션이 기존 파일을 덮어쓰던 문제와 macOS 앱이 기동 직후 종료되던 문제를 수정했습니다.

### v1.9.5 — 2026-08-31

**변경**
- 키워드만으로 통합 연동을 요구하며 요청을 차단하던 동작을 제거했습니다. 미연결 상태는 도구 호출 시점에 안내됩니다.
- 특정 단어로 파일 읽기 도구가 제외되던 동작을 제거해 로컬 경로 요청에서도 파일을 읽을 수 있습니다.
- 프롬프트 형식 규칙을 줄여 길이를 줄였습니다.
**수정**
- 채팅 본문이 중복되거나 소실되던 문제와 Step 라벨이 줄 중간에 붙던 문제를 수정했습니다.
- 응답 생성 중 Stop이나 세션 삭제가 데이터베이스 잠금으로 실패하던 문제를 수정했습니다.
- 도구 카드의 인자가 비어 있던 문제와 같은 Step 라벨 배지가 중복 표시되던 문제를 수정했습니다.
- 이전 저장소 마이그레이션이 기존 파일을 덮어쓰던 문제와 macOS 앱이 기동 직후 종료되던 문제를 수정했습니다.

### v1.9.4-smoke.16 — 2026-08-26

**수정**
- 계획만 표시하고 실행이 중간에 끊기던 문제를 수정했습니다.

### v1.9.4-smoke.15 — 2026-08-26

**추가**
- 응답 시작 시 계획(Plan Stage와 Action Stage)을 먼저 표시해 실행 중 말풍선이 비지 않도록 했습니다.
**변경**
- 터미널 탭 첫 표시 지연을 줄이기 위해 셸을 미리 준비합니다.
**수정**
- 터미널 재시작 후 크기를 바꾸기 전까지 터미널이 시작되지 않던 문제를 수정했습니다.

### v1.9.4-smoke.14 — 2026-08-26

**변경**
- 상시 실행 중인 와처의 폴링 비용을 줄였습니다.
- 사용되지 않는 내부 실행 코드를 제거했습니다.

### v1.9.4-smoke.13 — 2026-08-26

**변경**
- 앱 런타임을 최신 버전으로 업그레이드했습니다.
- 데이터베이스 엔진을 교체해 네이티브 모듈 재빌드가 필요 없도록 했습니다. 기존 데이터는 그대로 사용됩니다.

### v1.9.4-smoke.12 — 2026-08-26

**변경**
- Windows에서 중단 버튼이나 파이썬 도구 실행, 명령 탐색 중 앱이 멈추거나 응답 없음으로 보이던 현상을 줄였습니다.
**수정**
- 라이트 모드에서 채팅 말풍선 글자색이 겹쳐 보이던 문제를 수정했습니다.
- 세션을 전환해도 스크롤이 이전 위치에 고정되던 문제를 수정했습니다.
- 세션에 다시 들어오면 마지막으로 읽은 위치에 "여기까지 읽음" 구분선이 표시됩니다.
- 클립보드의 이미지를 채팅에 붙여넣어 첨부할 수 있습니다.
- 세션 목록에 마우스를 올리면 제목 옆에 편집용 연필 아이콘이 표시됩니다.
- Stop을 눌러도 작업이 계속되거나 다음 메시지에서 취소된 작업이 되살아나던 문제를 수정했습니다.

### v1.9.4-smoke.11 — 2026-08-21

**추가**
- Bedrock 모델 목록에 GPT-5.6 계열 모델 3종을 추가했습니다.
- 모델 목록을 조회할 수 없을 때 보여주는 기본 모델 목록을 최신 구성으로 갱신했습니다.
**변경**
- Bedrock에서 모델 제공사에 따라 프롬프트 캐시 방식을 자동으로 구분해 요청 거부를 방지합니다.
- Bedrock GPT-5.6 모델에서도 특정 도구 강제 선택이 동작합니다.

### v1.9.4-smoke.10 — 2026-08-20

**변경**
- Stop 이후 불필요하게 상태를 계속 확인하던 동작을 멈춥니다.
**수정**
- Stop을 눌러도 채팅이 정체됨 또는 실행 중 상태로 남던 문제를 수정했습니다.

### v1.9.4-smoke.9 — 2026-08-19

**변경**
- 내부 정리와 안정성 개선 (사용자에게 보이는 변경 없음)

### v1.9.4-smoke.8 — 2026-08-19

**수정**
- 채팅 응답 안의 표와 코드블록이 원문 그대로 노출되던 문제를 수정했습니다.
- 표 형식 판정을 넓혀 다양한 형태의 표가 정상 렌더되고, 닫히지 않은 코드블록이 뒤따르는 단계 카드를 가리지 않으며, 연속된 표 두 개가 하나로 합쳐지지 않습니다.

### v1.9.4-smoke.7 — 2026-08-13

**변경**
- 채팅 제목을 첫 질문과 답변이 끝난 뒤 요약해서 정합니다.
**수정**
- 세션 제목 생성 기록이 계속 쌓이지 않도록 정리했습니다.

### v1.9

**Theme:** Reliability hardening of the AI agent loop, a rebuilt "smart" Watcher, MCP support, a real login/data-integrity gate, and the move to a shared-store architecture — the longest-running and largest line in the project (June 8 – August 13, ~789 commits).

`v1.9.0 … v1.9.4-smoke.6`

- **Agent-loop "never-STOP" reliability rework**: root-caused and fixed a class of silent run terminations — `flow_plan` treated as a fake terminal answer, Bedrock dropping a stream event on soft-idle (corrupted tool-call JSON), collector stragglers misclassified as retryable timeouts causing 50-minute stalls, malformed tool-calls, and repeated-failure guards silently swallowing partial results. Later replaced the whole pre-loop intent/sizing/strategy LLM round-trip with a fixed safety cap, and removed `flow_plan` from the model-facing tool surface entirely in favor of runtime-owned fan-out.
- **Watcher rebuilt into a shape-aware, provider-neutral monitor**: URL/JSON probe that infers structure automatically (arrays, identity fields, nested paths), an interactive shape-tree picker UI, and/or condition groups, per-item dedup via stable identity paths (including nested arrays, e.g. per-Jira-comment alerts), and template-free `{watcher_text}` auto-formatting of any payload.
- **MCP (Model Context Protocol) client support** added end-to-end: stdio + HTTP transports with bearer auth, per-server tool aggregation, config UI, and a `{server}` marker to force a specific MCP tool — after an earlier, fully custom "Known Work" vector-knowledge-base feature (Postgres/pgvector, Trino, Qdrant, embedded SQLite backends, built over ~3 days) was scrapped and removed in favor of it.
- **Workflow engine rewritten** around a step-handler registry (shell/notify/slack/email/condition/wait/parallel/`ai_prompt`/`if`/`http_request`), full per-step input/output/error capture in run history, drag-to-reorder steps with forward-reference warnings, and workflow-owned cron schedules.
- **Login/data-integrity gate landed**: production Cognito login gate (group-based access, silent refresh, fail-closed) shipped after earlier "Signal" login-gate scaffolding, alongside a store read/write split (Electron reads a shared SQLite store, backend is sole writer; `.amicus-v2` → `.amicus` folder consolidation) fixing run-history that silently vanished across restarts, plus an async store-prepare rewrite to kill a Windows "Not Responding" boot hang caused by main-thread blocking spawns.
- **Sidecar/backend platform work**: `apps/desktop` folded into `src/`, sidecar lifecycle hardened against orphaned/zombie processes with bounded respawn, chat-run store moved to SQLite with TTL pruning and a concurrency semaphore, and the backend Python bootstrap made fully async with a splash-screen progress UI and a diagnostics/venv-repair panel.
- **Terminal & approval UX overhaul**: per-tool approval gate rebuild ("approve all this turn"), a redesigned terminal (separate xterm for tool output vs. interactive shell, ConPTY/Windows scroll fixes), window chrome simplified (start maximized, app menu removed), and an `ask_user` virtual tool that can pause a run for confirmation or masked secret input (e.g. sudo password) without leaking it into the transcript.
- **Provider/integration breadth**: Slack Watcher rewritten on Socket Mode (backend-driven, content-aware dedup, autonomous root-cause-analysis notifications), a backend Notifications domain with per-alert analysis threads, live AI model listing + provider budget/prompt-cache policy across Anthropic/OpenAI/Bedrock/Gemini/Codex/Ollama, and outbound HTTP routed through Electron's network stack so it respects the corporate VDI proxy.
- **Chat session auto-titling**: provider-neutral one-shot summary generates a real session title instead of the first message, updating the sidebar live.
- Numerous smaller fixes: CSV/report path cleanups, GitLab/GitHub token-drop-on-save fix, Bedrock `ListInferenceProfiles` pagination, GFM task-list checkbox rendering, and a release-CI fix so `-smoke.` prerelease tags stop publishing as `latest`.

### v1.8

**Theme:** Execution-contract completion tracking, `http_request` maturity, and a large dead-code purge of provider-specific integration methods in favor of the generic HTTP tool.

`v1.8.0 … v1.8.2-mock.1`

- Added an **execution-contract model** so the agent loop keeps running until there's real evidence of completion, instead of stopping early on a plan-only turn (superseding an earlier "API fanout reconciliation" experiment that was implemented, found to override multi-part plans with a single API result, and promptly removed).
- Enforced **multi-job completion** for bundled/compound requests so a multi-part ask isn't silently collapsed to one job.
- Matured `http_request` into a first-class collection tool: provider-neutral query serialization, idempotent retry with backoff/`Retry-After`, and NDJSON spooling of large paginated results to disk.
- **Large cleanup**: removed dead-code integration methods across Jira/Confluence/GitHub/GitLab/Slack/Gmail now superseded by `http_request`, deleted the standalone `facts_aggregate` tool (data_inspect is the sole data SSOT), and dropped unused dependencies (handlebars, etc.).
- Added **live AI model listing** (Anthropic/OpenAI/Bedrock) with hardcoded fallback, and bundled Google OAuth Desktop credentials so "Login with Google" works out of the box.
- Perf pass: async/parallel system-info probes with a persistent cache and startup prewarm, cutting first-message latency.

### v1.7

**Theme:** Chat history becomes durable and backend-owned, and the collector/execution stack gets a major provider-neutral architecture pass (VDI hardening line).

`v1.7.0 … v1.7.2-vdi-smoke.48`

- Built a proper **chat-history persistence layer** (SQLite tables + indexes, resumable runs, cursor-based capture) and rewired the sidebar/session list to read from it instead of legacy in-memory state.
- **`python_execute` became the canonical execution/report path**: classifier + args/cwd/timeout-aware executor with streaming and audit telemetry, culminating in auto-registering `.html` stdout as a report artifact — this is also where the older `report_generate` / `report_pipeline` / `direct_html_report` template machinery was superseded.
- **Bulk execution model rewrite** ("flow_plan" naming, PR-α/β series): moved environment/PATH/shell-family resolution out of TypeScript entirely and into the Python side (`amicus_run.py`) for parity between local and collector execution.
- **`data_inspect` established as the single source of truth** for structured file/data inspection (overview-by-default, YAML/TOML/XML structural counts, provider-neutral prompt gating), retiring parallel ad hoc paths.
- Collector hardening for VDI environments: kept parallel runs alive/resumable across flaky connections, derived batch parallelism from live probe timing instead of static guesses.

### v1.6

**Theme:** The single largest line (626 commits, April 14 – May 20) — a provider-neutral rebuild of the collection/adapter stack, a huge expansion of integration tools, the birth of the Python backend sidecar, and the start of chat ownership moving server-side.

`v1.6.0 … v1.6.128`

- **Windows compatibility hardening**: fixed native `.exe` hangs under Git Bash (routed through `cmd.exe`/PTY), AWS SSO token cache sync, process-tree kill via `taskkill /T`, and a large body of shell/PATH/CLI edge cases.
- **Provider-neutral adapter architecture**: introduced a `ProviderAdapter` protocol with a Python bridge, adapter versioning/audit trail, and a "shared-layer bias guard" CI check to keep vendor-specific logic out of shared code — plus production adapters for Kubernetes (in-cluster EKS bootstrap) and AWS (boto3).
- **Integration surface roughly tripled**: ~40 new tools added across Jira (11), Confluence (7), GitHub (9), GitLab (5), Slack (6), and Notion (3), with pagination support and read-only same-turn parallel dispatch.
- **Report generation matured**: HTML reports gained XLSX (multi-sheet) export, auto-inlined CSS for email compatibility, Handlebars-style templating, and a `batch_plan` tool that publishes upfront K/P/T (target/parallelism/timeout) sizing to the user.
- **The Python backend was born** (tagged mid-line as `v1.0.0-renew`, "Architect V2 runtime gateway skeleton") — a FastAPI-style `apps/backend` service with its own contracts, adapters, and API surface, separate from the Electron main process.
- **Chat ownership began moving to the backend**: the agent loop, streaming, progress reporting, and report generation were progressively re-owned by the Python sidecar rather than the Electron/TS layer ("backend agent loop SoT"), including a sidecar auto-bootstrap with its own managed Python 3.14 venv.
- Closed out with structured-progress UI rework (per-child result rows, adaptive `maxLoopUse`), a chat `/state` payload-bloat fix series, and the first version of `python_execute` as an install-hook–integrated runner.

### v1.5

**Theme:** Terminal/session-state reliability plus the first "embedded services" performance/infrastructure pass.

`v1.5.0 … v1.5.9`

- Fixed a cluster of terminal/session bugs: chat history surviving session re-clicks, terminal history surviving tab switches (singleton xterm + `React.memo`), a Windows `shell_execute` hang (exit-event + pipe-destroy fix), and AWS SSO token hangs.
- Added an `excel_create` tool (multi-sheet, styled headers via ExcelJS) and a custom-prompts tab.
- Enforced parallel shell execution for bulk operations and banned "announcement-only" AI responses that don't follow through with action.
- **Embedded services infrastructure** rolled out in phases: indexes/cache/circuit-breaker/persistent queue (Phase 1), croner/pino/bottleneck/p-queue (Phase 2), vectra/MCP-health/Handlebars (Phase 3) — plus migrating ~118 `console.log` calls to a structured logger.
- Closed the line by resolving all outstanding test failures (173/173 passing).

### v1.4

**Theme:** A short, single-feature bridge release.

`v1.4.0`

- Added an `excel_create` tool via ExcelJS.
- Added a custom-prompts tab (renamed the env-vars tab to Korean "보안").

### v1.3

**Theme:** Windows shell-execution edge cases and CLI non-interactivity.

`v1.3.0 … v1.3.4`

- Fixed native `.exe` execution on Windows Git Bash (winpty wrapper, then reverted `cmd.exe` routing after discovering `spawn` uses a pipe, not a PTY, avoiding a console deadlock).
- Forced non-interactive environment variables universally across CLI tools (not just AWS) to stop pager/prompt hangs.
- Banned useless `echo`/`sleep` commands and required the AI to run login commands itself rather than asking the user to.
- Always surface executed commands in the terminal for transparency.

### v1.2

**Theme:** Windows environment-variable and shell-execution correctness.

`v1.2.0 … v1.2.9`

- Read the full Windows system PATH from the registry for child processes, and switched to inheriting the full `process.env` instead of an allowlist filter.
- Used login shells (`--login`) and loaded the user's PowerShell profile with `ExecutionPolicy Bypass` for consistent tool availability.
- Routed Windows native `.exe` execution through `cmd.exe` to avoid Git Bash PTY hangs.
- Fixed CSV export Excel/UTF-8 compatibility and prevented Microsoft Store Python stub hangs with a timeout.

### v1.1

**Theme:** Shell-detection and execution-policy consistency between the terminal and AI tool calls.

`v1.1.0 … v1.1.9`

- Unified shell detection so `shell_execute` matches the interactive PTY (Git Bash preferred on Windows, PowerShell as an explicit fallback only).
- Fixed abort handling dropping the `tool_result`, and improved chat output readability.
- Added a user-configurable execution policy with a blocked-reason display, and polished the "AI running" banner (shimmer/bouncing-dots).

### v1.0

**Theme:** The 1.0 milestone — accessibility, i18n, resilience patterns, and safer environment-variable handling.

`v1.0.0 … v1.0.9`

- Added Circuit Breaker resilience for external API calls, i18n (ko/en) via i18next, message search (Cmd+F), and Google Sheets integration.
- Improved accessibility (ARIA labels, keyboard nav, contrast) and added HTML/CSV chat export.
- Switched environment-variable handling from an allowlist to a user-configurable **blocklist**, passing the full user environment through to child processes by default (fixing a long tail of "missing PATH/env" issues) while letting users still redact secrets.
- Refactored IPC handlers into focused modules and extracted shared workflow/registry helper functions as the codebase grew.
- Applied "approve" execution mode consistently to all tools, and made abort actually stop the tool loop.

### v0.9

**Theme:** A dedicated security-hardening release plus template/UI polish.

`v0.9.0 … v0.9.8`

- **Security release (v0.8.0 relabeled here)**: fixed 6 critical vulnerabilities and memory leaks, closed an email-header-injection hole and a markdown XSS vector, and added IPC type-safe argument validation.
- Implemented 24 medium-priority backend/frontend improvements identified in the security review.
- Fixed template duplication/dedup bugs on app restart (scoped dedup to default template names only).
- Raised `maxTokens` from 8192 → 16384 and fixed chat-history pairing of `tool_use`/`tool_result` blocks around approve-mode timing.
- UI polish: app-wide animations, environment-variables tab, Windows loading-dots animation and text wrapping.

### v0.8

**Theme:** Completing the HTML report-template catalog.

`v0.7.3 … v0.8.4`

- Completed the full report template catalog (13 templates, each with HTML + Markdown + prompt + data-source metadata).
- Shipped "security+perf" fixes across policy enforcement, environment variables, CI, and compression.
- Rebalanced the default window/panel layout (1200×800 → 1400×900; chat panel 35% → 50%) for a 1:1 center:chat ratio.

### v0.7

**Theme:** Template system consolidation and a first pass at deep multi-step investigation.

`v0.6.2 … v0.7.3`

- Unified template naming and added message-variant support; auto-migrated deprecated Korean template names on startup.
- Added 4 new HTML preview templates (incident-k8s, daily-status, security-alert, slack-digest).
- Introduced a "deep analysis chain" — multi-layer investigation prompting usable across all contexts.

### v0.6

**Theme:** Rapid report-template expansion.

`v0.5.0 … v0.6.2`

- Added a monthly ops report template (with a v2 animated/enhanced revision) and 5 more templates (incident, deploy, cost, security, SLA).
- Added CSV download to all report templates and a copy-paste-ready "prompt guide" for generating reports.
- Added an in-app template usage-guide tab.

### v0.5

**Theme:** File management and workflow flexibility.

`v0.4.2 … v0.5.0`

- Added a file-explorer with full CRUD (create/rename/delete files and folders).
- Added per-service "preferred accounts" for workflows and full Notion integration (DB query/list/create/delete/update row).
- Added parallel sub-step execution within workflows.

### v0.4

**Theme:** A brief cleanup/polish stop between v0.3 and v0.5.

`v0.4.0 … v0.4.2`

- Added dynamic `maxTokens` sizing and an "Open Folder" button after `file_write`.
- Made chat file paths clickable (opens in Finder/Explorer).
- Resolved all TypeScript lint errors and removed the Slack Bot Token path in favor of the linked user token.

### v0.3

**Theme:** Ticketing/DevOps integrations (Jira, Confluence, GitHub, GitLab) and report templating groundwork.

`v0.2.9 … v0.3.9`

- Added GitHub and GitLab integrations (both cloud and on-premise), and Jira/Confluence Cloud vs. Server/Data-Center API compatibility with PAT (Bearer) auth.
- Introduced report presets and HTML templates (e.g. a Korean-language "Daily Jira Status" template) plus a template catalog/gallery with AI auto-variable extraction from uploaded templates.
- Hardened `file_write` (path aliasing, `~` expansion, rejecting empty-content writes) and fixed `tool_call_delta` argument assembly for streamed tool calls.
- Raised `maxTokens` from 4096 → 16384 with truncation detection on Bedrock/Claude.

### v0.2

**Theme:** The automation model (Watcher/Cron/Workflow) got its first real redesign, plus cross-platform (Windows) terminal work.

`v0.1.0 … v0.2.9`

- Redesigned automation around a `WorkflowQueue` (concurrency limits, overflow control): Cron now triggers workflows instead of running the AI directly, and Watcher notifies workflows via `workflowIds` instead of ad hoc actions, with legacy configs auto-migrated.
- Added Windows terminal support: auto-detected Git Bash/Cygwin/WSL, synced terminal cwd with the file explorer, and fixed AWS credential parsing and path conversion (`/cygdrive/c/` → `C:\`) along the way.
- Added connected-account management (click to disconnect) and separated Jira/Confluence as independent connections.
- Set up CI to auto-upload releases to a separate `amicus-releases` repo, and hardened login-token persistence across app restarts.

### v0.1

**Theme:** The original scaffold — from an empty Electron shell to a working AI desktop agent with terminal, browser automation, MCP tools, and a first automation layer, in about a week.

`v0.1.0` (first commit 2026-03-24 → first tag 2026-03-31)

- Bootstrapped the Electron app: IPC registry, System/Executor/AI services, an approval-gated execution policy engine, and Claude/ChatGPT provider support (subscription web login + API key dual auth).
- Built the core UI: Tokyo-Night-themed layout with a Chat Panel, an xterm.js Terminal Panel, and a complete tool-calling loop (`shell_execute`, `file_read`, `file_write`).
- Added desktop agent tools — AppleScript, screenshot, clipboard, notifications — plus Playwright browser automation and an MCP client (desktop-commander, filesystem, Playwright servers).
- Delivered an interactive PTY terminal (real zsh/bash via node-pty) with AI commands routed through the same PTY for identical output, after multiple iterations to fix garbled/marker-polluted output.
- Introduced Memory (SQLite + FTS search), session persistence, and the first automation primitives: Cron scheduler, Watcher (event monitor), and Workflow (pipeline), plus a webhook receiver for Slack/Grafana/PagerDuty.
- Added Bedrock as a third AI provider, SMTP email, system tray, and a GitHub Actions CI/build pipeline (macOS + Windows).
