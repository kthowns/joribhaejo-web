# 🛠️ 조립해조 API 명세서 (v1.0.0)

커뮤니티 및 게시판 기능을 제공하는 **조립해조** 서비스의 REST API 명세서입니다.

---

## 🌐 서버 정보
* **배포 서버:** `https://jorib.kthowns.cloud`
* **로컬 서버:** `http://localhost:8080`

## 🔑 인증 방식
* **Access Token:** `Authorization` 헤더 사용 (Bearer 접두사 없이 JWT 토큰 원본 전송)

---

## 📂 API 요약

### 1. 사용자 서비스 (User)
| Method | Path | Summary | Details |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/users/signup` | 회원가입 | |
| `POST` | `/api/users/login` | 로그인 | AccessToken 발급 |
| `GET` | `/api/users/me` | 내 정보 조회 | 이메일, 사용자명 등 |

### 2. 게시판 및 게시글 서비스 (Board & Post)
| Method | Path | Summary | Details |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/boards` | 게시판 목록 조회 | |
| `POST` | `/api/boards` | 게시판 추가 | 테스트용 |
| `GET` | `/api/posts` | 게시글 목록 조회 | 검색, 페이징, 카테고리 필터링 지원 |
| `POST` | `/api/posts` | 게시글 작성 | 인증 필요 |
| `GET` | `/api/posts/{postId}` | 게시글 상세 조회 | |
| `PUT` | `/api/posts/{postId}` | 게시글 수정 | |
| `DELETE` | `/api/posts/{postId}` | 게시글 삭제 | |

### 3. 댓글 서비스 (Comment)
| Method | Path | Summary | Details |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/posts/{postId}/comments` | 댓글 목록 조회 | 특정 게시글의 전체 댓글 |
| `POST` | `/api/comments/{postId}` | 댓글 작성 | 대댓글(부모 ID) 지원 |
| `PUT` | `/api/comments/{commentId}` | 댓글 수정 | |
| `DELETE` | `/api/comments/{commentId}` | 댓글 삭제 | |

### 4. 쪽지 서비스 (Message)
| Method | Path | Summary | Details |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/messages/inbox` | 받은 쪽지함 조회 | |
| `GET` | `/api/messages/sent` | 보낸 쪽지함 조회 | |
| `POST` | `/api/messages/{receiverUsername}` | 쪽지 보내기 | 수신자 사용자명 기준 |
| `GET` | `/api/messages/{messageId}` | 쪽지 상세 조회 | |
| `DELETE` | `/api/messages/{messageId}` | 쪽지 삭제 | |

### 5. 좋아요 서비스 (Like)
| Method | Path | Summary | Details |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/likes/{targetId}/posts` | 게시글 좋아요 토글 | 클릭 시 좋아요/취소 |
| `POST` | `/api/likes/{targetId}/comments` | 댓글 좋아요 토글 | 클릭 시 좋아요/취소 |
| `GET` | `/api/users/me/liked-post-ids` | 내가 좋아한 게시글 ID 조회 | 리스트 형태 반환 |

---

## 📦 주요 데이터 모델 (DTO)

### 📝 PostCreateRequest (게시글 작성)
```json
{
  "boardId": 1,
  "title": "게시글 제목",
  "content": "게시글 내용",
  "category": "WEB" // WEB, MOBILE, BACK, HARD, AI, NETWORK, SECURITY, DEVOPS, ETC
}
