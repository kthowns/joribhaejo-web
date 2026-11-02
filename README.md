# 조립해조 (Joribhaejo)

**구름톤 in 판교에서 조립해조 팀이 개발한 Spring Boot + Next.js 커뮤니티 프로젝트입니다.**

게시판별로 글을 읽고 작성하며 댓글, 좋아요, 쪽지로 소통할 수 있습니다. 웹 개발·모바일·백엔드·하드웨어·AI/ML 등 IT 분야별 카테고리와 제목 검색을 제공합니다.

이 저장소는 [팀 원본 저장소](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web)를 fork한 저장소입니다. 아래에는 프로젝트의 주요 기능과 제가 기여한 작업을 정리했습니다.

## 주요 기능

| 영역 | 구현 내용 |
| --- | --- |
| 회원 | 회원가입, JWT 로그인, 내 정보 조회, BCrypt 비밀번호 암호화 |
| 게시판·게시글 | 게시판 조회·관리 API, 게시글 작성·조회·수정·삭제, 제목 검색, 카테고리 필터, 목록 페이지네이션 API |
| 댓글 | 댓글·답글 조회와 작성, 댓글 수정·삭제 |
| 좋아요 | 게시글·댓글 좋아요 토글, 좋아요 수 및 내가 좋아요한 게시글 ID 조회 |
| 쪽지 | 사용자 이름으로 쪽지 전송, 받은 쪽지·보낸 쪽지 목록과 상세 조회, 삭제 |
| 웹 화면 | 게시판 전환, 글 목록·상세·작성 화면, 로그인·회원가입 폼, 쪽지 모달, 라이트·다크 테마 |

해커톤 당시 코드를 기준으로 정리했습니다. API 구현과 화면의 전체 동작 검증은 구분되며, 프론트 API 연동 PR에서 확인되는 작업은 로그인, 게시글 목록·작성·상세, 댓글 목록입니다.

## 주요 기여

저는 백엔드 API와 인증·배포 구성을 구현하고, 프론트엔드의 주요 화면에 API를 연결했습니다. 아래 내용은 원본 저장소에 병합된 제 PR을 기준으로 정리했습니다.

