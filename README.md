# 📚 도서 관리 시스템 (Library Management System)

## 📋 프로젝트 개요

도서 관리 시스템은 도서관의 도서 대출/반납, 회원 관리, 도서 검색 등의 기능을 제공하는 웹 기반 애플리케이션입니다. 본 프로젝트는 동일한 백엔드 API를 사용하여 세 가지 다른 프론트엔드 기술로 구현되어, 각 기술의 특징과 장단점을 비교할 수 있도록 설계되었습니다.

### 🎯 프로젝트 목표
- 효율적인 도서 관리 시스템 구축
- 다양한 프론트엔드 기술 스택 비교 및 학습
- RESTful API 설계 및 구현
- 실무 수준의 프로젝트 경험 축적

## 🏗️ 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────────┐
│                     Frontend (3 Versions)                    │
├─────────────────┬──────────────────┬───────────────────────┤
│   Thymeleaf     │      JSP         │       React           │
│   (SSR)         │     (SSR)        │       (CSR)          │
└─────────────────┴──────────────────┴───────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    Backend (Spring Boot)                     │
├─────────────────────────────────────────────────────────────┤
│                      RESTful API Layer                       │
├─────────────────────────────────────────────────────────────┤
│                     Business Logic Layer                     │
├─────────────────────────────────────────────────────────────┤
│                  Data Access Layer (JPA)                     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    Database (MySQL)                          │
└─────────────────────────────────────────────────────────────┘
```

## 💻 기술 스택

### Backend
- **Framework**: Spring Boot 3.x
- **Language**: Java 17+
- **Build Tool**: Maven / Gradle
- **Database**: MySQL 8.0
- **ORM**: Spring Data JPA / Hibernate
- **Security**: Spring Security + JWT
- **API Documentation**: Swagger/OpenAPI 3.0
- **Testing**: JUnit 5, Mockito

### Frontend

#### 1. Thymeleaf 버전
- **Template Engine**: Thymeleaf 3.x
- **CSS Framework**: Bootstrap 5
- **JavaScript**: Vanilla JS / jQuery
- **특징**: 서버 사이드 렌더링, Spring Boot와의 완벽한 통합

#### 2. JSP 버전
- **View Technology**: JSP 2.3 + JSTL
- **CSS Framework**: Bootstrap 5
- **JavaScript**: jQuery
- **특징**: 전통적인 Java 웹 개발 방식, 레거시 시스템 이해

#### 3. React 버전
- **Framework**: React 18.x
- **State Management**: Redux Toolkit / Context API
- **Routing**: React Router 6
- **UI Library**: Material-UI / Ant Design
- **HTTP Client**: Axios
- **Build Tool**: Vite / Create React App
- **특징**: SPA, 컴포넌트 기반 개발, 현대적인 UI/UX

## 📊 데이터베이스 설계

### ERD (Entity Relationship Diagram)

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│    MEMBER    │     │     BOOK     │     │   CATEGORY   │
├──────────────┤     ├──────────────┤     ├──────────────┤
│ member_id PK │     │ book_id PK   │     │ category_id  │
│ email        │     │ isbn         │     │ name         │
│ password     │     │ title        │     │ description  │
│ name         │     │ author       │     └──────────────┘
│ phone        │     │ publisher    │            │
│ address      │     │ publish_date │            │ 1
│ join_date    │     │ category_id  │◄───────────┘
│ member_type  │     │ quantity     │            N
│ status       │     │ available    │
└──────────────┘     │ location     │
       │             │ description  │
       │             └──────────────┘
       │ 1                  │
       │                    │ N
       ▼ N                  ▼
┌──────────────────────────────┐
│          RENTAL              │
├──────────────────────────────┤
│ rental_id PK                 │
│ member_id FK                 │
│ book_id FK                   │
│ rental_date                  │
│ return_date                  │
│ actual_return_date           │
│ rental_status                │
│ overdue_fee                  │
└──────────────────────────────┘

┌──────────────┐     ┌──────────────┐
│  RESERVATION │     │    REVIEW    │
├──────────────┤     ├──────────────┤
│ reserve_id   │     │ review_id    │
│ member_id FK │     │ member_id FK │
│ book_id FK   │     │ book_id FK   │
│ reserve_date │     │ rating       │
│ status       │     │ comment      │
└──────────────┘     │ review_date  │
                     └──────────────┘
```

## 🔑 주요 기능

### 1. 회원 관리
- **회원가입/로그인**: 이메일 인증, 소셜 로그인 (OAuth2)
- **회원 정보 관리**: 프로필 수정, 비밀번호 변경
- **회원 등급**: 일반회원, 우수회원, VIP (대출 권수 차등)
- **관리자 기능**: 회원 목록 조회, 회원 상태 관리

