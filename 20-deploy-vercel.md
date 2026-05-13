# 세상에 공개하기 — Vercel 배포.

> CHAPTER 20 / 27 · PART 3 · 고구마마켓 · 예상 시간 30분

## 이번 챕터의 목표

지금까지 만든 고구마마켓을 인터넷에 공개합니다.

내 PC가 아닌, 전세계 누구나 접속할 수 있는 사이트로 만듭니다.

이번 챕터가 끝나면 친구에게 링크를 보낼 수 있습니다.

"이 사이트 내가 만들었어!" — 이 순간이 이 강의의 하이라이트입니다.

## 지금까지의 상황

지금까지 `localhost:3000`에서만 작동하는 고구마마켓을 만들었습니다.

```
localhost:3000 = 내 PC에서만 볼 수 있는 주소
```

이걸 누구나 볼 수 있게 하려면 인터넷 어딘가에 올려야 합니다. 이걸 **배포(deploy)** 라고 합니다.

```
localhost:3000 (나만 볼 수 있음)
        ↓  배포
goguma-market.vercel.app (전세계 누구나 볼 수 있음)
```

## Vercel이란?

Vercel은 웹사이트를 인터넷에 공개해주는 서비스입니다.

### 왜 Vercel인가?

| 특징 | 설명 |
|------|------|
| 무료 | 개인 프로젝트는 무료로 배포 가능 |
| 쉬움 | GitHub에 올리면 자동 배포 |
| 빠름 | 전세계 서버에서 제공 (한국 포함) |
| Next.js 최적화 | Next.js를 만든 회사가 Vercel (최고의 궁합) |
| 도메인 제공 | 내이름.vercel.app 무료 도메인 |
| HTTPS | 보안 인증서 자동 적용 |

다른 선택지도 있지만(AWS, Netlify 등), Next.js 프로젝트는 Vercel이 가장 편합니다.

## 사전 준비: GitHub에 코드 올리기

Vercel은 GitHub에서 코드를 가져와서 배포합니다. 11챕터에서 GitHub에 올렸다면 이미 준비 완료입니다.

아직 안 했다면:

```
이 프로젝트를 GitHub에 올려줘.
저장소 이름은 goguma-market으로.
```

클코가 git init → GitHub 저장소 생성 → 코드 push까지 해줍니다.

### 주의: .env.local은 올리면 안 됩니다

```
.gitignore 파일에 .env.local이 포함되어 있는지 확인해줘.
없으면 추가해줘.
```

`.env.local`에는 시크릿 키가 들어있으므로, 절대 GitHub에 올라가면 안 됩니다. Vercel에는 별도로 환경변수를 설정합니다.

## Vercel 가입

### 1단계: 사이트 접속

```
https://vercel.com
```

### 2단계: GitHub 계정으로 가입

1. Sign Up 클릭
2. Continue with GitHub 선택
3. GitHub 계정 연동 허용

GitHub 계정으로 가입하면, GitHub 저장소를 바로 연결할 수 있어 편합니다.

## 배포하기

두 가지 방법이 있습니다. 둘 다 결과는 같습니다.

### 방법 1: 클코에게 시키기 (추천)

```
이 프로젝트를 Vercel에 배포해줘.
```

클코가 Vercel CLI를 사용해서 배포합니다. 처음이라면 로그인 과정이 나올 수 있습니다.

브라우저가 열리면서 Vercel 로그인을 요청할 수 있습니다. 로그인하면 됩니다.

### 방법 2: Vercel 웹사이트에서 직접