| 영역 | 제가 수행한 작업 | 관련 PR |
| --- | --- | --- |
| 회원·인증·쪽지 | 사용자·쪽지 API와 Spring Security + JWT 인증을 구현했습니다. | [#1](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/1), [#2](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/2) |
| 게시글 | 게시글 API를 구현했습니다. 현재 코드에는 검색·카테고리 필터·페이지네이션과 작성자 확인 로직이 포함되어 있습니다. | [#3](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/3), [#4](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/4) |
| 게시판·댓글·좋아요 | 게시판·댓글 API와 좋아요 기능을 구현하고, 게시글·댓글 응답에 좋아요 수를 포함하도록 수정했습니다. | [#5](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/5), [#7](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/7), [#9](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/9) |
| API 문서·접근 설정 | Swagger·CORS 설정과 엔드포인트 설명·인증 토큰 입력을 구성하고 Security 설정을 수정했습니다. | [#8](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/8), [#9](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/9) |
| 배포 자동화 | 백엔드 배포 워크플로를 구성했습니다. 현재 워크플로는 Next.js 정적 빌드와 Spring Boot JAR·Docker 이미지 빌드, EC2 배포를 연결합니다. | [#1](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/1), [워크플로](.github/workflows/deploy-main.yml) |
| 프론트 API 연동 | 로그인, 게시글 목록·작성·상세, 댓글 목록 화면을 구현하고 API와 연결했습니다. | [#17](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pull/17) |

전체 작업 내역은 [원본 저장소 PR 목록](https://github.com/Goormthon-full-stack-joribhaejo/joribhaejo-web/pulls?q=is%3Apr)에서 확인할 수 있습니다.

## 기술 스택

| 구분 | 기술 |
| --- | --- |
| Backend | Java 17, Spring Boot 3.5.4, Spring Security, Spring Data JPA, JWT, MySQL |
| Frontend | Next.js 15.2.4, React 19, TypeScript, TanStack Query 5 |
| UI | Tailwind CSS, Radix UI, React Hook Form, Zod, Lucide, next-themes |
| API 문서 | springdoc-openapi / Swagger UI |
| 배포 | GitHub Actions, pnpm, Docker, Docker Compose, AWS EC2 |

## 프로젝트 구조

```text
joribhaejo-web/
├── joribhaejo-next/           # Next.js 프론트엔드
│   ├── app/                 # 페이지·레이아웃
│   ├── components/          # 게시글·댓글·회원·쪽지 UI
│   ├── hooks/               # TanStack Query 기반 API 훅
│   └── lib/                 # API 클라이언트·타입·상수
├── joribhaejo-spring/        # Spring Boot 백엔드
│   └── src/main/
│       ├── java/com/example/joribhaejospring/
│       │   ├── user/        # 회원
│       │   ├── board/       # 게시판
│       │   ├── post/        # 게시글
│       │   ├── comment/     # 댓글
│       │   ├── like/        # 좋아요
│       │   ├── message/     # 쪽지
│       │   └── common/      # 인증·설정·예외 처리
│       └── resources/       # application.yml·schema.sql
└── .github/workflows/       # 빌드·배포 워크플로
```

## 로컬 실행

### 백엔드

JDK 17과 MySQL이 필요합니다. MySQL에 사용할 데이터베이스와 계정을 준비한 뒤, PowerShell에서 다음 환경변수를 설정합니다. 아래 값은 로컬 개발용 예시입니다.

```powershell
cd joribhaejo-spring
$env:DB_HOST = 'localhost'
$env:DB_PORT = '3306'
$env:DB_NAME = 'jorib_db'
$env:DB_USER = 'jorib_dml'
$env:DB_PASSWORD = 'your-local-db-password'
$env:JWT_SECRET = 'local-development-secret-key-at-least-32-bytes-long'
$env:JWT_ACCESS_EXP = '3600000'
$env:JWT_REFRESH_EXP = '604800000'
.\gradlew.bat bootRun
```

macOS·Linux에서는 같은 환경변수를 `export`로 설정하고 `./gradlew bootRun`을 실행합니다. 설정 항목은 [application.yml](joribhaejo-spring/src/main/resources/application.yml)에서 확인할 수 있습니다.

Hibernate의 `ddl-auto: update`로 테이블을 생성·갱신합니다. [schema.sql](joribhaejo-spring/src/main/resources/schema.sql)은 스키마 참고 파일이며 현재 설정에는 자동 실행이 지정되어 있지 않습니다. 게시판 초기 데이터도 별도로 준비해야 합니다. 프론트엔드의 최초 선택 게시판 ID는 `1`입니다.

| 항목 | 로컬 주소 |
| --- | --- |
| API 서버 | `http://localhost:8080` |
| Swagger UI | `http://localhost:8080/api/my-docs` |
| OpenAPI JSON | `http://localhost:8080/api/api-spec` |

### 프론트엔드

Next.js 15.2.4를 실행할 수 있는 Node.js 환경과 pnpm이 필요합니다. 저장소의 배포 워크플로는 pnpm을 사용합니다.

```bash
cd joribhaejo-next
pnpm install
pnpm dev
```

개발 서버는 기본적으로 `http://localhost:3000`에서 실행됩니다.

현재 [lib/api.ts](joribhaejo-next/lib/api.ts)의 `API_BASE_URL`은 `https://jorib.kthowns.cloud/api`로 고정되어 있습니다. 로컬 백엔드에 연결하려면 이 값을 `http://localhost:8080/api`로 수정해야 합니다. 환경변수 파일을 통한 API 주소 전환은 구현되어 있지 않습니다.

정적 파일을 빌드하려면 `pnpm build`를 실행합니다. [Next.js 설정](joribhaejo-next/next.config.mjs)의 `output: 'export'`에 따라 결과물은 `out/`에 생성됩니다. 현재 설정은 빌드 중 TypeScript·ESLint 오류를 무시하므로 빌드 성공이 타입·린트 검사 통과를 의미하지는 않습니다.

## API 안내

엔드포인트별 메서드와 요청 예시는 [REST API 명세서](docs/api.md)를 참고하세요.

| 영역 | 주요 경로 |
| --- | --- |
| 회원 | `/api/users/signup`, `/api/users/login`, `/api/users/me` |
| 게시판 | `/api/boards`, `/api/boards/{boardId}` |
| 게시글 | `/api/posts`, `/api/posts/{postId}` |
| 댓글 | `/api/posts/{postId}/comments`, `/api/comments/{postId}` (작성), `/api/comments/{commentId}` (수정·삭제) |
| 좋아요 | `/api/likes/{targetId}/posts`, `/api/likes/{targetId}/comments`, `/api/users/me/liked-post-ids` |
| 쪽지 | `/api/messages/inbox`, `/api/messages/sent`, `/api/messages/{messageId}`, `/api/messages/{receiverUsername}` (전송) |

인증이 필요한 요청에는 `Authorization: Bearer <accessToken>` 헤더를 사용합니다. HTTP 메서드와 상세 요청·응답은 서버 실행 후 Swagger UI에서 확인할 수 있습니다.

## 배포

`main` 브랜치에 push하면 [GitHub Actions 워크플로](.github/workflows/deploy-main.yml)가 다음 작업을 수행합니다.

1. Next.js를 정적 빌드합니다.
2. `out` 디렉터리를 Spring Boot의 정적 리소스 경로 아래로 복사합니다.
3. Spring Boot JAR와 Docker 이미지를 빌드하고 이미지를 푸시합니다.
4. SSH로 EC2에 접속해 Docker Compose로 배포합니다.

fork에서 사용하려면 `jorib-backend` GitHub Environment와 DB·JWT·Docker·EC2 관련 Secrets, 서버의 Docker Compose 구성을 별도로 준비해야 합니다. 현재 API 클라이언트에 지정된 배포 주소의 운영 여부는 확인하지 않았습니다.