### 2. 도서 관리
- **도서 등록/수정/삭제** (관리자)
- **도서 검색**: 제목, 저자, ISBN, 카테고리별 검색
- **도서 상세 정보**: 도서 정보, 리뷰, 평점
- **재고 관리**: 보유 수량, 대출 가능 수량 관리

### 3. 대출/반납 관리
- **도서 대출**: 대출 신청, 대출 가능 여부 확인
- **도서 반납**: 반납 처리, 연체료 계산
- **대출 연장**: 1회 7일 연장 가능
- **대출 이력**: 개인 대출 이력 조회

### 4. 예약 시스템
- **도서 예약**: 대출 중인 도서 예약
- **예약 알림**: 도서 반납 시 예약자에게 알림
- **예약 취소**: 예약 취소 기능

### 5. 리뷰 및 평점
- **리뷰 작성**: 대출 이력이 있는 도서만 작성 가능
- **평점 부여**: 5점 만점 별점 시스템
- **리뷰 관리**: 수정, 삭제 기능

### 6. 통계 및 리포트
- **대출 통계**: 월별, 카테고리별 대출 통계
- **인기 도서**: 대출 순위, 평점 순위
- **회원 통계**: 활성 회원, 연체 회원 통계

## 📁 프로젝트 구조

```
book_management_system/
├── README.md
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/library/
│   │   │   │       ├── controller/
│   │   │   │       ├── service/
│   │   │   │       ├── repository/
│   │   │   │       ├── entity/
│   │   │   │       ├── dto/
│   │   │   │       ├── config/
│   │   │   │       ├── security/
│   │   │   │       ├── exception/
│   │   │   │       └── util/
│   │   │   └── resources/
│   │   │       ├── application.yml
│   │   │       ├── application-dev.yml
│   │   │       └── application-prod.yml
│   │   └── test/
│   └── pom.xml / build.gradle
│
├── frontend-thymeleaf/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/library/
│   │   │   │       └── controller/
│   │   │   └── resources/
│   │   │       ├── templates/
│   │   │       │   ├── layout/
│   │   │       │   ├── member/
│   │   │       │   ├── book/
│   │   │       │   ├── rental/
│   │   │       │   └── admin/
│   │   │       └── static/
│   │   │           ├── css/
│   │   │           ├── js/
│   │   │           └── images/
│   └── pom.xml
│
├── frontend-jsp/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/library/
│   │   │   │       └── controller/
│   │   │   └── webapp/
│   │   │       ├── WEB-INF/
│   │   │       │   ├── views/
│   │   │       │   │   ├── layout/
│   │   │       │   │   ├── member/
│   │   │       │   │   ├── book/
│   │   │       │   │   └── rental/
│   │   │       │   └── web.xml
│   │   │       └── resources/
│   │   │           ├── css/
│   │   │           ├── js/
│   │   │           └── images/
│   └── pom.xml
│
├── frontend-react/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── common/
│   │   │   ├── layout/
│   │   │   ├── member/
│   │   │   ├── book/
│   │   │   └── rental/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── store/
│   │   ├── hooks/
│   │   ├── utils/
│   │   ├── styles/
│   │   ├── App.jsx
│   │   └── index.jsx
│   ├── package.json
│   └── vite.config.js
│
└── database/
    ├── schema.sql
    ├── init-data.sql
    └── stored-procedures.sql
```

## 🚀 설치 및 실행 가이드

### Prerequisites
- Java 17+
- Node.js 16+ (React 버전)
- MySQL 8.0+
- Maven 3.8+ or Gradle 7+

### 1. 데이터베이스 설정
```bash
# MySQL 접속
mysql -u root -p

# 데이터베이스 생성
CREATE DATABASE library_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# 사용자 생성 및 권한 부여
CREATE USER 'library_user'@'localhost' IDENTIFIED BY 'library_pass';
GRANT ALL PRIVILEGES ON library_db.* TO 'library_user'@'localhost';
FLUSH PRIVILEGES;

# 스키마 및 초기 데이터 적용
mysql -u library_user -p library_db < database/schema.sql
mysql -u library_user -p library_db < database/init-data.sql
```

### 2. Backend 실행
```bash
cd backend

# Maven 사용 시
mvn clean install
mvn spring-boot:run

# Gradle 사용 시
./gradlew clean build
./gradlew bootRun

# API 문서 확인: http://localhost:8080/swagger-ui.html
```

### 3. Frontend 실행

#### Thymeleaf 버전
```bash
cd frontend-thymeleaf
mvn spring-boot:run
# 접속: http://localhost:8081
```

#### JSP 버전
```bash
cd frontend-jsp
mvn spring-boot:run
# 접속: http://localhost:8082
```

#### React 버전
```bash
cd frontend-react
npm install
npm run dev
# 접속: http://localhost:3000
```

