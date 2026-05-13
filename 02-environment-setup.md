# 환경 설치 (Windows).

> CHAPTER 02 / 27 · PART 1 · 시작하기 · 예상 시간 50분

---

## 두 가지 설치 방법

클로드코드를 설치하는 방법은 2가지입니다. **방법 A를 추천합니다.**

| | 방법 A: VSCode 확장 (추천) | 방법 B: CLI 직접 설치 |
|---|---|---|
| **난이도** | 쉬움 | 보통 |
| **설치할 것** | Git for Windows + VSCode + 확장 | Node.js + VSCode + npm 명령어 + Git |
| **Node.js** | 나중에 필요할 때 설치 | 처음부터 설치 |
| **사용 방식** | VSCode 안에서 마우스로 실행 | 터미널에서 claude 명령어로 실행 |

이 교재는 **방법 A(VSCode 확장)** 을 기준으로 설명합니다.  
방법 B는 페이지 하단에 별도로 안내합니다.

---

## 방법 A: VSCode 확장으로 설치 (추천)

### 설치할 것들

| 순서 | 프로그램 | 용도 | 시간 |
|---|---|---|---|
| 1 | Git for Windows | 클로드코드가 내부적으로 사용하는 셸 환경 | 3분 |
| 2 | VS Code | 코드 편집기 + 클로드코드 실행 환경 | 3분 |
| 3 | Claude Code 확장 | VSCode 안에서 클로드코드를 바로 실행 | 2분 |

### 1. Git for Windows 설치

Git for Windows는 코드 버전관리 도구이자, 클로드코드가 Windows에서 동작하기 위해 반드시 필요한 프로그램입니다.

회사에서 GitHub를 차단하고 있어도 괜찮습니다.  
Git for Windows는 내 컴퓨터에서만 동작하는 로컬 프로그램입니다.  
코드를 외부 서버에 올리는 GitHub(클라우드 서비스)과는 완전히 다릅니다.

#### 설치 방법

1. 브라우저에서 https://git-scm.com 을 엽니다
2. Download for Windows 클릭
3. 설치 파일 실행
4. 모든 화면에서 Next → Install → Finish
   - 옵션이 많이 나오는데, 기본값 그대로 두고 Next만 누름

#### 설치 확인

PowerShell 또는 CMD를 열고 아래를 입력합니다:

```
git --version
```

`git version 2.x.x` 같은 결과가 나오면 성공입니다.  
안 되면 PowerShell을 닫았다가 다시 열어보세요.  
그래도 안 되면 PC를 재시작하세요.

#### Git 초기 설정

Git을 사용하려면 이름과 이메일을 한 번 설정해야 합니다:

```
git config --global user.name "홍길동"
git config --global user.email "hong@example.com"
```

이름과 이메일은 나중에 코드 변경 기록에 남습니다. 실제 이메일이 아니어도 괜찮습니다.

---

### 2. VS Code 설치

VS Code(Visual Studio Code)는 마이크로소프트가 만든 무료 코드 편집기입니다.  
코드를 볼 수도 있고, 하단에 터미널이 내장되어 있고, 여기에 클로드코드를 설치합니다.

#### 설치 방법

1. 브라우저에서 아래 주소를 엽니다
   ```
   https://code.visualstudio.com
   ```
2. Download for Windows 파란 버튼 클릭
3. 다운로드된 설치 파일 실행
4. 설치 중 "추가 작업 선택" 화면이 나오면 아래를 모두 체크합니다:
   - "Open with Code" action을 Windows 탐색기 파일 상황에 맞는 메뉴에 추가
   - "Open with Code" action을 Windows 탐색기 디렉터리 상황에 맞는 메뉴에 추가
   - **PATH에 추가** (터미널에서 `code` 명령어로 VS Code를 열 수 있게 됩니다)

#### VS Code 화면 구성

| 영역 | 위치 | 설명 |
|---|---|---|
| 메뉴 | 최상단 | File, Edit, View, Terminal ... |
| 사이드바 | 왼쪽 | 파일 목록, 확장, 설정 등 |
| 편집 영역 | 중앙 | 코드가 여기에 표시됩니다 |
| 터미널 패널 | 하단 | 여기서 클로드코드를 실행합니다 |

#### 터미널 열기

터미널을 여는 방법 3가지:
1. 상단 메뉴: Terminal → New Terminal
2. 단축키: `Ctrl + \`` (백틱 키, 숫자 1 왼쪽)
3. 단축키: `Ctrl + Shift + '` (작은따옴표)

하단에 터미널 패널이 나타나면 성공입니다.

---

### 3. Claude Code 확장 설치

VSCode 확장을 설치하면 별도의 CLI 설치 없이 바로 클로드코드를 사용할 수 있습니다.  
확장이 클로드코드 CLI를 내장하고 있어서 npm 명령어를 입력할 필요가 없습니다.

#### 설치 방법

1. VS Code를 엽니다
2. 왼쪽 사이드바에서 확장(Extensions) 아이콘 클릭 (또는 `Ctrl + Shift + X`)
3. 검색창에 **Claude Code** 입력
4. Anthropic이 만든 "Claude Code" 확장을 찾아서 Install 클릭
5. 설치 완료 후, 왼쪽 사이드바에 ✻ (스파크) 아이콘이 나타납니다

> 스파크 아이콘이 안 보이면 VS Code를 한번 재시작해 보세요.

#### Claude 계정 연결 (로그인)

