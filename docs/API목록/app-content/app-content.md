# AppContent API Docs

---

1. [API 개요](#api-개요)
2. [AppContent 객체](#AppContent-객체)
3. 엔드포인트
   - [게이트웨이 연결 테스트](#게이트웨이-연결-테스트)
   - Basic App
     - [App에 등록된 Contents 리스트 가져오기](#app에-등록된-contents-리스트-가져오기)
      - 알림
        - [App 회원 알림](#app-회원-알림)
        - [App 회원 알림 수동 처리](#app-회원-알림-수동-처리)
      - 일정관리
        - [일정 리스트 가져오기](#일정-리스트-가져오기)
        - [일정 상세내용 조회하기](#일정-상세내용-조회하기)
      - 게시판
        - [게시물 리스트 가져오기](#게시물-리스트-가져오기-V2)
        - [게시물 저장하기](#게시물-저장하기-V2)
        - [게시물 수정하기](#게시물-수정하기-V2)
        - [게시물 삭제하기](#게시물-삭제하기-V2)
        - [게시물 좋아요 등록하기](#게시물-좋아요-등록하기-v2)
        - [게시물 좋아요 취소하기](#게시물-좋아요-취소하기-v2)
        - [게시물 북마크 등록하기](#게시물-북마크-등록하기-v2)
        - [게시물 북마크 취소하기](#게시물-북마크-취소하기-v2)
        - [게시물 상세정보](#게시물-상세정보-v2)
        - [게시물 북마크 리스트](#게시물-북마크-리스트-V2)
        - [댓글 저장하기](#댓글-저장하기-v2)
        - [댓글 수정하기](#댓글-수정하기-v2)
        - [댓글 삭제하기](#댓글-삭제하기-v2)
   - Custom App
     -  원데이 클래스
         - [클래스 리스트 가져오기](#강의-리스트-가져오기)
     - 테이크 아웃
             - [Item 리스트 조회](#item-리스트-조회)
             - [Item 조회](#item-조회)
             - [Item 북마크 등록](#item-북마크-등록)
             - [Item 북마크 제거](#item-북마크-제거)
     - 커뮤니티
         - [게시글 등록](#게시글-등록)
         - [게시물 상세 내용 조회](#게시물-상세-내용-조회)
         - [게시글 좋아요 등록](#게시글-좋아요-등록)
         - [게시글 좋아요 취소](#게시글-좋아요-취소)
         - [게시글 북마크 등록](#게시글-북마크-등록)
         - [게시글 북마크 취소](#게시글-북마크-취소)
         - [게시글 댓글 등록](#게시글-댓글-등록)

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
## AppContent 객체

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

### App 회원 알림 객체 상세

- **clientCode**
    - **타입**: `String`
    - **설명**: App 회원 코드.
- **summary**
    - **타입**: `String`
    - **설명**: 내용 요약.
- **redirect**
    - **타입**: `String`
    - **설명**: 해당 컨텐츠 이동 URL.
- **relationCode**
    - **타입**: `String`
    - **설명**: 알림이 발송될 컨텐츠 코드 (ex. client 와 연관된 컨텐츠 코드).
- **type**
    - **타입**: `Enum`
    - **설명**: 컨텐츠 알림 타입.
- **read**
    - **타입**: `Boolean`
    - **설명**: 알림 읽음 여부.
- **createAt**
    - **타입**: `String`
    - **설명**: 알림 생성일자.

### 원데이 클래스 객체 상세

- **code**
    - **타입**: `String`
    - **설명**: 항목 코드.
- **name**
    - **타입**: `String`
    - **설명**: 항목 이름.
- **capabilityInfo**
    - **타입**: `List`
    - **설명**: 항목의 기능 정보.
        - **capabilityInfo[]**
            - **타입**: `Enum`
            - **설명**: 항목의 기능 정보 개별 항목.
- **fileInfo**
    - **타입**: `Object`
    - **설명**: 파일 정보.
        - **fileInfo.fileId**
            - **타입**: `String`
            - **설명**: 파일 ID.
        - **fileInfo.fileUrl**
            - **타입**: `String`
            - **설명**: 파일 URL.
        - **fileInfo.fileName**
            - **타입**: `String`
            - **설명**: 파일 이름.
        - **fileInfo.fileType**
            - **타입**: `String`
            - **설명**: 파일 유형.
- **sequence**
    - **타입**: `Integer`
    - **설명**: 항목 순서.
- **createAt**
    - **타입**: `String`
    - **설명**: 항목 생성 시각 (ISO 8601 형식).
- **groupList**
    - **타입**: `List`
    - **설명**: 그룹 목록.
        - **groupList[]**
            - **타입**: `Object`
            - **설명**: 그룹 목록 개별 항목.
                - **groupList.idx**
                    - **타입**: `Integer`
                    - **설명**: 그룹 인덱스.
                - **groupList.groupCode**
                    - **타입**: `String`
                    - **설명**: 그룹 코드.
                - **groupList.groupName**
                    - **타입**: `String`
                    - **설명**: 그룹 이름.
- **status**
    - **타입**: `String`
    - **설명**: 항목 상태.

### Item 객체 상세

- **code**
    - **타입**: `String`
    - **설명**: Item 코드.
- **appCode**
    - **타입**: `String`
    - **설명**: App 코드.
- **partnerCode**
    - **타입**: `String`
    - **설명**: App 관리자 회원 코드.
- **name**
    - **타입**: `String`
    - **설명**: Item 이름.
- **content**
    - **타입**: `String`
    - **설명**: Item 내용.
- **price**
    - **타입**: `Integer`
    - **설명**: Item 가격.
- **hits**
    - **타입**: `Integer`
    - **설명**: 조회수.
- **fileId**
    - **타입**: `String`
    - **설명**: Item 이미지 파일 그룹 ID.
- **fileInfoList**
    - **타입**: `List`
    - **설명**: 파일 정보 목록.
        - **fileInfoList[]**
            - **타입**: `Object`
            - **설명**: 파일 정보 개별 항목.
                - **fileInfoList.fileId**
                    - **타입**: `String`
                    - **설명**: 파일 ID.
                - **fileInfoList.fileUrl**
                    - **타입**: `String`
                    - **설명**: 파일 URL.
                - **fileInfoList.fileName**
                    - **타입**: `String`
                    - **설명**: 파일 이름.
                - **fileInfoList.fileType**
                    - **타입**: `String`
                    - **설명**: 파일 유형.
- **favorites**
    - **타입**: `Integer`
    - **설명**: 좋아요 수.
- **status**
    - **타입**: `String`
    - **설명**: 항목 상태.

### 일정관리 객체 상세

- **code**
    - **타입**: `String`
    - **설명**: 일정 코드.
- **content**
    - **타입**: `String`
    - **설명**: 일정 내용.
- **title**
    - **타입**: `String`
    - **설명**: 일정 제목.
- **start**
    - **타입**: `String`
    - **설명**: 시작 일시 (YYYY.MM.DD. HH:mm 형식).
- **end**
    - **타입**: `String`
    - **설명**: 종료 일시 (YYYY.MM.DD. HH:mm 형식).

### Content 객체 상세

- **code**
    - **타입**: `String`
    - **설명**: 컨텐츠 코드.
- **name**
    - **타입**: `String`
    - **설명**: 컨텐츠 이름.
- **status**
    - **타입**: `String`
    - **설명**: 컨텐츠 사용 상태.
- **fileInfo**
    - **타입**: `Object`
    - **설명**: 컨텐츠 로고 정보.
        - **fileInfo.fileId**
            - **타입**: `String`
            - **설명**: 파일 ID.
        - **fileInfo.fileUrl**
            - **타입**: `String`
            - **설명**: 파일 URL.
        - **fileInfo.fileName**
            - **타입**: `String`
            - **설명**: 파일 이름.
        - **fileInfo.fileType**
            - **타입**: `String`
            - **설명**: 파일 유형.
- **sequence**
    - **타입**: `Integer`
    - **설명**: 컨텐츠 순서.
- **capabilityInfo**
    - **타입**: `List`
    - **설명**: 기능 정보 리스트.
        - **capabilityInfo[]**
            - **타입**: `Enum`
            - **설명**: 컨텐츠 유형 정보.

### 게시글 객체 상세

- **title**
    - **타입**: `String`
    - **설명**: 제목.
- **content**
    - **타입**: `String`
    - **설명**: 내용.
- **image**
    - **타입**: `String`
    - **설명**: 이미지 파일 ID.
- **download**
    - **타입**: `String`
    - **설명**: 다운로드 링크.
- **videoLink**
    - **타입**: `String`
    - **설명**: 비디오 링크 URL.

### 댓글 객체 상세

- **code**
    - **타입**: `String`
    - **설명**: 댓글 코드.
- **content**
    - **타입**: `String`
    - **설명**: 댓글 내용.
- **name**
    - **타입**: `String`
    - **설명**: 작성자 이메일.
- **clientCode**
    - **타입**: `String`
    - **설명**: 클라이언트 코드.
- **groupList**
    - **타입**: `List`
    - **설명**: 그룹 리스트.
- **createAt**
    - **타입**: `DateTime`
    - **설명**: 작성일시.
- **status**
    - **타입**: `Enum`
    - **설명**: 상태.
---

## 엔드포인트


### 게이트웨이 연결 테스트

- **URL:** `/app/health`
- **Method:** `GET`
- **Description:** 게이트웨이를 통한 연결을 확인합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization-Key` | API 엑세스 key        |

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
# BasicApp

### App에 등록된 Contents 리스트 가져오기

- **URL:** `/content/V2/menu`
- **Method:** `GET`
- **Description:** 해당 회원의 그룹이나 권한에 따라 App에서 관리자가 등록한 컨텐츠 리스트를 받아옵니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/v2/menu' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** App 에 등록되어있는 컨텐츠 리스트를 받아옵니다.
```json
{
  "result": "SUCCESS",
  "data": [
    {
      "code": "ct_76oZqfmhhyXLM7nGn",
      "name": "ㅇㅎㅇㅎㅇㄴ",
      "status": "ENABLE",
      "fileInfo": {
        "fileId": null,
        "fileUrl": null,
        "fileName": null,
        "fileType": null
      },
      "sequence": 16,
      "capabilityInfo": [
        "VIDEO_LINK"
      ]
    }
  ],
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name                       | Description |
|----------------------------|-------------|
| code `String`              | 컨텐츠 코드      |
| name `String`              | 컨텐츠 이름      |
| status `String`            | 컨텐츠 사용 상태   |
| fileInfo `Object`          | 컨텐츠 로고 정보   |
| fileInfo.fileId `String`   | 파일 ID       |
| fileInfo.fileUrl `String`  | 파일 URL      |
| fileInfo.fileName `String` | 파일 이름       |
| fileInfo.fileType `String` | 파일 유형       |
| sequence `Integer`         | 컨텐츠 순서      |
| capabilityInfo[] `List`    | 기능 정보 리스트   |
| capabilityInfo[] `Enum`    | 컨텐츠 유형 정보   |

- **capabilityInfo[] `Enum` Values**

  | Name         | Description |
  |--------------|-------------|
  | `VIDEO_LINK` | 비디오 링크      |
  | `FILE`       | 파일          |
  | `REPLY`      | 댓글          |
---




## 알림 기능

---
### App 회원 알림

- **URL:** `/content/notification`
- **Method:** `GET`
- **Description:** 엡 회원 알림 리스트.


**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/notification' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```
**Responses Body:**

- **Status Code:** `200`
- **Description:** App 회원 알림 리스트를 받아옵니다.

```json
{
  "result": "SUCCESS",
  "data": [
    {
      "clientCode": "string",
      "summary": "string",
      "redirect": "string",
      "relationCode": "string",
      "type": "COMMON",
      "read": true,
      "createAt": "string"
    }
  ],
  "message": "string",
  "errorCode": "string"
}
```
**Response Fields**
- **data `List` Values**

  | Name                      | Description                            |
  |---------------------------|----------------------------------------|
  | clientCode       `String` | App 회원 코드                              |
  | summary       `String`    | 내용 요약                                  |
  | redirect    `String`      | 해당 컨텐츠 이동 URL                          |
  | relationCode  `String`    | 알림이 발송될 컨텐츠 코드 ex) client 와 연관된 컨텐츠 코드 |
  | type `Enum`               | 컨텐츠 알림 타입                              |
  | read `Boolaen`            | 알림 읽음 여부                               |
  | createAt `String`         | 알림 생성일자                                |

- **type `Enum` Values**

  | Name       | Description  |
  |------------|--------------|
  | `COMMON`   | 공통 컨텐츠 알림 타입 |
  | `PERSONAL` | 개인 컨텐츠 알림 타입 |

---

### App 회원 알림 수동 처리

- **URL:** `/content/notification`
- **Method:** `DELETE`
- **Description:** 알림을 읽음처리 합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**Request Body:**

```json
{
  "relationCode": "string"
}
```

**RequestFields**

| Name                  | Required | Description       |
|-----------------------|----------|-------------------|
| relationCode `String` | `True`   | 컨테츠와의 관계를 확인하는 코드 |

**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/notifications' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "relationCode": "string"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 읽음 처리 완료.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```

---
## 일정관리 기능

---
### 일정 리스트 가져오기

- **URL:** `/content/V2/schedule`
- **Method:** `GET`
- **Description:** 일정관리에 등록된 리스트를 가져옵니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/V2/schedule' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 북마크에서 제거를 완료합니다.
```json
{
  "result": "SUCCESS",
  "data": [
    {
      "code": "cmy_scZQa4Tbkp24mhXv",
      "content": "test",
      "title": "test",
      "start": "2024.02.27. 09:00",
      "end": "2024.02.28. 09:00"
    }
  ],
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name              | Description                  |
|-------------------|------------------------------|
| code `String`     | 일정 코드                        |
| content `String`  | 일정 내용                        |
| title `String`    | 일정 제목                        |
| start `String`    | 시작 일시 (YYYY.MM.DD. HH:mm 형식) |
| end `String`      | 종료 일시 (YYYY.MM.DD. HH:mm 형식) |

---
### 일정 상세내용 조회하기

- **URL:** `/content/V2/schedule/{code}`
- **Method:** `GET`
- **Description:** 일정관리에 등록된 리스트를 가져옵니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| code      | `True`   | 일정 코드.      |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/V2/schedule/{code}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 북마크에서 제거를 완료합니다.
```json
{
  "result": "SUCCESS",
  "data": [
    {
      "code": "cmy_scZQa4Tbkp24mhXv",
      "content": "test",
      "title": "test",
      "start": "2024.02.27. 09:00",
      "end": "2024.02.28. 09:00"
    }
  ],
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name              | Description                  |
|-------------------|------------------------------|
| code `String`     | 일정 코드                        |
| content `String`  | 일정 내용                        |
| title `String`    | 일정 제목                        |
| start `String`    | 시작 일시 (YYYY.MM.DD. HH:mm 형식) |
| end `String`      | 종료 일시 (YYYY.MM.DD. HH:mm 형식) |

---

## 개시판 기능


### 게시물 리스트 가져오기 V2

- **URL:** `/content/V2/community/{menuCode}`
- **Method:** `GET`
- **Description:** 메뉴코드로 특정 게시판의 등록된 게시물 리스트를 가져옵니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Example:**

```bash
curl --request 'GET'\
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 메뉴코드로 특정 게시판의 등록된 게시물 리스트를 가져옵니다..
```json
{
  "result": "SUCCESS",
  "data": {
    "communityList": {
      "first": true,
      "last": true,
      "size": 0,
      "content": [
        {
          "code": "string",
          "menuCode": "string",
          "clientCode": "string",
          "clientName": "string",
          "profileUrl": "string",
          "appCode": "string",
          "title": "string",
          "content": "string",
          "fileId": "string",
          "favoriteCount": 0,
          "createAt": "string",
          "bookmark": true,
          "favorite": true,
          "status": "ACTIVE",
          "capabilityList": [
            "VIDEO_LINK"
          ],
          "fileInfoList": [
            {
              "fileId": "string",
              "fileUrl": "string",
              "fileName": "string",
              "fileType": "string"
            }
          ]
        }
      ],
      "number": 0,
      "sort": {
        "empty": true,
        "sorted": true,
        "unsorted": true
      },
      "numberOfElements": 0,
      "pageable": {
        "offset": 0,
        "sort": {
          "empty": true,
          "sorted": true,
          "unsorted": true
        },
        "pageNumber": 0,
        "pageSize": 0,
        "paged": true,
        "unpaged": true
      },
      "empty": true
    }
  },
  "message": "string",
  "errorCode": "string"
}
```
**Response Fields**

- **communityList**

  | Name                       | Description    |
  |----------------------------|----------------|
  | first `Boolean`            | 첫 페이지 여부       |
  | last `Boolean`             | 마지막 페이지 여부     |
  | size `Integer`             | 페이지 크기         |
  | content `List`             | 페이지 내용         |
  | number `Integer`           | 현재 페이지 번호      |
  | sort `Sort`                | 정렬 정보          |
  | numberOfElements `Integer` | 현재 페이지 내 항목 수  |
  | pageable `Pageable`        | 페이지 정보         |
  | empty `Boolean`            | 페이지가 비어 있는지 여부 |

- **content[]**

  | Name                             | Description       |
  |----------------------------------|-------------------|
  | code `String`                    | 설명                |
  | menuCode `String`                | 메뉴 코드             |
  | clientCode `String`              | 게시물 작성자 App 회원 코드 |
  | clientName `String`              | 게시물 작성자 이름        |
  | profileUrl `String`              | 작성자 프로필 이미지 Url   |
  | appCode `String`                 | App 코드            |
  | title `String`                   | 게시물 제목            |
  | content `String`                 | 게시물 내용            |
  | fileId `String`                  | 게시물 파일 ID         |
  | favoriteCount `Integer`          | 게시물 좋아요 수         |
  | createAt `String`                | 게시물 작성일           |
  | bookmark `Boolean`               | 게시물 북마크 여부        |
  | favorite `Boolean`               | 게시물 좋아요 여부        |
  | status `Enum`                    | 게시물 상태            |
  | capabilityList[] `List`          | 게시물 기능 리스트        |
  | fileInfoList[] `List`            | 파일 정보 목록          |
  | fileInfoList[].fileId `String`   | 파일 ID             |
  | fileInfoList[].fileUrl `String`  | 파일 URL            |
  | fileInfoList[].fileName `String` | 파일 이름             |
  | fileInfoList[].fileType `String` | 파일 유형             |

- **capabilityList[] `Enum` Values**

  | Name         | Description |
  |--------------|-------------|
  | `VIDEO_LINK` | 비디오 링크      |
  | `FILE`       | 파일          |
  | `REPLY`      | 댓글          |

- **status `Enum` Values**

  | Name     | Description |
  |----------|-------------|
  | `ACTIVE` | 활동중         |
  | `BLIND`  | 가리기         |

- **sort (communityList.sort, communityList.pageable.sort)**

  | Name               | Description      |
  |--------------------|------------------|
  | empty `Boolean`    | 정렬 항목이 비어 있는지 여부 |
  | sorted `Boolean`   | 정렬 여부            |
  | unsorted `Boolean` | 정렬되지 않음          |

- **pageable (communityList)**

  | Name                 | Description | 
  |----------------------|-------------|
  | offset `Integer`     | 페이지 오프셋     |
  | sort `Sort`          | 정렬 정보       |
  | pageNumber `Integer` | 현재 페이지 번호   |
  | pageSize `Integer`   | 페이지 크기      |
  | paged `Boolean`      | 페이징 여부      |
  | unpaged `Boolean`    | 페이징 되지 않음   |
---

### 게시물 저장하기 V2

- **URL:** `/content/V2/community/{menuCode}`
- **Method:** `POST`
- **Description:** 메뉴코드로 특정 게시판에 게시물을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "title": "제목",
  "content": "내용",
  "image": "이미지",
  "download": "다운로드",
  "videoLink": "https://www.aipp.help"
}
```

**RequestFields:**

| Name               | Description |
|--------------------|-------------|
| title `String`     | 제목          |
| content `String`   | 내용          |
| image `String`     | 이미지         |
| download `String`  | 다운로드        |
| videoLink `String` | 비디오 링크      |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "title": "제목",
                "content": "내용",
                "image": "이미지",
                "download": "다운로드",
                "videoLink": "https://www.aipp.help"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 특정 게시판에 게시글을 등록하고 게시글의 코드를 받습니다.
```json
{
  "result": "SUCCESS",
  "data": "cmy_Pq7BFjHCWSaKBJoC",
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name                | Description |
|---------------------|-------------|
| data       `String` | 게시글 코드      |


---


### 게시물 수정하기 V2

- **URL:** `/content/V2/community/{menuCode}`
- **Method:** `PUT`
- **Description:** 메뉴코드로 특정 게시판에 있는 게시물을 수정합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "cmy_Pq7BFjHCWSaKBJoC",
  "title": "제목수정",
  "content": "내용수정",
  "image": "string",
  "download": "string",
  "videoLink": "https://www.aiapp.help"
}
```

**RequestFields:**

| Name               | Description |
|--------------------|-------------|
| code `String`      | 게시글 코드      |
| title `String`     | 수정할 제목      |
| content `String`   | 수정할 내용      |
| image `String`     | 수정할 이미지     |
| download `String`  | 수정할 다운로드 링크 |
| videoLink `String` | 수정핳 비디오 링크  |

**Example:**

```bash
curl --request 'PUT' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                  "code": "cmy_Pq7BFjHCWSaKBJoC",
                  "title": "제목수정",
                  "content": "내용수정",
                  "image": "string",
                  "download": "string",
                  "videoLink": "https://www.aiapp.help"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 특정 게시판에 게시글을 등록하고 게시글의 코드를 받습니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```
---

### 게시물 삭제하기 V2

- **URL:** `/content/V2/community/{menuCode}`
- **Method:** `DELETE`
- **Description:** 메뉴코드로 특정 게시판에 게시물을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "string"
}
```

**RequestFields:**

| Name          | Description |
|---------------|-------------|
| code `String` | 게시글 코드      |

**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "code": "게시글 코드",
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 특정 게시판에 게시글을 삭제합니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name                | Description |
|---------------------|-------------|
| data       `String` | 게시글 코드      |



---

### 댓글 저장하기 V2

- **URL:** `/content/V2/community/{menuCode}/reply`
- **Method:** `POST`
- **Description:** 개시글에 댓글을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "content": "댓글 내용",
  "relationCode": "string",
  "groupCode": "string"
}
```

**RequestFields:**

| Name                  | Required | Description    |
|-----------------------|----------|----------------|
| content `String`      | `True`   | 댓글 내용          |
| relationCode `String` | `True`   | 알림 관계 코드       |
| groupCode `String`    | `False`  | 게시판 그룹이 지정된 경우 |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/reply' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                  "content": "dsadasdas",
                  "relationCode": "realationCode
                  "groupCode": "groupCode"
                }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 댓글을 등록합니다.
```json
{
  "result": "SUCCESS",
  "data": "cot_re_EFlBYDjQRESoX",
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name                | Description |
|---------------------|-------------|
| data       `String` | 댓글 코드       |


---

### 댓글 수정하기 V2

- **URL:** `/content/V2/community/{menuCode}/reply`
- **Method:** `PUT`
- **Description:** 게시글에 댓글을 수정합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "string",
  "content": "string"
}
```

**RequestFields:**

| Name             | Required | Description |
|------------------|----------|-------------|
| code `String`    | `True`   | 댓글 코드       |
| content `String` | `True`   | 수정할 댓글 내용   |

**Example:**

```bash
curl --request 'PUT' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/reply' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                  "code": "string",
                  "content": "string"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 댓글을 수정합니다.
```json
{
  "result": "SUCCESS",
  "data": "cot_re_EFlBYDjQRESoX",
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name                | Description |
|---------------------|-------------|
| data       `String` | 댓글 코드       |


---

### 댓글 삭제하기 V2

- **URL:** `/content/V2/community/{menuCode}/reply`
- **Method:** `DELETE`
- **Description:** 게시글에 댓글을 수정합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "string"
}
```

**RequestFields:**

| Name             | Required | Description |
|------------------|----------|-------------|
| code `String`    | `True`   | 댓글 코드       |

**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/reply' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                  "code": "string",
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 댓글을 삭제합니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```

---
### 게시물 좋아요 등록하기 V2

- **URL:** `/content/V2/community/{menuCode}/favorite`
- **Method:** `POST`
- **Description:** 개시글에 좋아요를 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "게시글 코드"
}
```

**RequestFields:**

| Name          | Required | Description |
|---------------|----------|-------------|
| code `String` | `True`   | 게시글 코드 번호   |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "code": "cmy_XXX",
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 댓글을 등록합니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```

---

### 게시물 좋아요 취소하기 V2

- **URL:** `/content/V2/community/{menuCode}/favorite`
- **Method:** `DELETE`
- **Description:** 개시글에 좋아요를 취소합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "게시글 코드"
}
```

**RequestFields:**

| Name          | Required | Description |
|---------------|----------|-------------|
| code `String` | `True`   | 게시글 코드 번호   |

**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "code": "cmy_XXX",
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 좋아요를 취소합니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```
---

### 게시물 북마크 등록하기 V2

- **URL:** `/content/V2/community/{menuCode}/bookmark`
- **Method:** `POST`
- **Description:** 개시글을 북마크에 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "게시글 코드"
}
```

**RequestFields:**

| Name          | Required | Description |
|---------------|----------|-------------|
| code `String` | `True`   | 게시글 코드 번호   |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "code": "cmy_XXX",
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글을 북마크에 등록합니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```

---

### 게시물 북마크 취소하기 V2

- **URL:** `/content/V2/community/{menuCode}/bookmark`
- **Method:** `DELETE`
- **Description:** 개시글에 북마크를 취소합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**Request Body:**

```json
{
  "code": "게시글 코드"
}
```

**RequestFields:**

| Name          | Required | Description |
|---------------|----------|-------------|
| code `String` | `True`   | 게시글 코드 번호   |

**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "code": "cmy_XXX",
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 북마크를 취소합니다.
```json
{
  "result": "SUCCESS",
  "data": "OK",
  "message": null,
  "errorCode": null
}
```

---

### 게시물 상세정보 V2

- **URL:** `/content/V2/community/{menuCode}/detail`
- **Method:** `GET`
- **Description:** 개시글에 상세정보를 확인합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| menuCode  | `True`   | 컨텐츠 게시판 코드  |

**QueryParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| code      | `True`   | 게시물 코드      |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/{menuCode}/detail?code={code}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시물의 상세정보를 조회합니다.
```json
{
  "result": "SUCCESS",
  "data": {
    "videoLink": null,
    "download": [],
    "reply": [
      {
        "code": "cot_re_kC4uX1N6LACbb",
        "content": "댓글내용",
        "name": "test11@test.com",
        "clientCode": "app_mbr_aEhqdc7rVbq9",
        "groupList": [],
        "createAt": "2024-07-10T15:48:57.11584",
        "status": "ACTIVE"
      }
    ],
    "replyCount": 2
  },
  "message": null,
  "errorCode": null
}
```
**Response Fields**

- **videoLink**

  | Name                          | Description |
  |-------------------------------|-------------|
  | videoLink `String` `Optional` | 비디오 링크      |

- **download**

  | Name                       | Description |
  |----------------------------|-------------|
  | download `List` `Optional` | 다운로드 링크 목록  |

- **reply (댓글 리스트)**

  | Name                | Description |
  |---------------------|-------------|
  | code `String`       | 댓글 코드       |
  | content `String`    | 댓글 내용       |
  | name `String`       | 작성자 이메일     |
  | clientCode `String` | 클라이언트 코드    |
  | groupList `List`    | 그룹 리스트      |
  | createAt `DateTime` | 작성일시        |
  | status `Enum`       | 상태          |

- **status `Enum` Values**

  | Name     | Description |
  |----------|-------------|
  | `ACTIVE` | 활동중         |
  | `BLIND`  | 가리기         |

- **replyCount**

  | Name                        | Description |
  |-----------------------------|-------------|
  | replyCount `Integer`        | 댓글 수        |

---

### 게시물 북마크 리스트 V2

- **URL:** `/content/V2/community/bookmark/list`
- **Method:** `GET`
- **Description:** 북마크를 등록한 리스트를 확인합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/V2/community/bookmark/list' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 북마크에 등록한 게시글 리스트를 받아옵니다.
```json
{
  "result": "SUCCESS",
  "data": {
    "communityList": {
      "content": [
        {
          "code": "cmy_XX",
          "menuCode": "ct_XX",
          "clientCode": "app_mbr_XX",
          "clientName": "test11@test.com",
          "profileUrl": "test11@test.com",
          "appCode": "{appCode}",
          "title": "제목2",
          "content": "내용2",
          "fileId": "FLE_2408",
          "favoriteCount": 0,
          "createAt": "2024.07.09. 16:51",
          "bookmark": true,
          "favorite": false,
          "status": "ACTIVE",
          "capabilityList": [
            "VIDEO_LINK"
          ],
          "fileInfoList": [
            {
              "fileId": "FLE_2408",
              "fileUrl": "https://file.mbaas.kr/assets/20240703/c5267f1e-c6e7-495b-b0ca-ef9039f0aa07.png",
              "fileName": "Capa_1 (3).png",
              "fileType": "png"
            }
          ]
        }
      ],
      "pageable": {
        "sort": {
          "empty": false,
          "unsorted": false,
          "sorted": true
        },
        "offset": 0,
        "pageNumber": 0,
        "pageSize": 1,
        "paged": true,
        "unpaged": false
      },
      "first": true,
      "last": true,
      "size": 1,
      "number": 0,
      "sort": {
        "empty": false,
        "unsorted": false,
        "sorted": true
      },
      "numberOfElements": 1,
      "empty": false
    }
  },
  "message": null,
  "errorCode": null
}
```
**Response Fields**

- **pageable (페이지 정보)**

| Name                 | Description |
|----------------------|-------------|
| sort `Object`        | 정렬 정보       |
| offset `Integer`     | 오프셋         |
| pageNumber `Integer` | 페이지 번호      |
| pageSize `Integer`   | 페이지 크기      | 
| paged `Boolean`      | 페이징 여부      |
| unpaged `Boolean`    | 페이징 안함 여부   |

- **sort**

  | Name               | Description |
  |--------------------|-------------|
  | empty `Boolean`    | 비어있는지 여부    |
  | unsorted `Boolean` | 정렬되지 않음 여부  |
  | sorted `Boolean`   | 정렬됨 여부      |


- **페이지 정보**

  | Name                       | Description |
  |----------------------------|-------------|
  | first `Boolean`            | 첫 페이지 여부    |
  | last `Boolean`             | 마지막 페이지 여부  |
  | size `Integer`             | 페이지 크기      |
  | number `Integer`           | 페이지 번호      |
  | numberOfElements `Integer` | 요소 수        |
  | empty `Boolean`            | 비어있는지 여부    |


- **communityList**

    - **content**

      | Name                    | Description              |
      |-------------------------|--------------------------|
      | code `String`           | 게시글 코드                   |
      | menuCode `String`       | 게시판 메뉴 코드                |
      | clientCode `String`     | App 회원 코드                |
      | clientName `String`     | App 회원 이름                |
      | profileUrl `String`     | App 회원 프로필 URL           |
      | appCode `String`        | 앱 코드                     |
      | title `String`          | 제목                       |
      | content `String`        | 내용                       |
      | fileId `String`         | 파일 ID                    |
      | favoriteCount `Integer` | 즐겨찾기 수                   |
      | createAt `String`       | 작성일시 (yyyy.MM.dd. HH:mm) |
      | bookmark `Boolean`      | 북마크 여부                   |
      | favorite `Boolean`      | 좋아요 여부                   |
      | status `String`         | 상태 (예: ACTIVE)           |
      | capabilityList `List`   | 기능 목록                    |
      | fileInfoList `List`     | 파일 정보 리스트                |

    - **fileInfoList**

      | Name              | Description |
      |-------------------|-------------|
      | fileId `String`   | 파일 ID       |
      | fileUrl `String`  | 파일 URL      |
      | fileName `String` | 파일 이름       |
      | fileType `String` | 파일 유형       |

    - **capabilityList[] `Enum` Values**

      | Name         | Description |
      |--------------|-------------|
      | `VIDEO_LINK` | 비디오 링크      |
      | `FILE`       | 파일          |
      | `REPLY`      | 댓글          | 

    - **status `Enum` Values**

      | Name     | Description |
      |----------|-------------|
      | `ACTIVE` | 활동중         |
      | `BLIND`  | 가리기         |



---


# CustomApp

## 원데이 클래스 App

---
### 강의 리스트 가져오기

- **URL:** `/content/one_day_class`
- **Method:** `GET`
- **Description:** 등록된 강의 리스트.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/one_day_class' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' 
```

**Responses Body:**

- **Status Code:** `200`
- **Description:**  강의 리스트를 가져옵니다.
```json
{
  "result": "SUCCESS",
  "data": {
    "next": true,
    "prev": true,
    "nowPage": 0,
    "totalPage": 0,
    "totalCount": 0,
    "mainList": [
      {
        "code": "string",
        "name": "string",
        "capabilityInfo": [
          "VIDEO_LINK"
        ],
        "fileInfo": {
          "fileId": "string",
          "fileUrl": "string",
          "fileName": "string",
          "fileType": "string"
        },
        "sequence": 0,
        "createAt": "string",
        "groupList": [
          {
            "idx": 0,
            "groupCode": "string",
            "groupName": "string"
          }
        ],
        "status": "string"
      }
    ]
  },
  "message": "string",
  "errorCode": "string"
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


- **mainList**
    
    | Name                         | Description            |
    |------------------------------|------------------------|
    | code `String`                | 항목 코드                  |
    | name `String`                | 항목 이름                  |
    | capabilityInfo `List`        | 항목의 기능 정보              |
    | capabilityInfo[] `Enum`      | 항목의 기능 정보 개별 항목        |
    | fileInfo `Object`            | 파일 정보                  |
    | fileInfo.fileId `String`     | 파일 ID                  |
    | fileInfo.fileUrl `String`    | 파일 URL                 |
    | fileInfo.fileName `String`   | 파일 이름                  |
    | fileInfo.fileType `String`   | 파일 유형                  |
    | sequence `Integer`           | 항목 순서                  |
    | createAt `String`            | 항목 생성 시각 (ISO 8601 형식) |
    | groupList `List`             | 그룹 목록                  |
    | groupList[] `List`           | 그룹 목록 개별 항목            |
    | groupList.idx `Integer`      | 그룹 인덱스                 |
    | groupList.groupCode `String` | 그룹 코드                  |
    | groupList.groupName `String` | 그룹 이름                  |
    | status `String`              | 항목 상태                  |

- **capabilityInfo[] `Enum` Values**

  | Name         | Description |
  |--------------|-------------|
  | `VIDEO_LINK` | 비디오 링크      |
  | `FILE`       | 파일          |
  | `REPLY`      | 댓글          |


---


## 테이크아웃

---
### Item 리스트 조회

- **URL:** `/content/item`
- **Method:** `GET`
- **Description:** 아이템 리스트를 조회합니다..

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/item' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** Item 리스트를 조회합니다.
```json
{
  "result": "SUCCESS",
  "data": {
    "next": false,
    "prev": false,
    "nowPage": 0,
    "totalPage": 1,
    "totalCount": 1,
    "mainList": [
      {
        "code": "itm_ttkzGRh41ncoVPIm",
        "appCode": "kr.mbaas.app.managerjm",
        "partnerCode": "mbr_test",
        "name": "가로로 긴 사진",
        "content": "<p>테스트</p>",
        "price": 3300,
        "hits": 0,
        "fileId": "FLE_2426",
        "fileInfoList": [
          {
            "fileId": "FLE_2426",
            "fileUrl": "https://file.mbaas.kr/assets/20240704/00486f0a-5927-41a9-bdbe-f44dcc0cfd18.png",
            "fileName": "Frame.png",
            "fileType": "png"
          }
        ],
        "favorites": 0,
        "status": "PREPARE"
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


- **mainList**

  | Name                             | Description       |
  |----------------------------------|-------------------|
  | code `String`                    | Item 코드           |
  | appCode `String`                 | App 코드            |
  | partnerCode `String`             | App 관리자 회원 코드     |
  | name `String`                    | Item 이름           |
  | content `String`                 | Item 내용           |
  | price `Integer`                  | Item 가격           |
  | hits `Integer`                   | 조회수               |
  | fileId `String`                  | Item 이미지 파일 그룹아이디 |
  | fileInfoList[] `List`            | 파일 정보 목록          |
  | fileInfoList[].fileId `String`   | 파일 ID             |
  | fileInfoList[].fileUrl `String`  | 파일 URL            |
  | fileInfoList[].fileName `String` | 파일 이름             |
  | fileInfoList[].fileType `String` | 파일 유형             |
  | favorites `Integer`              | 좋아요 수             |
  | status `String`                  | 항목 상태             |


---
### Item 상세조회

- **URL:** `/content/item/{itemCode}`
- **Method:** `GET`
- **Description:** Item 코드로 해당 Item 정보를 조회합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| itemCode  | `True`   | Item 코드.    |


**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/item/{itemCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' 
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** QnA에 파일을 등록합니다..
```json
{
  "result": "SUCCESS",
  "data": {
    "code": "itm_ttkzGRh41ncoVPIm",
    "appCode": "kr.mbaas.app.managerjm",
    "partnerCode": "mbr_test",
    "name": "가로로 긴 사진",
    "content": "<p>테스트</p>",
    "price": 3300,
    "hits": 0,
    "fileId": "FLE_2426",
    "fileInfoList": [
      {
        "fileId": "FLE_2426",
        "fileUrl": "https://file.mbaas.kr/assets/20240704/00486f0a-5927-41a9-bdbe-f44dcc0cfd18.png",
        "fileName": "Frame.png",
        "fileType": "png"
      }
    ],
    "favorites": 0,
    "status": "PREPARE"
  },
  "message": null,
  "errorCode": null
}
```

**Response Fields**
    
| Name                             | Description       |
|----------------------------------|-------------------|
| code `String`                    | Item 코드           |
| appCode `String`                 | App 코드            |
| partnerCode `String`             | App 관리자 회원 코드     |
| name `String`                    | Item 이름           |
| content `String`                 | Item 내용           |
| price `Integer`                  | Item 가격           |
| hits `Integer`                   | 조회수               |
| fileId `String`                  | Item 이미지 파일 그룹 ID |
| fileInfoList[] `List`            | 파일 정보 목록          |
| fileInfoList[].fileId `String`   | 파일 ID             |
| fileInfoList[].fileUrl `String`  | 파일 URL            |
| fileInfoList[].fileName `String` | 파일 이름             |
| fileInfoList[].fileType `String` | 파일 유형             |
| favorites `Integer`              | 좋아요 수             |
| status `String`                  | 항목 상태             |


- **status `Enum` Values**

  | Name          | Description |
  |---------------|-------------|
  | `PREPARE`     | 판매준비중       |
  | `ON_SALE`     | 판매중         |
  | `END_OF_SALE` | 판매종료        |


---
### Item 북마크에 등록하기

- **URL:** `/content/item/{itemCode}/favorite`
- **Method:** `POST`
- **Description:** itemCode로 북마크에 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| itemCode  | `True`   | Item 코드.    |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/item/{itemCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 북마크 등록을 완료합니다.
```json
{
  "result": "SUCCESS",
  "data": "SUCCESS",
  "message": null,
  "errorCode": null
}
```

### Item 북마크에서 제거하기

- **URL:** `/content/item/{itemCode}/favorite`
- **Method:** `DELETE`
- **Description:** itemCode로 북마크에서 제거합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |


**PathParameters**

| Parameter | Required | Description |
|-----------|----------|-------------|
| itemCode  | `True`   | Item 코드.    |

**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/item/{itemCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 북마크에서 제거를 완료합니다.
```json
{
  "result": "SUCCESS",
  "data": "SUCCESS",
  "message": null,
  "errorCode": null
}
```
---
## 커뮤니티

---
### 메인 페이지

- **URL:** `/content/community/main`
- **Method:** `GET`
- **Description:** 메인페이지의 데이터를 가져옵니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**QueryParameters**

| Name             | Required | Description            |
|------------------|----------|------------------------|
| appCode `String` | `True`   | 메인 페이지를 불러올 고유 appCode |

**Example:**

```bash
curl --request 'GET'\
      --url 'https://api.aiapp.link/aiapp/content/community/main?appCode={appCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 메인페이지의 정보를 가져옵니다 .
```json
{
  "result": "SUCCESS",
  "data": [
    {
      "code": "cmy_r3soppWBxbm7uTyP",
      "menuCode": null,
      "clientCode": "app_mbr_aEhqdc7rVbq9",
      "clientName": "테스트11",
      "profileUrl": null,
      "appCode": "kr.mbaas.app.managerjm",
      "title": "제목2",
      "content": "내용2",
      "fileId": "FLE_2408",
      "favoriteCount": 0,
      "createAt": "2024.07.09. 16:51",
      "bookmark": true,
      "favorite": false,
      "status": "ACTIVE",
      "capabilityList": null,
      "fileInfoList": [
        {
          "fileId": "FLE_2408",
          "fileUrl": "https://file.mbaas.kr/assets/20240703/c5267f1e-c6e7-495b-b0ca-ef9039f0aa07.png",
          "fileName": "Capa_1 (3).png",
          "fileType": "png"
        }
      ]
    }
  ],
  "message": null,
  "errorCode": null
}
```
**Response Fields**

| Name                             | Description      |
|----------------------------------|------------------|
| code `String`                    | 댓글 코드번호          |
| menuCode `String` `nullable`     | 메뉴 코드            |
| clientCode `String`              | 댓글 작성자 App 회원 코드 |
| clientName `String`              | 댓글 작성자 이름        |
| profileUrl `String` `nullable`   | 프로필 이미지 Url      |
| appCode `String`                 | 앱 코드             |
| title `String`                   | 제목               |
| content `String`                 | 내용               |
| fileId `String`                  | 파일 ID            |
| favoriteCount `Integer`          | 좋아요 수            |
| createAt `String`                | 작성일              |
| bookmark `Boolean`               | 북마크 여부           |
| favorite `Boolean`               | 좋아요 여부           |
| status `String`                  | 상태               |
| capabilityList `List` `nullable` | 기능 리스트           |
| capabilityList[] `Enum`          | 기능 목록            |
| fileInfoList `List`              | 파일 정보 목록         |

- **capabilityList[] `Enum` Values**

  | Name         | Description |
  |--------------|-------------|
  | `VIDEO_LINK` | 비디오 링크      |
  | `FILE`       | 파일          |
  | `REPLY`      | 댓글          |

- **fileInfoList[]**

  | Name              | Description |
  |-------------------|-------------|
  | fileId `String`   | 파일 ID       |
  | fileUrl `String`  | 파일 URL      |
  | fileName `String` | 파일 이름       |
  | fileType `String` | 파일 타입       |


---
### 게시글 등록

- **URL:** `/content/community`
- **Method:** `POST`
- **Description:** 게시글을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**Request Body:**

```json
{
  "title": "string",
  "content": "string",
  "image": "FLE_2408",
  "download": "첨부파일 파일 아이디",
  "videoLink": "https://www.aiapp.help"
}
```
**RequestFields**

| Name               | Description |
|--------------------|-------------|
| title `String`     | 제목          |
| content `String`   | 내용          |
| image `String`     | 이미지 파일 ID   |
| download `String`  | 다운로드 링크     |
| videoLink `String` | 비디오 링크 URL  |


**Example:**

```bash
curl --request 'POST'\
      --url 'https://api.aiapp.link/aiapp/content/community' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "title": "제목2",
                "content": "내용2",
                "image": "FLE_2408",
                "download": "다운링크",
                "videoLink": "https://www.aiapp.help"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글 등록 완료.
```json
{
  "result": "SUCCESS",
  "data": "cmy_r3soppWBxbm7uTyP",
  "message": null,
  "errorCode": null
}
```

---

### 게시물 상세 내용 조회

- **URL:** `/content/ccommunity/detail/{communityCode}`
- **Method:** `GET`
- **Description:** 게시물 리스트 조회시 모든 정보를 불러 오기 때문에 게시물의 댓글만 조회 합니다.


**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter     | Required | Description |
|---------------|----------|-------------|
| communityCode | `True`   | 게시글 코드.     |



**Example:**

```bash
curl --request GET \
      --url 'https://api.aiapp.link/aiapp/content/community/detail/{communityCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}}'
```
**Responses Body:**

- **Status Code:** `200`
- **Description:** 해당 회원이 문의한 QnA 리스트를 가져옵니다.

```json
{
  "result": "SUCCESS",
  "data": {
    "next": false,
    "prev": false,
    "nowPage": 0,
    "totalPage": 0,
    "totalCount": 0,
    "communityReplyList": [
      {
        "code": "string",
        "clientCode": "string",
        "clientName": "string",
        "profileUrl": "string",
        "content": "string",
        "createAt": "string"
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

- **communityReplyList (댓글 리스트)**

  | Name                | Description      |
  |---------------------|------------------|
  | code `Integer`      | 댓글 코드번호          |
  | clientCode `String` | 댓글 작성자 App 회원 코드 |
  | clientName `String` | 댓글 작성자 이름        |
  | profileUrl `String` | 프로필 이미지 Url      |
  | content `String`    | 댓글 내용            |
  | createAt `String`   | 댓글 작성일           |


---
### 게시글 좋아요 등록

- **URL:** `/content/community/{communityCode}/favorite`
- **Method:** `POST`
- **Description:** 게시글에 좋아요를 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter     | Required | Description |
|---------------|----------|-------------|
| communityCode | `True`   | 게시글 코드.     |


**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/community{communityCode}/bookmark' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글을 북마크에 등록합니다.
```json
{
  "result": "SUCCESS",
  "data": "북마크 등록 완료",
  "message": null,
  "errorCode": null
}
```


### 게시글 좋아요 취소

- **URL:** `/content/community/{communityCode}/favorite`
- **Method:** `DELETE`
- **Description:** 게시글에 좋아요를 취소합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter     | Required | Description |
|---------------|----------|-------------|
| communityCode | `True`   | 게시글 코드.     |


**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/community{communityCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 좋아요를 취소합니다.
```json
{
  "result": "SUCCESS",
  "data": "좋아요 취소 완료",
  "message": null,
  "errorCode": null
}
```

---
### 게시글 북마크 등록

- **URL:** `/content/community/{communityCode}/bookmark`
- **Method:** `POST`
- **Description:** 게시글에 좋아요를 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter     | Required | Description |
|---------------|----------|-------------|
| communityCode | `True`   | 게시글 코드.     |


**Example:**

```bash
curl --request 'POST' \
      --url 'https://api.aiapp.link/aiapp/content/community{communityCode}/favorite' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 좋아요를 등록합니다.
```json
{
  "result": "SUCCESS",
  "data": "좋아요 등록 완료",
  "message": null,
  "errorCode": null
}
```
---
### 게시글 북마크 취소

- **URL:** `/content/community/{communityCode}/bookmark`
- **Method:** `DELETE`
- **Description:** 게시글의 북마크를 취소합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**PathParameters**

| Parameter     | Required | Description |
|---------------|----------|-------------|
| communityCode | `True`   | 게시글 코드.     |


**Example:**

```bash
curl --request 'DELETE' \
      --url 'https://api.aiapp.link/aiapp/content/community{communityCode}/bookmark' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글의 북마크를 취소합니다.
```json
{
  "result": "SUCCESS",
  "data": "북마크 취소 완료",
  "message": null,
  "errorCode": null
}
```

---
### 게시글 댓글 등록

- **URL:** `/content/community/reply`
- **Method:** `POST`
- **Description:** 게시글에 댓글을 등록합니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**Request Body:**

```json
{
  "code": "cmy_r3soppWBxbm7uTyP",
  "content": "string",
  "clientName": "string"
}
```
**RequestFields**

| Name                | Required | Description |
|---------------------|----------|-------------|
| code `String`       | `True`   | 커뮤니티 코드     |
| content `String`    | `True`   | 댓글 내용       |
| clientName `String` | `False`  | 설명          |


**Example:**

```bash
curl --request 'POST'\
      --url 'https://api.aiapp.link/aiapp/content/community/reply' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}' \
      --header 'Content-Type: application/json' \
      --data '{
                "code": "cmy_r3soppWBxbm7uTyP",
                "content": "string",
                "clientName": "string"
              }'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글에 댓글을 등록합니다.
```json
{
  "result": "SUCCESS",
  "data": "cmy_re_QqeHx50oiIAvD",
  "message": null,
  "errorCode": null
}
```

**Response Fields**

  | Name                | Description |
  |---------------------|-------------|
  | data       `String` | 댓글 코드       |


---

### 게시물 리스트 가져오기

- **URL:** `/content/community/list`
- **Method:** `GET`
- **Description:** 게시물 페이지를 가져옵니다.

**RequestHeader**

| Name                | Description        |
|---------------------|--------------------|
| `Authorization`     | 로그인 App 회원의 JWT 토큰 |
| `Authorization-Key` | API 엑세스 key        |

**QueryParameters**

| Name             | Required | Description            |
|------------------|----------|------------------------|
| appCode `String` | `True`   | 메인 페이지를 불러올 고유 appCode |

**Example:**

```bash
curl --request 'GET' \
      --url 'https://api.aiapp.link/aiapp/content/community/list?appCode={appCode}' \
      --header 'Authorization-Key: {API Key}' \
      --header 'Authorization: Bearer {token}'

```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게시글 페이지를 가져옵니다 .
```json
{
  "result": "SUCCESS",
  "data": {
    "next": true,
    "prev": false,
    "nowPage": 0,
    "totalPage": 49,
    "totalCount": 49,
    "communityMainSimpleList": [
      {
        "code": "cmy_r3soppWBxbm7uTyP",
        "menuCode": null,
        "clientCode": "app_mbr_aEhqdc7rVbq9",
        "clientName": "테스트11",
        "profileUrl": null,
        "appCode": "kr.mbaas.app.managerjm",
        "title": "제목2",
        "content": "내용2",
        "fileId": "FLE_2408",
        "favoriteCount": 0,
        "createAt": "2024.07.09. 16:51",
        "bookmark": true,
        "favorite": false,
        "status": "ACTIVE",
        "capabilityList": null,
        "fileInfoList": [
          {
            "fileId": "FLE_XXXX",
            "fileUrl": "",
            "fileName": "",
            "fileType": "png"
          }
        ]
      }
    ]
  },
  "message": null,
  "errorCode": null
}
```
**Response Fields**

- **페이지 정보**

  | Name                 | Description |
  |----------------------|-------------|
  | next `Boolean`       | 다음 페이지 여부   |
  | prev `Boolean`       | 이전 페이지 여부   |
  | nowPage `Integer`    | 현재 페이지 번호   |
  | totalPage `Integer`  | 전체 페이지 수    |
  | totalCount `Integer` | 전체 공지사항 수   |

- **communityMainSimpleList**

  | Name                             | Description      |
  |----------------------------------|------------------|
  | code `String`                    | Item 코드          |
  | menuCode `String` `nullable`     | 메뉴 코드            |
  | clientCode `String`              | 댓글 작성자 App 회원 코드 |
  | clientName `String`              | 댓글 작성자 이름        |
  | profileUrl `String` `nullable`   | 프로필 이미지 Url      |
  | appCode `String`                 | App 코드           |
  | title `String`                   | 제목               |
  | content `String`                 | 내용               |
  | fileId `String`                  | 파일 ID            |
  | favoriteCount `Integer`          | 좋아요 수            |
  | createAt `String`                | 작성일              |
  | bookmark `Boolean`               | 북마크 여부           |
  | favorite `Boolean`               | 좋아요 여부           |
  | status `String`                  | 상태               |
  | capabilityList `List` `nullable` | 기능 리스트           |
  | capabilityList[] `Enum`          | 기능 목록            |
  | fileInfoList[] `List`            | 파일 정보 목록         |
  | fileInfoList[].fileId `String`   | 파일 ID            |
  | fileInfoList[].fileUrl `String`  | 파일 URL           |
  | fileInfoList[].fileName `String` | 파일 이름            |
  | fileInfoList[].fileType `String` | 파일 유형            |

- **capabilityList[] `Enum` Values**

  | Name         | Description |
  |--------------|-------------|
  | `VIDEO_LINK` | 비디오 링크      |
  | `FILE`       | 파일          |
  | `REPLY`      | 댓글          |


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
| Error Code                 | Status Code | Description                              |
|----------------------------|-------------|------------------------------------------|
| `COMMON_SYSTEM_ERROR`      | `500`       | 일시적인 오류가 발생했습니다. 잠시 후 다시 시도해주세요. (장애 상황) |
| `COMMON_INVALID_PARAMETER` | `200`       | 요청한 값이 올바르지 않습니다.                        |
| `COMMON_ENTITY_NOT_FOUND`  | `200`       | 존재하지 않는 엔티티입니다.                          |
| `COMMON_ILLEGAL_STATUS`    | `200`       | 잘못된 상태값입니다.                              |
| `COMMON_ORDER`             | `200`       | 주문이 정상적으로 이루어지지 않았습니다.                   |
| `COMMON_RESERVATION`       | `400`       | 예약이 정상적으로 이루어지지 않았습니다.                   |
| `INVALID_AUTH`             | `200`       | 작성자 정보와 토큰 정보가 일치하지 않습니다.                |
| `INVALID_ROLE`             | `200`       | 유저권한이 존재하지 않거나 권한이 없습니다.                 |


## 자주 묻는 질문

### Q: 인증은 어떻게 하나요?
A: `Authorization` 헤더에 Bearer 토큰을 보내야 합니다.

### Q: 요청 본문은 어떤 형식이어야 하나요?
A: 이미지 업로드를 제외한 모든 요청 본문은 `JSON` 형식이어야 합니다.
