# AppBoard API Docs

---

1. [AppBoard 객체](#AppBoard-객체)
2. [API 개요](#api-개요)
3. 엔드포인트
    - [게이트웨이 연결 테스트](#게이트웨이-연결-테스트)
    - QnA
      - [QnA 리스트](#qna-리스트)
      - [QnA 등록](#qna-등록)
      - [QnA 수정](#qna-수정)
      - [QnA 삭제](#qna-삭제)
      - [QnA 파일 등록](#qna-파일-등록)
      - [특정 QnA 조회](#qna-상세정보-조회)
    - Notice
      - [Notice 상세정보 조회](#Notice-상세정보-조회)
      - [Notice 리스트](#Notice-리스트)
4. [에러 코드](#에러-코드)
    - [Status Code](#status-code)
    - [CustomErrorCode](#customerrorcode)
5. [자주 묻는 질문](#자주-묻는-질문)

---
## API 개요

**Base URL:**
- `https://api.aiapp.link/aiapp`

**Base Header**
- Authorization-Key : `{API Key}`

**Authentication:**
- Authorization : `Bearer Token`

---
## AppBoard 객체

### Response 객체 상세
- **result**
    - **`SUCCESS`**: 요청의 결과 성공을 나타냅니다.
    - **`FAIL`**: 요청에 문제가 있어 실패했음을 나타냅니다.
- **data**: 요청 결과에 대한 데이터를 포함합니다. 예) `data.appCode`
- **message**: 요청의 결과에 추가 메시지나 실패 시 `CustomErrorCode`의 내용을 응답합니다.
- **errorCode**: 발생한 예외의 `CustomErrorCode`를 응답합니다.
- **error** : `API Key` 관련 예외 발생시 응답합니다.
    - `Missing Key` : RequestHeader 에서 `Authorization-Key` 를 추가해주세요.
    - `Method not allowed` : `API Key` 가 올바르지 않습니다.

### Page 객체 상세
- **next**
    - **타입**: `Boolean`
    - **설명**: 다음 페이지 여부.
- **prev**
    - **타입**: `Boolean`
    - **설명**: 이전 페이지 여부.
- **nowPage**
    - **타입**: `Integer`
    - **설명**: 현재 페이지 번호.
- **totalPage**
    - **타입**: `Integer`
    - **설명**: 전체 페이지 수.
- **totalCount**
    - **타입**: `Integer`
    - **설명**: 전체 문의 수.

### QnA 객체 상세
- **typeList**
  - **타입**: `List`
  - **설명**: 문의 유형 리스트.

      - **value**
          - **타입**: `Enum`
          - **설명**: 문의 유형 코드.
      - **name**
          - **타입**: `String`
          - **설명**: 문의 유형의 이름.
- **qnaList**
  - **타입**: `List`
  - **설명**: 문의 리스트.

      - **qnaCode**
          - **타입**: `String`
          - **설명**: 문의 코드.
      - **title**
          - **타입**: `String`
          - **설명**: 문의 제목.
      - **content**
          - **타입**: `String`
          - **설명**: 문의 내용.
      - **createBy**
          - **타입**: `String`
          - **설명**: 작성자 ID.
      - **type**
          - **타입**: `Enum`
          - **설명**: 문의 유형 객체.
          - **type.value**
              - **타입**: `Enum`
              - **설명**: 문의 유형 코드.
          - **type.name**
              - **타입**: `String`
              - **설명**: 문의 유형의 이름.
      - **name**
          - **타입**: `String`
          - **설명**: 작성자 이름.
      - **answer**
          - **타입**: `Boolean`
          - **설명**: 답변 여부.
      - **createAt**
          - **타입**: `LocalDate`
          - **설명**: 생성 일자.
      - **fileId**
          - **타입**: `String`
          - **설명**: 파일 그룹 ID.
      - **fileUrl**
          - **타입**: `List`
          - **설명**: 파일 URL 리스트.
          - **fileUrl[]**
              - **타입**: `String`
              - **설명**: 파일 URL 개별 항목.
### Notice 객체 상세

- **sequence**
  - **타입**: `Integer`
  - **설명**: 공지사항 순서.

- **noticeCode**
  - **타입**: `String`
  - **설명**: 공지사항 코드.

- **title**
  - **타입**: `String`
  - **설명**: 공지사항 제목.

- **content**
  - **타입**: `String`
  - **설명**: 공지사항 내용 (HTML).

- **startDate**
  - **타입**: `LocalDate`
  - **설명**: 공지 시작일.

- **fileId**
  - **타입**: `String`
  - **설명**: 파일 ID (null일 수 있음).

- **fileUrl**
  - **타입**: `List`
  - **설명**: 파일 URL 리스트.
      - **fileUrl[]**
          - **타입**: `String`
          - **설명**: 파일 URL 개별 항목.

- **prevContent**
  - **타입**: `Object`
  - **설명**: 이전 공지사항 내용 객체 (`nullable`).
      - **prevContent.sequence**
          - **타입**: `Integer`
          - **설명**: 이전 공지사항 순서.
      - **prevContent.noticeCode**
          - **타입**: `String`
          - **설명**: 이전 공지사항 코드.
      - **prevContent.noticeTitle**
          - **타입**: `String`
          - **설명**: 이전 공지사항 제목.
      - **prevContent.createAt**
          - **타입**: `Date`
          - **설명**: 이전 공지사항 생성 일자.
      - **prevContent.noticeStartDate**
          - **타입**: `Date`
          - **설명**: 이전 공지사항 시작일.
- **nextContent**
  - **타입**: `Object`
  - **설명**: 다음 공지사항 내용 객체 (`nullable`).
---

## 엔드포인트


### 게이트웨이 연결 테스트

- **URL:** `/app/health`
- **Method:** `GET`
- **Description:** 게이트웨이를 통한 연결을 확인합니다.

**Example:**

```bash
curl --request GET \
      --url 'https://api.aiapp.link/aiapp/app/health' \
      --header 'Authorization-Key: {API Key}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게이트 웨이 상태 양호
```json
{"result": "SUCCESS", "message": "app-service OK"}
```
---

### QnA 리스트

- **URL:** `/app-board/member/qna`
- **Method:** `GET`
- **Description:** 앱유저 QnA 리스트 출력.


**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**Example:**

```bash
curl --request GET \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 해당 회원이 문의한 QnA 리스트를 가져옵니다.

```json
{
  "result": "SUCCESS",
  "data": {
    "typeList": [
      {
        "value": "TRADE",
        "name": "거래문의"
      },
      {
        "value": "USE",
        "name": "이용문의"
      },
      {
        "value": "PAY_REFUND",
        "name": "결제/환불"
      },
      {
        "value": "SERVICE",
        "name": "서비스 관련"
      },
      {
        "value": "ACCOUNT",
        "name": "회원/계정"
      },
      {
        "value": "SERVICE_ROLE",
        "name": "운영정책"
      },
      {
        "value": "OTHER",
        "name": "기타"
      }
    ],
    "next": false,
    "prev": false,
    "nowPage": 0,
    "totalPage": 1,
    "totalCount": 3,
    "qnaList": [
      {
        "qnaCode": "qna_NGKNLEkNAqXuXnfC",
        "title": "제목",
        "content": "내용",
        "createBy": "app_mbr_duuuum",
        "type": {
          "value": "TRADE",
          "name": "거래문의"
        },
        "name": "더모",
        "answer": false,
        "createAt": "2024-07-05"
      }
    ]
  },
  "message": null,
  "errorCode": null
}
```
**Response Fields**

- **typeList (문의 유형 리스트)**

    | Name           | Description  |
    |----------------|--------------|
    | value `Enum`   | 문의 유형        |
    | name  `String` | 문의 유형의 value |

- **페이지 정보**
    
    | Name                 | Description |
    |----------------------|-------------|
    | next       `Boolean` | 다음 페이지 여부   |
    | prev       `Boolean` | 이전 페이지 여부   |
    | nowPage    `Integer` | 현재 페이지 번호   |
    | totalPage  `Integer` | 전체 페이지 수    |
    | totalCount `Integer` | 전체 문의 수     |

- **qnaList (문의 리스트)**

  | Name               | Description  |
  |--------------------|--------------|
  | qnaCode `String`   | 문의 코드        |
  | title `String`     | 문의 제목        |
  | content `String`   | 문의 내용        |
  | createBy `String`  | 작성자 ID       |
  | type `Enum`        | 문의 유형 객체     |
  | type.value `Enum`  | 문의 유형 코드     |
  | type.name `String` | 문의 유형의 이름    |
  | name `String`      | 작성자 이름       |
  | answer `Boolean`   | 답변 여부        |
  | createAt `Date`    | 생성 일자        |
  | fileId `String`    | 파일 그룹 ID     |
  | fileUrl `List`     | 파일 URL 리스트   |
  | fileUrl[] `String` | 파일 URL 개별 항목 |

- **type `Enum` Values**
    
    | Name           | Value    | Description  |
    |----------------|----------|--------------|
    | `TRADE`        | `거래문의`   | 거래문의 유형입니다.  |
    | `USE`          | `이용문의`   | 이용문의 유형입니다.  |
    | `PAY_REFUND`   | `결제/환불`  | 결제/환불 유형입니다. |
    | `SERVICE`      | `서비스 관련` | 서비스 유형입니다.   |
    | `ACCOUNT`      | `회원/계정`  | 회원/계정 유형입니다. |
    | `SERVICE_ROLE` | `운영정책`   | 운영정책 유형입니다.  |
    | `OTHER`        | `기타`     | 기타 유형입니다.    |


---

### QnA 등록

- **URL:** `/app-board/member/qna`
- **Method:** `POST`
- **Description:** QnA을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key          |

**Request Body:**

```json
{
  "title": "제목",
  "content": "내용",
  "type": {
    "value": "TRADE",
    "name": "거래문의",
    "type": "TRADE"
  },
  "fileId": ""
}
```
**RequestFields**

| Name               | Required | Description        |
|--------------------|----------|--------------------|
| title `String`     | `True`   | 문의사항의 제목입니다.       |
| content `String`   | `True`   | QnA 내용입니다.         |
| type.value `Enum`  | `True`   | 문의 유형의 `Enum` 입니다. |
| type.name `String` | `True`   | 문의 유형의 value 입니다.  |
| type.type `Enum`   | `True`   | 문의 유형의 `Enum` 입니다. |
| fileId `String`    | `True`   | App 의 고유 Code 입니다. |

**type Enum Values**

| Name           | Value    | Description  |
|----------------|----------|--------------|
| `TRADE`        | `거래문의`   | 거래문의 유형입니다.  |
| `USE`          | `이용문의`   | 이용문의 유형입니다.  |
| `PAY_REFUND`   | `결제/환불`  | 결제/환불 유형입니다. |
| `SERVICE`      | `서비스 관련` | 서비스 유형입니다.   |
| `ACCOUNT`      | `회원/계정`  | 회원/계정 유형입니다. |
| `SERVICE_ROLE` | `운영정책`   | 운영정책 유형입니다.  |
| `OTHER`        | `기타`     | 기타 유형입니다.    |


**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna' \
      --header 'Authorization-key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                  "title": "제목",
                  "content": "내용",
                  "type": {
                    "value": "TRADE",
                    "name": "거래문의",
                    "type": "TRADE"
                  },
                  "fileId": ""
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** QnA 등록.
```json
{
  "result": "SUCCESS",
  "data": "qnaCode",
  "message": null,
  "errorCode": null
}
```

---

### QnA 수정

- **URL:** `/app-board/member/qna`
- **Method:** `PUT`
- **Description:** QnA을 수정합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key          |



**Request Body:**

```json
{
  "qnaCode": "qna_NGKNLEkNAqXuXnfC",
  "title": "제목수정",
  "content": "내용수정",
  "type": {
    "value": "TRADE",
    "name": "거래문의",
    "type": "TRADE"
  },
  "fileId": ""
}
```
**RequestFields**

| Name               | Required | Description        |
|--------------------|----------|--------------------|
| qnaCode `String`   | `True`   | 수정할 QnA 코드입니다.     |
| title `String`     | `True`   | 문의사항의 제목입니다.       |
| content `String`   | `True`   | QnA 내용입니다.         |
| type.value `Enum`  | `True`   | 문의 유형의 `Enum` 입니다. |
| type.name `String` | `True`   | 문의 유형의 value 입니다.  |
| type.type `Enum`   | `True`   | 문의 유형의 `Enum` 입니다. |
| fileId `String`    | `True`   | App 의 고유 Code 입니다. |

**type `Enum` Values**

| Name           | Value    | Description  |
|----------------|----------|--------------|
| `TRADE`        | `거래문의`   | 거래문의 유형입니다.  |
| `USE`          | `이용문의`   | 이용문의 유형입니다.  |
| `PAY_REFUND`   | `결제/환불`  | 결제/환불 유형입니다. |
| `SERVICE`      | `서비스 관련` | 서비스 유형입니다.   |
| `ACCOUNT`      | `회원/계정`  | 회원/계정 유형입니다. |
| `SERVICE_ROLE` | `운영정책`   | 운영정책 유형입니다.  |
| `OTHER`        | `기타`     | 기타 유형입니다.    |


**Example:**

```bash
curl --request 'PUT' \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna' \
      --header 'Authorization-key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "qnaCode": "qna_NGKNLEkNAqXuXnfC",
                  "title": "제목",
                  "content": "내용",
                  "type": {
                    "value": "TRADE",
                    "name": "거래문의",
                    "type": "TRADE"
                  },
                  "fileId": ""
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** QnA 수정완료.
```json
{
  "result": "SUCCESS",
  "data": "qnaCode",
  "message": null,
  "errorCode": null
}
```
---
### QnA 삭제

- **URL:** `/app-board/member/qna`
- **Method:** `DELETE`
- **Description:** QnA을 삭제합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key          |

**Request Body:**

```json
{
  "qnaCodeList": [
    "qna_NGKNLEkNAqXuXnfC"
  ]
}
```
**RequestFields**

| Name                   | Required | Description     |
|------------------------|----------|-----------------|
| qnaCodeList   `List`   | `True`   | QnA 코드 리스트 입니다. |
| qnaCodeList[] `String` | `True`   | QnA 개별코드 입력합니다. |


**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna' \
      --header 'Authorization: Bearer {token}' \
      --header 'Authorization-key: {API Key}' \
      --header 'Content-Type: application/json' \
      --data '{
                  "qnaCodeList": [
                      "qna_NGKNLEkNAqXuXnfC"
                  ]
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** QnA을 삭제함.
```json
{
  "result": "SUCCESS",
  "data": [
    "qna_NGKNLEkNAqXuXnfC"
  ],
  "message": null,
  "errorCode": null
}
```
---
### QnA 파일 등록

- **URL:** `/app-board/member/qna/file`
- **Method:** `POST`
- **Description:** QnA에 파일을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key          |

**Request Body:**

```json
{
  "qnaCode": "qna_NGKNLEkNAqXuXnfC",
  "fileId": "FLE_2408"
}
```
**RequestFields**

| Name             | Required | Description    |
|------------------|----------|----------------|
| qnaCode `String` | `True`   | QnA 코드 입니다.    |
| fileId `String`  | `True`   | 파일 그룹 아이디 입니다. |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna/file' \
      --header 'Authorization-key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "qnaCode": "qna_NGKNLEkNAqXuXnfC",
                "fileId": "FLE_2408"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** QnA에 파일을 등록합니다..
```json
{
  "result": "SUCCESS",
  "data": "FLE_2408",
  "message": null,
  "errorCode": null
}
```
---
### QnA 상세정보 조회

- **URL:** `/app-board/member/qna/{qnaCode}`
- **Method:** `GET`
- **Description:** QnA 코드로 QnA을 조회합니다.

**RequestHeader**

| Name                | Description    |
|---------------------|----------------|
| `Authorization`     | 로그인 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key      |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| qnaCode   | `True`   | QnA 코드.     |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna/{qnaCode}' \
      --header 'Authorization-key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 특정 QnA 조회.
```json
{
  "result": "SUCCESS",
  "data": {
    "qnaCode": "qna_NGKNLEkNAqXuXnfC",
    "title": "제목수정",
    "content": "내용수정",
    "createBy": "app_mbr_duuuum",
    "type": {
      "value": "TRADE",
      "name": "거래문의"
    },
    "name": "더모",
    "answer": false,
    "createAt": "2024-07-05",
    "fileId": "FLE_2408",
    "fileUrl": [
      "https://file.mbaas.kr/assets/20240703/c5267f1e-c6e7-495b-b0ca-ef9039f0aa07.png"
    ]
  },
  "message": null,
  "errorCode": null
}
```
**ResponseFields**

| Name                 | Description    |
|----------------------|----------------|
| qnaCode `String`     | 문의 코드          |
| title `String`       | 문의 제목          |
| content `String`     | 문의 내용          |
| createBy `String`    | 작성자 ID         |
| type `Enum`          | 문의 유형 객체       |
| type.value `Enum`    | 문의 유형의 `Enum`  |
| type.name `String`   | 문의 유형의 `value` |
| name `String`        | 작성자 이름         |
| answer `Boolean`     | 답변 여부          |
| createAt `LocalDate` | 생성 일자          |
| fileId `String`      | 파일 그룹 ID       |
| fileUrl `List`       | 파일 URL 리스트     |
| fileUrl[] `String`   | 파일 URL 개별 항목   |

---

# CustomApp

---


### Notice 상세정보 조회

- **URL:** `/app-board/member/notice/{noticeCode}`
- **Method:** `GET`
- **Description:** 공지사항 코드로 공지사항을 조회합니다.

**RequestHeader**

| Name                | Description    |
|---------------------|----------------|
| `Authorization`     | 로그인 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key      |

**QueryParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| appCode   | `True`   | App 고유 코드.  |

**PathParameters**

| Parameter  | Required | Description |
|------------|----------|-------------|
| noticeCode | `True`   | 공지사항 코드.    |

**Example:**

```bash
curl --request GET \
      --url 'https://api.aiapp.link/aiapp/app-board/member/notice/{noticeCode}?appCode={appCode}' \
      --header 'Authorization-key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** QnA 상세정보 조회.
```json
{
  "result": "SUCCESS",
  "data": {
    "sequence": 206,
    "noticeCode": "ntc_aJOLdqjoEYewluTZ",
    "title": "공지사항",
    "content": "<p>1123</p>",
    "startDate": "2024-05-29",
    "fileId": null,
    "fileUrl": [],
    "prevContent": {
      "sequence": 205,
      "noticeCode": "ntc_yCiXTDGFZBIbtLJZ",
      "noticeTitle": "이전 컨텐츠",
      "createAt": "2024-05-23",
      "noticeStartDate": "2024-05-30"
    },
    "nextContent": null
  },
  "message": null,
  "errorCode": null
}
```
**ResponseFields**

| Name                                    | Description    |
|-----------------------------------------|----------------|
| sequence `Integer`                      | 공지사항 순서        |
| noticeCode `String`                     | 공지사항 코드        |
| title `String`                          | 공지사항 제목        |
| content `String`                        | 공지사항 내용 (HTML) |
| startDate `Date`                        | 공지 시작일         |
| fileId `String` `nullable`              | 파일 ID          |
| fileUrl `List`                          | 파일 URL 리스트     |
| fileUrl[] `String`                      | 파일 URL 개별 항목   |
| prevContent `Object` `nullable`         | 이전 공지사항 내용 객체  |
| prevContent.sequence `Integer`          | 이전 공지사항 순서     |
| prevContent.noticeCode `String`         | 이전 공지사항 코드     |
| prevContent.noticeTitle `String`        | 이전 공지사항 제목     |
| prevContent.createAt `LocalDate`        | 이전 공지사항 생성 일자  |
| prevContent.noticeStartDate `LocalDate` | 이전 공지사항 시작일    |
| nextContent `Object` `nullable`         | 다음 공지사항 내용 객체  |


---

### Notice 리스트

- **URL:** `/app-board/member/notice`
- **Method:** `GET`
- **Description:** 공지사항 리스트 출력.


**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | 앱 엑세스 key          |

**Example:**

```bash
curl --request GET \
      --url 'https://api.aiapp.link/aiapp/app-board/member/qna' \
      --header 'Authorization-key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json'
```
**Responses Body:**

- **Status Code:** `200`
- **Description:** 해당 회원이 문의한 QnA 리스트를 가져옵니다.

```json
{
  "result": "SUCCESS",
  "data": {
    "next": true,
    "prev": false,
    "nowPage": 0,
    "totalPage": 5,
    "totalCount": 48,
    "noticeList": [
      {
        "sequence": 206,
        "noticeCode": "ntc_aJOLdqjoEYewluTZ",
        "noticeTitle": "공지사항",
        "createAt": "2024-05-29",
        "noticeStartDate": "2024-05-29"
      }
    ]
  },
  "message": null,
  "errorCode": null
}
```
**Response Fields**

- **페이지 정보**

    | Name                   | Description |
    |------------------------|-------------|
    | next `Boolean`         | 다음 페이지 여부   |
    | prev `Boolean`         | 이전 페이지 여부   |
    | nowPage `Integer`      | 현재 페이지 번호   |
    | totalPage `Integer`    | 전체 페이지 수    |
    | totalCount `Integer`   | 전체 공지사항 수   |

- **noticeList (문의 리스트)**

    | Name                        | Description |
    |-----------------------------|-------------|
    | sequence `Integer`          | 공지사항 순서     |
    | noticeCode `String`         | 공지사항 코드     |
    | noticeTitle `String`        | 공지사항 제목     |
    | createAt `LocalDate`        | 공지사항 작성일    |
    | noticeStartDate `LocalDate` | 공지사항 시작일    |


---

## 에러 코드
### Status Code

| Status Code | Description           |
|-------------|-----------------------|
| `400`       | Bad Request           |
| `401`       | Unauthorized          |
| `403`       | Forbidden             |
| `404`       | Not Found             |
| `500`       | Internal Server Error |

### CustomErrorCode

| Error Code                 | Status Code | Description                      |
|----------------------------|-------------|----------------------------------|
| `COMMON_INVALID_PARAMETER` | `200`       | 요청한 값이 올바르지 않습니다.                |
| `COMMON_ILLEGAL_STATUS`    | `200`       | 잘못된 상태값입니다.                      |
| `COMMON_UPDATE`            | `200`       | 수정이 불가능 합니다.                     |
| `COMMON_FORBIDDEN`         | `403`       | 유저 요청 권한이 없습니다.                  |
| `COMMON_SYSTEM_ERROR`      | `500`       | 일시적인 오류가 발생했습니다. 잠시 후 다시 시도해주세요. |


## 자주 묻는 질문

### Q: 인증은 어떻게 하나요?
A: `Authorization` 헤더에 Bearer 토큰을 보내야 합니다.  
A: `Authorization-Key` 헤더에 앱 엑세스 키를 보내야 합니다.
### Q: 요청 본문은 어떤 형식이어야 하나요?
A: 이미지 업로드를 제외한 모든 요청 본문은 `JSON` 형식이어야 합니다.
