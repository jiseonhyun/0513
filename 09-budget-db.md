# 가계부에 DB 붙이기.

> CHAPTER 09 / 27 · PART 2 · 가계부 만들기 · 예상 시간 50분

## 이번 챕터의 목표

앞에서 만든 가계부에 Supabase를 연결해서 새로고침해도 데이터가 남아있게 만듭니다.

## 지금까지의 상태

```
✅ 가계부 웹앱 완성 (입력, 목록, 합계)
✅ Supabase 가입 완료
✅ Supabase MCP 연결 완료
❌ 데이터 영구 저장 (이번 챕터에서 해결!)
```

## 1단계: 가계부 프로젝트에서 클코 실행

```
cd C:\claude-projects\my-budget
claude
```

## 2단계: 클코에게 DB 연결 시키기

아래 프롬프트를 복사해서 붙여넣으세요:

```
이 가계부 앱에 Supabase를 연결해줘.

현재 상태:

가계부 웹앱이 Next.js로 만들어져 있음
수입/지출 입력, 목록 보기, 합계 표시 기능이 있음
데이터가 새로고침하면 사라짐 (현재 state로만 관리)
Supabase MCP가 연결되어 있음

해줘야 할 것:

Supabase에 budget 테이블 만들기

id (UUID, 자동생성)
date (날짜)
type (수입/지출)
category (카테고리)
amount (금액, 정수)
memo (메모, nullable)
created_at (자동)

RLS(Row Level Security) 정책 설정

일단 모든 사용자가 읽기/쓰기 가능하게 (나중에 로그인 붙이면 변경)

앱에서 Supabase 연결

@supabase/supabase-js 패키지 설치
환경변수로 URL과 키 관리
입력하면 Supabase에 저장
페이지 열면 Supabase에서 불러오기
삭제도 Supabase에서 삭제

환경변수 파일 (.env.local):
```

클코가 Supabase MCP로 테이블을 직접 만들고, 앱 코드도 수정합니다.

## 3단계: 환경변수 설정

클코가 `.env.local` 파일을 만들어줄 겁니다.

값을 채워야 합니다.

### Supabase에서 확인하는 법

1. Supabase 대시보드 → Settings → API
2. 두 가지를 복사:

| 항목 | 찾는 위치 | 환경변수 이름 |
|------|----------|--------------|
| Project URL | 상단 "Project URL" | NEXT_PUBLIC_SUPABASE_URL |
| anon public key | "Project API keys" → anon public | NEXT_PUBLIC_SUPABASE_ANON_KEY |

⚠️ 여기서는 anon key를 사용합니다. MCP 설정 때 쓴 service_role key가 아닙니다!

anon key는 매우 긴 문자열입니다(`eyJ...`로 시작). 전체를 빠짐없이 복사했는지 확인하세요. 중간에 잘려서 복사되면 연결이 안 됩니다.

- anon key = 일반 사용자용 (앱에서 사용, 공개해도 됨)
- service_role key = 관리자용 (MCP에서 사용, 비공개)

### 환경변수 파일 확인

`.env.local` 파일이 이렇게 되어있어야 합니다:

```
NEXT_PUBLIC_SUPABASE_URL=https://xxxxx.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.xxxxx
```

클코가 자동으로 만들어줬을 수도 있고, 직접 값을 넣으라고 할 수도 있습니다.

값이 비어있으면 Supabase 대시보드에서 복사해서 넣어주세요.

### .env.local 파일을 직접 편집하는 법

클코에게 시키는 게 가장 쉽지만, 직접 편집해야 할 때도 있습니다:

방법 1: 클코에게 시키기 (추천)

```
.env.local 파일의 NEXT_PUBLIC_SUPABASE_URL 값을 https://abcde.supabase.co 로 바꿔줘
```

방법 2: VS Code에서 직접 편집

1. VS Code 왼쪽 사이드바에서 `.env.local` 파일을 클릭
2. 파일이 열리면 값을 직접 수정
3. Ctrl + S로 저장

`.env.local` 파일이 안 보인다면, VS Code 왼쪽 사이드바 상단의 탐색기 아이콘을 클릭하세요.

파일명이 `.`으로 시작하는 숨김 파일이라 안 보일 수 있습니다.

VS Code에서는 보통 정상적으로 표시됩니다.

## 4단계: 개발 서버 재시작

환경변수를 바꿨으면 개발 서버를 재시작해야 합니다:

```
개발 서버 다시 시작해줘
```

환경변수는 서버 시작 시점에 읽어들입니다.

변경 후 재시작 안 하면 이전 값이 사용됩니다.

## 5단계: 확인하기

### 테스트 1: 데이터 입력

1. 브라우저에서 http://localhost:3000 을 엽니다
2. 수입/지출 데이터를 2~3개 입력합니다
3. 목록에 나타나는지 확인합니다

### 테스트 2: 새로고침

1. 브라우저를 새로고침합니다 (F5)
2. 데이터가 살아있으면 성공! 🎉

### 테스트 3: Supabase 대시보드에서 확인

1. Supabase 사이트 → Table Editor 메뉴
2. budget 테이블을 클릭
3. 방금 입력한 데이터가 여기에도 보이면 완벽!

## 잘 안 될 때

### 데이터가 저장 안 되면

```
가계부에서 데이터 입력하면 저장이 안 돼.
브라우저 콘솔(F12)에 이런 에러가 나와:
[콘솔 에러 스크린샷]
```

### 흔한 원인들

| 에러 메시지 | 원인 | 해결 |
|------------|------|------|
| relation "budget" does not exist | 테이블이 안 만들어짐 | "budget 테이블 만들어줘" |
| new row violates row-level security | RLS 정책 문제 | "RLS 정책 설정해줘. 모든 사용자 허용으로" |
| Invalid API key | 환경변수 잘못됨 | .env.local 파일의 키 확인 |
| fetch failed / network error | URL 잘못됨 | NEXT_PUBLIC_SUPABASE_URL 확인 |
| 에러 없는데 데이터 안 보임 | 서버 재시작 필요 | "개발 서버 다시 시작해줘" |

## 체크리스트

- Supabase에 budget 테이블이 생겼다
- 가계부에서 데이터를 입력하면 저장된다
- 새로고침해도 데이터가 유지된다
- Supabase 대시보드에서 데이터를 확인할 수 있다
- 삭제도 정상 동작한다