1. Vercel 대시보드(https://vercel.com/dashboard) 접속
2. Add New... → Project 클릭
3. Import Git Repository에서 `goguma-market` 저장소 선택
4. Framework Preset이 Next.js로 자동 감지되는지 확인
5. Deploy 클릭

몇 분 후 배포가 완료됩니다!

## 환경변수 설정

이 단계가 매우 중요합니다. 빠뜨리면 사이트가 제대로 동작하지 않습니다.

`.env.local`에 있던 환경변수를 Vercel에도 넣어줘야 합니다.

### 방법 1: 클코에게 시키기

```
Vercel에 다음 환경변수를 설정해줘:
- NEXT_PUBLIC_SUPABASE_URL
- NEXT_PUBLIC_SUPABASE_ANON_KEY
- NEXT_PUBLIC_TOSS_CLIENT_KEY
- TOSS_SECRET_KEY
값은 .env.local에 있는 것과 동일하게.
```

### 방법 2: Vercel 웹에서 직접

1. Vercel 대시보드에서 배포한 프로젝트 클릭
2. Settings 탭 → Environment Variables
3. 하나씩 추가:

| Key | Value | 참고 |
|-----|-------|------|
| NEXT_PUBLIC_SUPABASE_URL | .env.local에서 복사 | Supabase 프로젝트 URL |
| NEXT_PUBLIC_SUPABASE_ANON_KEY | .env.local에서 복사 | Supabase 공개 키 |
| NEXT_PUBLIC_TOSS_CLIENT_KEY | .env.local에서 복사 | 토스 클라이언트 키 |
| TOSS_SECRET_KEY | .env.local에서 복사 | 토스 시크릿 키 |

4. 환경변수를 추가한 후 재배포가 필요합니다:
   - Vercel 대시보드 → Deployments 탭 → 가장 최근 배포의 ... 메뉴 → Redeploy

흔한 실수: 환경변수를 추가하고 재배포를 안 하는 것!

환경변수는 배포 시점에 적용되므로, 추가 후 반드시 재배포하세요.

## Supabase 리다이렉트 URL 설정

배포하면 새로운 도메인이 생깁니다 (예: `goguma-market.vercel.app`).

소셜 로그인이 이 도메인에서도 작동하려면, Supabase에 새 도메인을 알려줘야 합니다.

### 설정 방법

1. Supabase 대시보드 → Authentication → URL Configuration
2. Site URL을 배포된 URL로 변경:

```
https://goguma-market-xxx.vercel.app
```

3. Redirect URLs에 추가:

```
https://goguma-market-xxx.vercel.app/**
```

4. Save 클릭

### 구글/카카오 콘솔에서도 추가

구글 (Google Cloud Console):

1. APIs & Services → Credentials → OAuth 클라이언트 선택
2. Authorized redirect URIs에 추가:

```
https://[프로젝트ID].supabase.co/auth/v1/callback
```

(이미 있다면 추가할 필요 없음 — Supabase가 리다이렉트를 중계하므로)

카카오 (Kakao Developers):

1. 내 애플리케이션 → 카카오 로그인 → Redirect URI에 이미 Supabase URL이 있으면 OK
   (Supabase URL이 이미 등록되어 있다면 추가 작업 불필요)

핵심: 로그인 흐름은 항상 Supabase URL을 거치므로, Supabase의 Redirect URLs에 Vercel 도메인을 추가하는 것이 가장 중요합니다.

## 배포 확인

배포가 완료되면 Vercel이 URL을 알려줍니다:

```
https://goguma-market-xxx.vercel.app
```

이 주소를 브라우저에서 열어보세요!

### 확인 체크리스트

- 메인 페이지가 정상적으로 열리는가?
- 상품 목록이 표시되는가? (Supabase 연결 확인)
- 상품 등록이 되는가?
- 구글/카카오 로그인이 되는가?
- 결제 위젯이 나타나는가?
- 스마트폰으로 접속해도 잘 보이는가?

### 안 되면?

| 증상 | 원인 | 해결 |
|------|------|------|
| 빌드 실패 (배포 자체가 안 됨) | 코드에 에러가 있음 | Vercel → Deployments → 로그 확인, 클코에게 전달 |
| 페이지는 열리는데 데이터가 안 나옴 | 환경변수 미설정 | Vercel Settings → Environment Variables 확인 |
| 로그인이 안 됨 | Redirect URL 미설정 | Supabase URL Configuration 확인 |
| "500 Internal Server Error" | 서버 에러 | Vercel → Functions 로그 확인, 클코에게 전달 |
| 결제가 안 됨 | 토스 키 미설정 | 환경변수에 토스 키가 있는지 확인 |
| 환경변수 추가했는데 반영 안 됨 | 재배포 안 함 | Vercel → Deployments → Redeploy |

## 자동 배포

이제부터 정말 편해집니다.

코드를 GitHub에 push하면, Vercel이 자동으로 새 버전을 배포합니다.

```
코드 수정 → git push → Vercel이 자동 감지 → 자동 빌드 → 자동 배포 → 사이트 업데이트
```

즉, 이렇게 하면 됩니다:

```
[기능 수정/추가를 클코에게 시킨 후]
지금까지 작업한 거 커밋하고 GitHub에 푸시해줘.
```

1~2분 후 Vercel에서 자동으로 새 버전이 배포됩니다.

Vercel 대시보드에서 배포 상태를 실시간으로 확인할 수 있습니다.

## 커스텀 도메인 (선택)

기본으로 받는 `xxx.vercel.app` 대신 나만의 도메인을 쓰고 싶다면:

### 도메인 구매

- 가비아 (https://gabia.com) — 한국 서비스
- Namecheap (https://namecheap.com) — 해외 서비스
- `.com` 도메인은 연간 1~2만원 정도

### Vercel에 연결

1. Vercel 대시보드 → Settings → Domains
2. 구매한 도메인 입력 (예: `goguma-market.com`)
3. Vercel이 안내하는 DNS 설정을 도메인 관리 사이트에서 설정
4. 설정 완료 후 10~30분 기다리면 적용

커스텀 도메인은 선택사항입니다. `vercel.app` 도메인으로도 충분합니다.

나중에 필요할 때 추가해도 됩니다.

## 축하합니다!

여러분이 만든 고구마마켓이 인터넷에 공개되었습니다!

URL을 친구, 가족에게 보내보세요. 스마트폰으로도 접속됩니다.

```
"이 사이트 내가 만들었어!"
https://goguma-market-xxx.vercel.app
```

비개발자가 코드 한 줄 직접 쓰지 않고, 클코와 대화만으로 이걸 만들었습니다:

- 상품 등록/수정/삭제
- 구글/카카오 소셜 로그인
- 토스페이먼츠 결제
- Supabase 데이터베이스
- 인터넷 배포

이것이 AI 시대의 개발입니다.

## 핵심 정리

- 배포 = 내 PC에서만 보이던 사이트를 인터넷에 공개하는 것
- Vercel = Next.js에 최적화된 무료 배포 서비스
- 환경변수는 Vercel에도 별도로 설정해야 함 (설정 후 재배포 필수!)
- Supabase Redirect URL에 배포 도메인 추가 필수 (소셜 로그인 작동에 필요)
- 자동 배포: `git push`하면 Vercel이 알아서 새 버전 배포
- 커스텀 도메인: 선택사항, 나중에 추가 가능
