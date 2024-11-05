# SsamMuTalk

## 설명

NEXON Open API를 활용한, 메이플스토리 캐릭터 기반의 오픈 채팅 서비스

## 기능

- API Key를 통한 로그인
- 캐릭터 선택
- 채팅

## 기술스택

- Language: TypeScript
- BE: Nest.js
- FE: React
- DB: MySQL, MongoDB
- IDE: Cursor
- Infra: OCI(예정)

## 화면

### 로그인

![login](https://github.com/user-attachments/assets/81fbab07-bcf0-427f-a8a1-7fb0db074daf)

#### API Key 발급 받기(Notion)

![docs](https://github.com/user-attachments/assets/18bd8fad-7fab-48f4-ae89-3a7cdb5af71a)

### 캐릭터 선택

![choose](https://github.com/user-attachments/assets/390403da-ee5a-4f19-ae58-521e736422b9)

### 채팅

`구현중`

## 구현 요소

### `Promise.all()`을 활용한 API 호출 성능 향상

- 최초 상황: 싱글 스레드 + 동기 방식의 순차적 API 호출을 40건 이상 실행 -> 평균 `5.42s` 소요
- 분석
  - 서비스 API 기준 `초당 최대 허용량 500건 / 초`
  - 메이플스토리 유니온은 최대 42개의 캐릭터만 적용
  - 특정 chunk 단위로 병렬 처리를 하면 성능 향상이 가능할 것
- 시도
  - JavaScript V8 Engine은 싱글 스레드 -> Event Loop를 통한 비동기식 병렬 처리
  - `Promise.all()`: 동시에 여러 요청을 보내고 결과를 병렬적으로 처리할 수 있는 방식
- 결과
  - 동일 로직 수행 결과 평균 `0.33s` 소요 -> 기존 코드 대비 **16.1배의 성능 향상**

### `sessionStorage`를 이용한 캐싱을 통해 렌더링 성능 향상

- sessionStorage는 페이지 세션이 종료되면 제거되는 웹 스토리지 객체
- sessionStorage에 캐릭터 정보를 저장하였고, 저장된 캐릭터 정보가 있다면 API 호출 대신 저장된 정보 활용
- 단, 이미지 캐싱의 경우 추가로 고려해야 할 요소

### `Cursor IDE`를 활용한 frontend 생산성 극대화

- 스크립트 작성 후, 제공받은 코드에 대한 수정
  - 여기서 기존 과정에 비해 압도적인 시간 절약 경험
- 이후, 세부적인 내용은 직접 개발 및 수정

## 기간

- BE: 2024-08-21 ~ 2024-08-28
- FE: 2024-11-05 ~ 