1. 왼쪽 사이드바에서 ✻ 아이콘 클릭
2. 처음 실행하면 로그인 화면이 나타납니다
3. **Anthropic Console** 선택
4. 브라우저가 자동으로 열리면서 Claude 로그인 페이지가 뜹니다
5. Claude 계정으로 로그인합니다
6. "Claude Code에 접근을 허용하시겠습니까?" → 허용 클릭
7. VS Code로 돌아오면 클로드코드 채팅 패널이 나타납니다

#### 첫 대화 테스트

채팅 패널에 아래를 입력합니다:

```
안녕? 넌 뭘 할 수 있어?
```

클코가 자기소개를 하면 연결 성공입니다!

#### 안 되면?

| 증상 | 해결 방법 |
|---|---|
| 확장이 검색 안 됨 | VS Code 버전을 확인하세요. 1.98.0 이상 필요합니다 (Help → About) |
| 스파크 아이콘이 안 보임 | VS Code를 재시작하세요 |
| 브라우저가 안 열림 | 화면에 나온 URL을 직접 복사해서 브라우저에 붙여넣으세요 |
| 로그인했는데 반응 없음 | 잠시 기다려보세요 (10초 정도). 안 되면 확장을 삭제 후 다시 설치 |
| Git Bash를 찾을 수 없다는 에러 | Git for Windows가 설치되었는지 확인하세요 (1번으로 돌아가기) |
| Pro 플랜인데 사용 불가 | claude.ai에서 구독 상태를 확인하세요 |

---

## 작업 폴더 만들기

앞으로 모든 실습 프로젝트를 담을 폴더를 만듭니다.

VS Code 터미널에서:

```
mkdir C:\claude-projects
cd C:\claude-projects
```

이 폴더 안에서 프로젝트별로 하위 폴더를 만들어 작업합니다.  
예: `C:\claude-projects\budget-app\`, `C:\claude-projects\goguma-market\`

---

## Node.js 설치 (챕터 05부터 필요)

지금 당장은 필요 없지만, 챕터 05(나만의 놀이터)부터 웹사이트를 직접 만들 때 필요합니다.  
미리 설치해두는 것을 권장합니다.

### 설치 방법

1. 브라우저에서 아래 주소를 엽니다
   ```
   https://nodejs.org
   ```
2. 화면에 버튼이 2개 보입니다. 왼쪽 **LTS 버전(초록색)** 을 클릭합니다.
   - LTS = 안정적인 버전이라는 뜻
   - 오른쪽 Current 버전은 쓰지 마세요
3. 다운로드된 `.msi` 파일을 실행합니다
4. 설치 화면에서 모두 Next → Next → Install → Finish 클릭합니다.
   - "Automatically install the necessary tools" 체크박스가 나오면 체크해주세요

### 설치 확인

VS Code 터미널에서:

```
node --version
```

`v22.x.x` 같은 버전 번호가 나오면 성공입니다.

```
npm --version
```

`10.x.x` 같은 숫자가 나오면 됩니다. npm은 Node.js를 설치하면 자동으로 같이 설치됩니다.

### 안 되면?

| 증상 | 해결 방법 |
|---|---|
| node를 찾을 수 없다는 에러 | 터미널을 닫았다가 다시 열어보세요 |
| 그래도 안 됨 | PC를 재시작하세요 |
| 재시작해도 안 됨 | Node.js를 삭제 후 다시 설치하세요. 설치 시 "Add to PATH" 옵션 확인 |

---

## 최종 체크리스트

아래 명령어를 하나씩 실행해서 모두 버전 번호가 나오면 환경 설치 완료입니다:

```
git --version
node --version
npm --version
```

| 프로그램 | 명령어 | 예상 결과 | 필수 여부 |
|---|---|---|---|
| Git | `git --version` | git version 2.x.x | 필수 |
| Node.js | `node --version` | v22.x.x | 챕터 05부터 필요 |
| npm | `npm --version` | 10.x.x | 챕터 05부터 필요 |

Claude Code는 VSCode 확장으로 설치했으므로 별도 확인이 필요 없습니다.  
모두 통과했으면 다음 챕터로 넘어갑시다!

---

## 부록: 방법 B — CLI로 직접 설치하기

VSCode 확장 대신 터미널에서 직접 `claude` 명령어를 실행하고 싶다면 이 방법을 사용하세요.

### 추가로 필요한 것

Node.js가 설치되어 있어야 합니다 (위의 Node.js 설치 참고).

### 설치 명령어

VS Code 터미널에서 아래 명령어를 입력합니다:

```
npm install -g @anthropic-ai/claude-code
```

- `npm` = Node.js 패키지 관리자
- `install -g` = 전역(global)으로 설치하라는 뜻
- 설치에 1~2분 정도 걸립니다

### 설치 확인

```
claude --version
```

`1.x.x` 같은 버전 번호가 나오면 성공입니다.

### 실행 방법

프로젝트 폴더에서:

```
cd C:\claude-projects\my-project
claude
```

터미널에 `>` 프롬프트가 나타나면 성공입니다.

### 안 되면?

| 증상 | 해결 방법 |
|---|---|
| npm: command not found | Node.js 설치가 안 된 것. Node.js 설치로 돌아가세요 |
| 설치 중 EACCES 권한 에러 | PowerShell을 관리자 권한으로 실행하세요 (PowerShell 우클릭 → "관리자 권한으로 실행") |
| 브라우저가 안 열림 | 터미널에 나온 URL을 직접 복사해서 브라우저에 붙여넣으세요 |
| 로그인했는데 터미널에 반응 없음 | 잠시 기다려보세요 (10초 정도). 안 되면 Ctrl+C로 취소하고 claude를 다시 실행 |
