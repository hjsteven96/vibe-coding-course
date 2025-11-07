# 🔐 Chapter 8: "영구 기억" (Cloud Database) - 어디서든 + 로그인

> **목표:** 클라우드 데이터베이스(Supabase)를 사용해서 어느 기기에서든 같은 데이터를 보고, 로그인으로 내 메모를 보호합니다.

## Step 8.1: AI에게 Supabase 프로젝트 생성 지시하기

이제 AI가 거의 모든 것을 자동으로 해줄 수 있습니다!

1. 먼저 [Supabase 웹사이트](https://supabase.com/)에 접속해서 GitHub 계정으로 로그인합니다.

2. `New Project` 버튼을 클릭하고:
   - **Name**: `my-vibe-canvas`
   - **Database Password**: 강력한 비밀번호 입력 (꼭 메모해 두세요!)
   - **Region**: `Northeast Asia (Seoul)` 선택
   - `Create new project` 버튼 클릭

3. 프로젝트가 생성되는 동안(약 2분) 기다립니다.

## Step 8.2: Supabase API 키 가져오기

1. 프로젝트 대시보드 왼쪽 메뉴에서 `Settings` (톱니바퀴 아이콘) > `API`를 클릭합니다.

2. **Project URL**과 **anon public key**를 복사해 둡니다.

## Step 8.3: AI에게 Supabase 연결 지시하기

이제 AI가 모든 설정을 자동으로 해줍니다!

1. Cursor로 돌아와 우측 **채팅창**을 엽니다.

2. 이렇게 말합니다:

   > "이제 Supabase를 연결하려고 해. Supabase SDK를 설치하고, 
   > 
   > Project URL: (여기에 복사한 URL 붙여넣기)
   > anon key: (여기에 복사한 anon key 붙여넣기)
   > 
   > 이 정보를 .env.local 파일에 저장하고, Supabase 클라이언트를 초기화하는 코드를 만들어 줘. 
   > Authentication과 Database를 사용할 거야."

3. AI가 자동으로:
   - ✅ `npm install @supabase/supabase-js` 실행
   - ✅ `.env.local` 파일 생성 및 환경변수 저장
   - ✅ Supabase 클라이언트 초기화 코드 생성

## Step 8.4: 데이터베이스 테이블 생성하기

Supabase에서 메모를 저장할 테이블을 만들어야 합니다.

1. 우측 **채팅창**에 이렇게 말합니다:

   > "Supabase에서 메모를 저장할 테이블을 만들려고 해. 
   > 
   > 테이블 이름: vibes
   > 컬럼: 
   > - id (uuid, primary key, auto-generated)
   > - user_id (uuid, 사용자 ID)
   > - title (text, 제목)
   > - content (text, 본문)
   > - created_at (timestamp, 생성일시)
   > 
   > 이 테이블을 만드는 SQL 쿼리를 알려줘. 그리고 Row Level Security(RLS)를 활성화해서 각 사용자가 자기 메모만 볼 수 있게 해줘."

2. AI가 SQL 쿼리를 만들어 줄 겁니다.

3. **Supabase 대시보드**로 가서:
   - 왼쪽 메뉴에서 `SQL Editor` 클릭
   - AI가 만들어준 SQL 쿼리를 복사해서 붙여넣기
   - `Run` 버튼 클릭

## Step 8.5: 로그인 기능 추가하기

1. 우측 **채팅창**에 `@app/page.tsx`를 입력하고:

   > "@app/page.tsx 이제 Supabase로 로그인 기능을 추가하려고 해. 페이지 상단에 '로그인' 버튼을 만들어 줘. 로그인하지 않은 사용자는 이메일과 비밀번호로 회원가입/로그인할 수 있게 해줘. 로그인한 사용자는 이메일이 표시되고 '로그아웃' 버튼이 보이게 해줘."

2. AI가 Supabase Authentication을 이용한 로그인 UI와 로직을 만들어 줄 겁니다.

3. 브라우저에서 테스트해보세요. 이메일과 비밀번호로 회원가입이 되나요?

## Step 8.6: 메모를 Supabase에 저장하기

1. 우측 **채팅창**에 `@app/page.tsx`를 입력하고:

   > "@app/page.tsx 이제 localStorage 대신 Supabase를 사용하게 바꿔줘. 로그인한 사용자의 메모만 'vibes' 테이블에 저장하고, 로그인한 사용자 본인의 메모만 불러오게 해줘. user_id로 필터링해서 관리해 줘."

2. AI가 코드를 수정해 줄 겁니다.

3. 브라우저에서 테스트해보세요:
   - 로그인하고 메모를 추가합니다.
   - 새로고침을 해도 메모가 남아있나요?
   - **다른 브라우저나 시크릿 모드로 같은 계정으로 로그인해보세요.** 같은 메모가 보이나요? 🎉
   - Supabase 대시보드의 `Table Editor`에서 데이터가 실제로 저장되는지 확인해보세요!

## Step 8.7: Vercel에 다시 배포하기 (환경 변수 추가)

1. 코드를 GitHub에 push합니다:

   ```bash
   git add .
   git commit -m "Add Supabase authentication and database"
   git push
   ```

2. [Vercel 대시보드](https://vercel.com/dashboard)로 이동합니다.

3. 내 프로젝트를 클릭하고 `Settings` > `Environment Variables`로 갑니다.

4. `.env.local` 파일에 있는 환경 변수를 추가합니다:
   - `NEXT_PUBLIC_SUPABASE_URL` = (여러분의 Supabase Project URL)
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY` = (여러분의 Supabase anon key)

5. `Deployments` 탭으로 가서 `Redeploy` 버튼을 누릅니다.

6. 배포가 완료되면, 실제 URL에서도 로그인과 메모 저장이 잘 작동하는지 확인하세요!

## 🔥 8단계 성과

**축하합니다!** 여러분은 이제:

- ✅ 로그인/회원가입 기능이 있는 웹 앱을 만들었습니다.
- ✅ 클라우드 데이터베이스를 사용해 어느 기기에서든 같은 데이터를 볼 수 있습니다.
- ✅ 사용자별로 데이터가 분리되는 진짜 서비스를 만들었습니다.
- ✅ 인터넷에 배포된 실제 웹 서비스를 완성했습니다.

**이제 여러분은 코딩 없이도 AI와 함께 풀스택 웹 개발자가 되었습니다!** 🚀

---

**다음:** [Chapter 9: "심화 기능" (Advanced Features) - 진짜 앱처럼 만들기](./chapter-9-심화기능.md)

