# Woori Chatbot Practice

네이버 CLOVA 챗봇 API를 연동해 간단한 채팅 UI에서 질의를 보내고, 응답의 `description` 안에 들어있는 JSON 문자열을 파싱해 `title`, `content`, `keywords` 형태로 반환하는 연습 프로젝트입니다.

---

## 프로젝트 실행 방법

### 로컬 실행

```bash
npm install
node chatServer.js
```

### 환경 변수 설정

`.env` 파일에 아래 값을 설정합니다.

```
CLOVA_CHATBOT_URL=발급받은_챗봇_API_URL
CLOVA_SECRET_KEY=발급받은_시크릿_키
```

### 접속

브라우저에서 `http://localhost:3000`으로 접속합니다.

---

## API Endpoint 안내

* **채팅 요청:** `POST http://localhost:3000/chat`
  - Request Body:
    ```json
    { "description": "사용자 질문" }
    ```
  - Response:
    ```json
    {
      "title": "제목",
      "content": "본문",
      "keywords": ["키워드1", "키워드2"]
    }
    ```

---

## 기능 요약

* CLOVA 챗봇 API 호출 및 서명 생성
* `bubbles[0].data.description`의 JSON 문자열 파싱
* 채팅 UI에서 메시지 전송 및 응답 렌더링
* 응답 `keywords` 기반 자동완성/클릭 입력

---

## 처리 흐름 (Task)

### Task 1: 사용자 질문 수집
* 프론트에서 `/chat`으로 `description`을 전송합니다.

### Task 2: 외부 API 호출
* 서버에서 CLOVA 챗봇 API로 요청을 보내고 응답을 받습니다.

### Task 3: 응답 파싱
* `description` 필드 안의 JSON 문자열을 파싱해 `title`, `content`, `keywords`를 추출합니다.

### Task 4: UI 렌더링 및 키워드 보조 입력
* 결과를 화면에 표시하고, `keywords`를 자동완성 후보로 제공합니다.

---

## 기술 스택

* **Backend:** Node.js, Express
* **HTTP Client:** superagent
* **Config:** dotenv
* **Frontend:** HTML, CSS, Vanilla JS
