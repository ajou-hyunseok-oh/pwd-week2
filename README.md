# SvelteKit 프로젝트 Vercel 배포 실습 가이드

## 📋 실습 개요

이번 실습에서는 SvelteKit을 사용하여 간단한 자기소개 웹사이트를 만들고, GitHub를 통해 코드를 관리하며, Vercel을 통해 실제로 배포하는 전체 과정을 경험합니다.

### 학습 목표
- Node.js와 npm 환경 구축
- SvelteKit 프레임워크로 정적 사이트 제작
- Git/GitHub를 활용한 버전 관리
- Vercel을 통한 자동 배포 파이프라인 구축

### 소요 시간
약 2-3시간

---

## 🔧 Step 1: Node.js 설치 및 환경 설정

### 1.1 Node.js 다운로드 및 설치

1. [Node.js 공식 사이트](https://nodejs.org) 접속
2. LTS 버전 다운로드 (2025년 기준 v20.x.x 권장)
3. 운영체제별 설치:
   - **Windows**: 다운로드한 .msi 파일 실행 → Next 클릭하며 기본 설정으로 설치
   - **Mac**: 다운로드한 .pkg 파일 실행 → 설치 마법사 따라 진행
   - **Linux**: 터미널에서 아래 명령어 실행
     ```bash
     curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
     sudo apt-get install -y nodejs
     ```

### 1.2 설치 확인

터미널(Windows는 명령 프롬프트 또는 PowerShell)을 열고 다음 명령어로 설치 확인:

```bash
node --version
# v20.x.x 형태로 버전 출력되면 성공

npm --version  
# 10.x.x 형태로 버전 출력되면 성공
```

> ⚠️ **오류 해결**: 명령어를 찾을 수 없다고 나오는 경우
> - Windows: 시스템 재시작 후 다시 시도
> - Mac/Linux: 터미널 재시작 후 다시 시도

---

## 📦 Step 2: SvelteKit 프로젝트 생성

### 2.1 프로젝트 폴더 생성 및 이동

```bash
# 작업할 폴더로 이동 (예: 바탕화면)
cd Desktop

# 프로젝트를 생성할 상위 폴더 만들기 (선택사항)
mkdir web-projects
cd web-projects
```

### 2.2 SvelteKit 프로젝트 초기화

```bash
npm create svelte@latest my-portfolio
```

### 2.3 설치 옵션 선택

대화형 프롬프트가 나타나면 다음과 같이 선택:

```
┌  Welcome to SvelteKit!
│
◇  Which Svelte app template?
│  ○ SvelteKit demo app
│  ● Skeleton project (선택)
│  ○ Library project
│
◇  Add type checking with TypeScript?
│  ○ Yes, using JavaScript with JSDoc comments
│  ● Yes, using TypeScript syntax (선택)
│  ○ No
│
◇  Select additional options (use arrow keys/space bar)
│  ◻ Add ESLint for code linting
│  ◻ Add Prettier for code formatting  
│  ◻ Add Playwright for browser testing
│  ◻ Add Vitest for unit testing
│  (Enter 키를 눌러 선택 없이 진행)
└
```

### 2.4 프로젝트 폴더로 이동 및 의존성 설치

```bash
cd my-portfolio
npm install
```

### 2.5 개발 서버 실행 테스트

```bash
npm run dev
```

브라우저에서 `http://localhost:5173` 접속하여 SvelteKit 기본 페이지 확인
- "Welcome to SvelteKit" 메시지가 보이면 성공!
- 종료: 터미널에서 `Ctrl + C` 누르기

---

## 🐙 Step 3: GitHub 저장소 생성

### 3.1 GitHub 계정 생성 (이미 있다면 스킵)

1. [GitHub](https://github.com) 접속
2. Sign up 클릭 → 이메일, 비밀번호, 사용자명 입력
3. 이메일 인증 완료

### 3.2 새 저장소 생성

1. GitHub 로그인 후 우측 상단 `+` 버튼 클릭
2. `New repository` 선택
3. 저장소 설정:
   - **Repository name**: `my-portfolio` (프로젝트명과 동일하게)
   - **Description**: "나의 포트폴리오 웹사이트" (선택사항)
   - **Public** 선택 (무료 배포를 위해 필수)
   - **Initialize this repository with** 항목들은 모두 체크 해제
4. `Create repository` 클릭

### 3.3 생성된 저장소 URL 복사

생성 후 나타나는 페이지에서 HTTPS URL 복사:
```
https://github.com/[your-username]/my-portfolio.git
```

---

## 🔗 Step 4: 로컬 프로젝트와 GitHub 저장소 연동

### 4.1 Git 초기화 및 첫 커밋

프로젝트 폴더(my-portfolio)에서 터미널 실행:

```bash
# Git 저장소 초기화
git init

# 모든 파일을 스테이징
git add .

# 첫 번째 커밋
git commit -m "Initial commit: SvelteKit 프로젝트 생성"
```

### 4.2 GitHub 저장소 연결

```bash
# 원격 저장소 추가 (복사한 URL 사용)
git remote add origin https://github.com/[your-username]/my-portfolio.git

# 브랜치 이름을 main으로 변경 (필요한 경우)
git branch -M main

# GitHub에 푸시
git push -u origin main
```

### 4.3 연동 확인

GitHub 저장소 페이지 새로고침하여 파일들이 업로드되었는지 확인

---

## 🎨 Step 5: 자기소개 페이지 작성

### 5.1 기본 레이아웃 생성

`src/routes/+layout.svelte` 파일 생성:

```svelte
<script>
  import './styles.css';
</script>

<nav>
  <a href="/">홈</a>
  <a href="/about">소개</a>
  <a href="/projects">프로젝트</a>
  <a href="/contact">연락처</a>
</nav>

<main>
  <slot />
</main>

<footer>
  <p>© 2025 My Portfolio. All rights reserved.</p>
</footer>
```

### 5.2 전역 스타일 추가

`src/routes/styles.css` 파일 생성:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Pretendard', -apple-system, sans-serif;
  line-height: 1.6;
  color: #333;
}

nav {
  background: #2c3e50;
  padding: 1rem 2rem;
  display: flex;
  gap: 2rem;
}

nav a {
  color: white;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;
}

nav a:hover {
  color: #3498db;
}

main {
  min-height: calc(100vh - 120px);
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

footer {
  background: #34495e;
  color: white;
  text-align: center;
  padding: 1rem;
}
```

### 5.3 메인 페이지 작성

`src/routes/+page.svelte` 파일 수정:

```svelte
<script>
  let name = "홍길동";
  let title = "웹 개발자";
  let skills = ["HTML/CSS", "JavaScript", "SvelteKit", "Node.js"];
</script>

<section class="hero">
  <h1>안녕하세요, {name}입니다</h1>
  <p class="subtitle">{title}</p>
  
  <div class="intro">
    <p>
      웹 개발에 열정을 가진 개발자입니다. 
      사용자 경험을 중시하며 깔끔하고 효율적인 코드를 작성하려 노력합니다.
    </p>
  </div>

  <div class="skills">
    <h2>기술 스택</h2>
    <div class="skill-list">
      {#each skills as skill}
        <span class="skill-tag">{skill}</span>
      {/each}
    </div>
  </div>
</section>

<style>
  .hero {
    text-align: center;
    padding: 4rem 0;
  }

  h1 {
    font-size: 3rem;
    color: #2c3e50;
    margin-bottom: 1rem;
  }

  .subtitle {
    font-size: 1.5rem;
    color: #7f8c8d;
    margin-bottom: 2rem;
  }

  .intro {
    max-width: 600px;
    margin: 0 auto 3rem;
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .skills {
    margin-top: 3rem;
  }

  .skill-list {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1rem;
    flex-wrap: wrap;
  }

  .skill-tag {
    background: #3498db;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.9rem;
  }
</style>
```

### 5.4 About 페이지 추가

`src/routes/about/+page.svelte` 파일 생성:

```svelte
<h1>About Me</h1>
<div class="content">
  <p>
    디지털미디어학과에서 웹 개발을 공부하고 있는 학생입니다.
    사용자 중심의 서비스를 만들기 위해 노력하고 있습니다.
  </p>
  
  <h2>교육</h2>
  <ul>
    <li>○○대학교 디지털미디어학과 재학중</li>
    <li>실무 웹 서비스 개발 수강중</li>
  </ul>
  
  <h2>관심 분야</h2>
  <ul>
    <li>프론트엔드 개발</li>
    <li>UI/UX 디자인</li>
    <li>웹 접근성</li>
  </ul>
</div>

<style>
  .content {
    max-width: 800px;
    margin: 2rem auto;
  }
  
  h2 {
    margin-top: 2rem;
    color: #2c3e50;
  }
  
  ul {
    margin-left: 2rem;
    margin-top: 1rem;
  }
  
  li {
    margin: 0.5rem 0;
  }
</style>
```

### 5.5 변경사항 저장 및 푸시

```bash
# 변경된 파일 확인
git status

# 모든 변경사항 스테이징
git add .

# 커밋
git commit -m "feat: 자기소개 페이지 완성"

# GitHub에 푸시
git push origin main
```

---

## 🚀 Step 6: Vercel 배포

### 6.1 Vercel 계정 생성

1. [Vercel](https://vercel.com) 접속
2. `Sign Up` 클릭
3. **Continue with GitHub** 선택 (GitHub 계정으로 로그인)
4. GitHub 권한 승인

### 6.2 새 프로젝트 Import

1. Vercel 대시보드에서 `Add New...` → `Project` 클릭
2. GitHub 저장소 목록에서 `my-portfolio` 찾기
3. 저장소 옆 `Import` 버튼 클릭

### 6.3 프로젝트 설정

Import 페이지에서 다음 설정 확인:

- **Project Name**: my-portfolio (자동 입력됨)
- **Framework Preset**: SvelteKit (자동 감지됨)
- **Root Directory**: ./ (기본값)
- **Build Command**: `npm run build` (자동 설정)
- **Output Directory**: `.svelte-kit` (자동 설정)
- **Install Command**: `npm install` (자동 설정)

환경 변수는 현재 필요없으므로 그대로 두고 `Deploy` 클릭

### 6.4 배포 진행 확인

1. 배포가 시작되면 실시간 로그 확인 가능
2. 일반적으로 1-3분 내 완료
3. "Congratulations!" 메시지와 함께 배포 완료

### 6.5 배포된 사이트 확인

- 제공된 URL 클릭 (형식: `https://my-portfolio-[random].vercel.app`)
- 사이트가 정상적으로 표시되는지 확인

> 💡 **프로덕션 URL**: Vercel은 고정 URL도 제공합니다
> - 형식: `https://my-portfolio.vercel.app`
> - 이 URL은 항상 최신 배포를 가리킵니다

### 6.6 자동 배포 테스트

이제 GitHub main 브랜치에 푸시할 때마다 자동으로 재배포됩니다:

```bash
# 테스트: 작은 변경 후 푸시
echo "# 자동 배포 테스트" >> README.md
git add README.md
git commit -m "test: 자동 배포 확인"
git push origin main
```

Vercel 대시보드에서 새 배포가 시작되는 것 확인

---

## ✅ 과제 제출 체크리스트

### 필수 제출 항목
- [ ] GitHub 저장소 URL
- [ ] Vercel 배포 URL (`.vercel.app` 도메인)
- [ ] 자기소개 페이지 포함 여부
- [ ] 최소 2개 이상의 페이지 구성

### 평가 기준

#### 기능 구현 (40%)
- SvelteKit 프로젝트 정상 생성
- 라우팅 구현 (여러 페이지 이동)
- 자기소개 컨텐츠 포함

#### Git 사용 (30%)
- 의미있는 커밋 메시지
- 단계별 커밋 (최소 3개 이상)
- GitHub 저장소 정상 연동

#### 배포 (30%)
- Vercel 배포 성공
- 배포된 사이트 정상 작동
- 자동 배포 파이프라인 구축

---

## 🔍 자주 발생하는 문제와 해결법

### Q1. npm 명령어를 찾을 수 없다고 나옵니다

**A:** Node.js가 제대로 설치되지 않았거나 PATH 설정 문제입니다.
- Windows: Node.js 재설치 후 컴퓨터 재시작
- Mac/Linux: `source ~/.bashrc` 또는 `source ~/.zshrc` 실행

### Q2. GitHub 푸시 시 인증 오류가 발생합니다

**A:** 2021년부터 비밀번호 대신 토큰 사용 필요:
1. GitHub → Settings → Developer settings → Personal access tokens
2. Generate new token (classic) 선택
3. repo 권한 체크 → Generate token
4. 비밀번호 대신 생성된 토큰 사용

### Q3. Vercel 배포가 실패합니다

**A:** Build 로그 확인하여 오류 메시지 체크:
- `package.json` 파일이 저장소 루트에 있는지 확인
- 모든 파일이 GitHub에 푸시되었는지 확인
- Node.js 버전 호환성 문제일 경우 Vercel 설정에서 Node 버전 지정

### Q4. 로컬에서는 작동하는데 배포 후 오류가 발생합니다

**A:** 대소문자 구분 문제일 가능성이 높음:
- Windows는 대소문자 구분 안 함, Vercel(Linux)은 구분함
- 파일명과 import 구문의 대소문자가 정확히 일치하는지 확인

---

## 📚 추가 학습 자료

### 공식 문서
- [SvelteKit 공식 문서](https://kit.svelte.dev/docs)
- [Vercel 문서](https://vercel.com/docs)
- [Git 기초 가이드](https://git-scm.com/book/ko/v2)

### 다음 단계 학습
1. **동적 라우팅**: 파라미터를 활용한 동적 페이지 생성
2. **API 라우트**: SvelteKit에서 백엔드 API 구현
3. **데이터베이스 연동**: Supabase, MongoDB 등 연결
4. **인증 구현**: 로그인/회원가입 기능 추가

### 유용한 VS Code 확장 프로그램
- Svelte for VS Code: Svelte 문법 하이라이팅
- GitLens: Git 히스토리 시각화
- Prettier: 코드 자동 포맷팅
- Thunder Client: API 테스트 도구

---

## 🎯 실습 완료!

축하합니다! 여러분은 이제:
- ✅ Node.js 환경을 구축했습니다
- ✅ SvelteKit 프로젝트를 생성했습니다
- ✅ Git/GitHub로 버전 관리를 시작했습니다
- ✅ 실제 웹사이트를 인터넷에 배포했습니다

이것은 웹 개발자로서의 첫 걸음입니다. 계속해서 기능을 추가하고 개선해나가세요!

---

## 💡 추가 정보: 도메인 연결 (선택사항)

Vercel의 기본 `.vercel.app` 도메인으로 충분하지만, 커스텀 도메인을 연결하고 싶다면:

1. **무료 도메인 옵션**
   - Cafe24 이벤트 도메인 (한국)
   - EU.org 서브도메인 (글로벌)
   
2. **연결 방법**
   - Vercel 대시보드 → Settings → Domains
   - 도메인 추가 후 DNS 설정
   - 자동 HTTPS 인증서 발급

> 📌 **참고**: 이 부분은 개인적으로 진행하시면 됩니다. 수업에서는 Vercel 기본 도메인으로 충분합니다!
