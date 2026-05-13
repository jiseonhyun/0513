# MCP와 Supabase — AI에 데이터베이스를 연결하다.

> CHAPTER 08 / 27 · PART 2 · 가계부 만들기 · 예상 시간 40분

## 문제 상황

지금까지 만든 가계부는 새로고침하면 데이터가 사라집니다.

이건 데이터가 **브라우저 메모리**에만 있기 때문입니다.

```
입력 → 화면에 보임 → 새로고침 → 전부 사라짐 😢
```

데이터를 영구적으로 저장하려면 데이터베이스가 필요합니다.

## 데이터베이스란?

엑셀과 비교하면 이해하기 쉽습니다:

| 엑셀 | 데이터베이스 |
|------|-------------|
| 파일 (.xlsx) | 데이터베이스 |
| 시트 (Sheet1) | 테이블 (Table) |
| 행 (Row) | 레코드 (한 건의 데이터) |
| 열 (Column) | 컬럼 (항목) |

가계부로 예를 들면:

테이블: budget

| 날짜 | 타입 | 카테고리 | 금액 | 메모 |
|------|------|----------|------|------|
| 2026-03-01 | 수입 | 급여 | 300만 | 3월 |
| 2026-03-05 | 지출 | 식비 | 1.5만 | 점심 |
| 2026-03-07 | 지출 | 교통 | 3천 | 버스 |

이 데이터가 인터넷 서버에 저장되니까, 새로고침해도 사라지지 않습니다.

## Supabase란?

Supabase는 무료로 쓸 수 있는 클라우드 데이터베이스 서비스입니다.

왜 Supabase인가:

- 무료 — 개인 프로젝트에 충분한 무료 용량
- 쉬움 — 회원가입만 하면 바로 사용 가능
- 웹 대시보드 — 브라우저에서 데이터를 직접 볼 수 있음
- 로그인 기능 내장 — 나중에 고구마마켓에서 사용
- MCP 지원 — 클코가 직접 DB를 조작할 수 있음 (이게 핵심!)

## Supabase 가입하기

### 1단계: 사이트 접속

```
https://supabase.com
```

### 2단계: 가입

Supabase 가입에는 GitHub 계정이 필요합니다.

GitHub 계정이 없으면 먼저 가입하세요:

1. https://github.com 에 접속
2. Sign up 클릭
3. 이메일, 비밀번호, 사용자명 입력 → 이메일 인증 완료

GitHub 계정이 준비되었으면:

1. Supabase 사이트에서 Start your project 클릭
2. Sign up with GitHub 클릭
3. Supabase에 GitHub 접근 허용

### 3단계: 새 프로젝트 만들기

1. New Project 클릭
2. 정보 입력:
   - Organization: 기본값 그대로
   - Project name: `my-project` (자유롭게)
   - Database Password: 기억할 수 있는 비밀번호 입력 (나중에 쓸 일 없지만 기록해두세요)
   - Region: Northeast Asia (Seoul) 선택 — 한국에서 가장 빠름
3. Create new project 클릭
4. 1~2분 기다리면 프로젝트가 생성됩니다

## MCP란?

여기서 이 강의의 핵심 개념이 나옵니다.

MCP(Model Context Protocol)는 AI에게 외부 도구를 연결하는 표준 방법입니다.

### MCP 없이

```
나: "Supabase에 테이블 만들어줘"
클코: "이런 SQL을 Supabase 대시보드에서 실행하세요" (알려주기만 함)
나: (직접 Supabase 가서 복사/붙여넣기...)
```

### MCP 연결 후

```
나: "Supabase에 테이블 만들어줘"
클코: (직접 Supabase에 접속해서 테이블 생성) "만들었습니다!"
```

MCP는 클코에게 손을 달아주는 것과 같습니다.

연결 전에는 **이렇게 하세요**라고 알려주기만 하지만,

연결 후에는 직접 해줍니다.

### 이 강의에서 연결할 MCP들

| MCP | 역할 | 배우는 챕터 |
|-----|------|------------|
| Supabase | 데이터베이스 직접 조작 | 지금 (08) |
| Context7 | 최신 기술 문서 읽기 | 16 |
| Playwright | 브라우저 자동 조작/테스트 | 18 |

## Supabase MCP 연결하기

### 1단계: Supabase에서 키 확인

1. Supabase 대시보드에서 프로젝트를 엽니다
2. 왼쪽 메뉴에서 Settings (톱니바퀴) 클릭
3. API 메뉴 클릭
4. 두 가지 정보를 복사합니다:

| 항목 | 어디에 있나 | 용도 |
|------|------------|------|
| Project URL | 상단 "Project URL" | Supabase 주소 |
| service_role key | 하단 "Project API keys" → service_role | 관리자 권한 키 |

⚠️ service_role key는 절대 외부에 공유하지 마세요!

이 키가 있으면 데이터베이스를 마음대로 조작할 수 있습니다.

### 2단계: 클코에 MCP 추가

클로드코드를 종료하고(`/exit`), 터미널에서 아래 명령어를 입력합니다.

`여기에_Project_URL`과 `여기에_service_role_key` 부분을 실제 값으로 바꿔주세요:

```
claude mcp add supabase -e SUPABASE_URL=여기에_Project_URL -e SUPABASE_SERVICE_ROLE_KEY=여기에_service_role_key -- npx -y @supabase/mcp-server-supabase@latest
```

### 3단계: 확인

클로드코드를 다시 실행합니다:

```
claude
```

연결이 잘 됐는지 확인:

```
supabase MCP 연결됐는지 확인해줘. 프로젝트 정보 보여줘.
```

클코가 Supabase 프로젝트 정보를 보여주면 성공입니다!

### 안 되면?

| 증상 | 해결 |
|------|------|
| "MCP server failed to start" | URL이나 키를 다시 확인. 복사할 때 앞뒤 공백이 없는지 확인 |
| "Invalid API key" | service_role key가 맞는지 확인. anon key가 아닌 service_role key를 써야 합니다 |
| MCP는 연결됐는데 동작 안 함 | claude를 종료하고 다시 실행 |

## MCP 연결 후 해볼 수 있는 것들

이제 클코가 직접 Supabase를 조작할 수 있습니다:

### 테이블 확인

```
Supabase에 어떤 테이블이 있는지 보여줘
```

### 테이블 만들기

```
budget이라는 테이블 만들어줘.
컬럼:
- id (자동 생성)
- date (날짜)
- type (수입/지출)
- category (카테고리)
- amount (금액)
- memo (메모)
- created_at (생성 시간, 자동)
```

### 테스트 데이터 넣기

```
budget 테이블에 테스트 데이터 5개 넣어줘.
수입 2개, 지출 3개로. 현실적인 데이터로.
```

### 데이터 확인

```
budget 테이블의 데이터 전부 보여줘
```

## 핵심 정리

- 데이터베이스 = 데이터를 영구 저장하는 곳 (엑셀의 클라우드 버전)
- Supabase = 무료 클라우드 DB 서비스
- MCP = AI에게 외부 도구를 연결하는 방법
- Supabase MCP = 클코가 DB를 직접 만들고 조작할 수 있게 해줌
- 한 번 설정하면 계속 사용 가능