## 📝 API 명세

### 인증 API
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/signup` | 회원가입 |
| POST | `/api/auth/login` | 로그인 |
| POST | `/api/auth/logout` | 로그아웃 |
| POST | `/api/auth/refresh` | 토큰 갱신 |

### 회원 API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/members` | 회원 목록 조회 |
| GET | `/api/members/{id}` | 회원 상세 조회 |
| PUT | `/api/members/{id}` | 회원 정보 수정 |
| DELETE | `/api/members/{id}` | 회원 탈퇴 |

### 도서 API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/books` | 도서 목록 조회 |
| GET | `/api/books/{id}` | 도서 상세 조회 |
| POST | `/api/books` | 도서 등록 |
| PUT | `/api/books/{id}` | 도서 수정 |
| DELETE | `/api/books/{id}` | 도서 삭제 |
| GET | `/api/books/search` | 도서 검색 |

### 대출 API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/rentals` | 대출 목록 조회 |
| POST | `/api/rentals` | 대출 신청 |
| PUT | `/api/rentals/{id}/return` | 반납 처리 |
| PUT | `/api/rentals/{id}/extend` | 대출 연장 |
| GET | `/api/rentals/member/{memberId}` | 회원별 대출 이력 |

### 예약 API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/reservations` | 예약 목록 조회 |
| POST | `/api/reservations` | 도서 예약 |
| DELETE | `/api/reservations/{id}` | 예약 취소 |

### 리뷰 API
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/reviews/book/{bookId}` | 도서별 리뷰 조회 |
| POST | `/api/reviews` | 리뷰 작성 |
| PUT | `/api/reviews/{id}` | 리뷰 수정 |
| DELETE | `/api/reviews/{id}` | 리뷰 삭제 |

## 🔒 보안 고려사항

1. **인증/인가**
   - JWT 토큰 기반 인증
   - Role 기반 접근 제어 (ADMIN, USER)
   - Refresh Token 구현

2. **데이터 보안**
   - 비밀번호 암호화 (BCrypt)
   - SQL Injection 방지 (Prepared Statement)
   - XSS 방지 (입력값 검증 및 이스케이프)
   - CSRF 토큰 사용

3. **API 보안**
   - Rate Limiting
   - CORS 설정
   - HTTPS 적용

## 📈 성능 최적화

1. **데이터베이스**
   - 인덱싱 전략
   - 쿼리 최적화
   - 커넥션 풀 설정
   - 캐싱 (Redis)

2. **애플리케이션**
   - Lazy Loading
   - 페이지네이션
   - 비동기 처리
   - 이미지 최적화

3. **프론트엔드**
   - 코드 스플리팅 (React)
   - 번들 최적화
   - CDN 활용
   - 브라우저 캐싱

## 🧪 테스트 전략

1. **단위 테스트**
   - JUnit 5
   - Mockito
   - 80% 이상 코드 커버리지 목표

2. **통합 테스트**
   - Spring Boot Test
   - TestContainers (MySQL)
   - RestAssured

3. **프론트엔드 테스트**
   - Jest (React)
   - React Testing Library
   - Cypress (E2E)

## 📅 개발 로드맵

### Phase 1: 기본 기능 구현 (4주)
- [x] 프로젝트 설정 및 환경 구축
- [ ] 데이터베이스 설계 및 구현
- [ ] Backend API 개발
- [ ] 기본 CRUD 기능 구현

### Phase 2: Frontend 개발 (6주)
- [ ] Thymeleaf 버전 개발 (2주)
- [ ] JSP 버전 개발 (2주)
- [ ] React 버전 개발 (2주)

### Phase 3: 고급 기능 구현 (3주)
- [ ] 예약 시스템
- [ ] 리뷰 및 평점
- [ ] 통계 및 리포트
- [ ] 알림 기능

### Phase 4: 최적화 및 배포 (2주)
- [ ] 성능 최적화
- [ ] 보안 강화
- [ ] 테스트 및 버그 수정
- [ ] 배포 및 문서화

## 👥 팀 구성 및 역할

- **Project Manager**: 전체 프로젝트 관리
- **Backend Developer**: Spring Boot API 개발
- **Frontend Developer 1**: Thymeleaf/JSP 개발
- **Frontend Developer 2**: React 개발
- **Database Administrator**: DB 설계 및 최적화
- **DevOps Engineer**: CI/CD, 배포 환경 구축

## 📚 참고 자료

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [React Documentation](https://react.dev/)
- [Thymeleaf Documentation](https://www.thymeleaf.org/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [REST API Best Practices](https://restfulapi.net/)

## 📄 라이선스

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 문의사항

- Email: admin@library-system.com
- Issue Tracker: [GitHub Issues](https://github.com/yourusername/book_management_system/issues)

---
*Last Updated: 2024*