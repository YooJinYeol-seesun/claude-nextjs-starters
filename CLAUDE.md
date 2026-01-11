# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 개발 환경

- **Framework**: Next.js 16.1.1 (App Router)
- **Language**: TypeScript 5 (strict mode)
- **Runtime**: Node.js LTS
- **Styling**: Tailwind CSS v4 (with @tailwindcss/postcss)
- **Package Manager**: npm (사용 가능)
- **UI Components**: shadcn/ui (configured with New York style, RSC enabled)
- **Icon Library**: lucide-react

## 자주 사용하는 명령어 

### 개발 및 빌드
```bash
npm run dev        # 개발 서버 실행 (http://localhost:3000)
npm run build      # 프로덕션 빌드
npm start          # 프로덕션 서버 실행
npm run lint       # ESLint 실행
```

## 코드 구조

```
.
├── app/                    # Next.js App Router
│   ├── layout.tsx          # 루트 레이아웃 (글꼴, 메타데이터)
│   ├── page.tsx            # 홈페이지
│   └── globals.css         # 전역 스타일 (Tailwind + CSS 변수)
├── lib/
│   └── utils.ts            # cn() 유틸리티 함수 (clsx + tailwind-merge)
├── components/             # shadcn/ui 컴포넌트 (cli로 추가됨)
├── public/                 # 정적 자산
├── components.json         # shadcn/ui 설정
├── tsconfig.json           # TypeScript 설정 (경로: @/*)
├── eslint.config.mjs       # ESLint 설정 (Next.js + TypeScript)
├── postcss.config.mjs      # PostCSS 설정 (@tailwindcss/postcss)
└── next.config.ts          # Next.js 설정
```

## 아키텍처 특징

### 스타일링
- **Tailwind CSS v4**: 최신 문법 (@import, @theme 등)
- **CSS 변수**: OKLch 색상 시스템 사용
  - 라이트 모드: 밝은 배경 (oklch(1 0 0))
  - 다크 모드: 어두운 배경 (oklch(0.145 0 0))
  - sidebar, chart, accent 등 전용 색상 변수 제공
- **유틸리티**: `lib/utils.ts`의 `cn()` 함수로 클래스 병합 (clsx + tailwind-merge)

### shadcn/ui 설정
- **경로 별칭**:
  - `@/components` → components 디렉토리
  - `@/components/ui` → UI 컴포넌트
  - `@/lib/utils` → 유틸리티 함수
  - `@/hooks` → 커스텀 훅
- **설정파일**: `components.json` (New York style, RSC enabled)
- **추가 방법**: `npx shadcn-ui@latest add [component-name]`

### 타입스크립트
- `strict: true` 모드 활성화
- 경로 별칭: `@/*` → 프로젝트 루트
- JSX: `react-jsx` (React 19 호환)

### ESLint
- Next.js Core Web Vitals 규칙 적용
- TypeScript 지원 활성화
- 제외 대상: `.next/`, `out/`, `build/`, `next-env.d.ts`

## 개발 가이드라인

### 컴포넌트 작성
- **위치**: `components/` 또는 `app/` 내부
- **명명**: PascalCase (예: `UserCard.tsx`)
- **RSC 기본**: shadcn/ui 컴포넌트는 RSC 호환

### 스타일 추가
- Tailwind 클래스 우선 사용
- 필요시 `app/globals.css`에 CSS 변수 추가
- `cn()` 함수로 조건부 스타일 처리

### shadcn/ui 컴포넌트 사용
1. `npx shadcn-ui@latest add [component-name]` 실행
2. 자동으로 `components/ui/` 에 설치됨
3. 타입스크립트 지원, 커스터마이징 가능

## 주요 의존성

- **next**: 16.1.1 (App Router)
- **react**: 19.2.3
- **react-dom**: 19.2.3
- **tailwindcss**: 4.x (@tailwindcss/postcss 사용)
- **class-variance-authority**: CVA 패턴 지원
- **clsx & tailwind-merge**: 스타일 유틸리티
- **lucide-react**: 아이콘 라이브러리
- **eslint & eslint-config-next**: 코드 품질

## 참고사항

- Tailwind CSS v4의 새로운 문법 사용 (tailwind.config.js 불필요)
- CSS 변수는 `app/globals.css`의 `:root`와 `.dark`에 정의됨
- 다크 모드 지원: HTML 요소에 `.dark` 클래스 추가 필요
