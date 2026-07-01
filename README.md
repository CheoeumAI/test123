# NIE-style Notice Board
국립생태원 강의 중
Material 3 Design System 기반의 공공기관형 공지사항 게시판입니다. 사용자 목록/상세, 관리자 로그인, 공지 CRUD, S3 호환 첨부파일 업로드, Prisma/PostgreSQL 모델을 포함합니다.

## Setup

1. 의존성을 설치합니다.

```bash
npm install
```

2. `.env.example`을 기준으로 `.env`를 만듭니다.

```bash
cp .env.example .env
```

필수 환경변수:

- `DATABASE_URL`
- `AUTH_SECRET`
- `NEXTAUTH_URL`
- `S3_ENDPOINT`
- `S3_REGION`
- `S3_BUCKET`
- `S3_ACCESS_KEY_ID`
- `S3_SECRET_ACCESS_KEY`

관리자 seed를 생성하려면 `ADMIN_EMAIL`과 `ADMIN_PASSWORD`를 `.env`에 직접 추가합니다. 두 값이 없으면 샘플 공지만 생성합니다.

3. Prisma 마이그레이션과 seed를 실행합니다.

```bash
npm run prisma:migrate
npm run prisma:seed
```

4. 개발 서버를 실행합니다.

```bash
npm run dev
```

사용자 화면은 `http://localhost:3000/notices`, 관리자 화면은 `http://localhost:3000/admin/notices`입니다.

## Scripts

- `npm run dev`: 개발 서버 실행
- `npm run build`: Prisma Client 생성 후 production build
- `npm run lint`: Next.js lint
- `npm run typecheck`: TypeScript 검사
- `npm test`: Vitest 단위 테스트
- `npm run prisma:migrate`: PostgreSQL 마이그레이션
- `npm run prisma:seed`: 샘플 공지 생성, `ADMIN_EMAIL`과 `ADMIN_PASSWORD`가 있을 때만 관리자 생성

## Project Structure

- `src/app`: Next.js App Router 라우팅 진입점과 API route 파일
- `src/frontend`: 화면 컴포넌트와 전역 스타일
- `src/backend`: 인증, DB, 스토리지, 검증, 공지 도메인 로직과 타입
- `backend/prisma`: Prisma schema와 seed
- `docs`: 작업 가이드와 에이전트 지침
- `test`: Vitest 단위 테스트
- `Material 3 Design System`: 프로젝트 디자인 시스템 원본 자산

## Design System

전역 CSS는 `src/frontend/styles/globals.css`에서 `Material 3 Design System/styles.css`를 import합니다. UI 색상, 간격, 모서리, elevation, motion은 M3 토큰을 우선 사용합니다.

## Notes

- 원본 NIE 콘텐츠는 이관하지 않았습니다. 구조와 UX 패턴만 참고했습니다.
- 삭제는 물리 삭제가 아니라 `HIDDEN` 상태 변경으로 처리합니다.
- 첨부파일은 20MB 이하만 허용하며, 허용 확장자는 `pdf`, `hwp`, `hwpx`, `doc`, `docx`, `xls`, `xlsx`, `png`, `jpg`, `jpeg`, `zip`입니다.
