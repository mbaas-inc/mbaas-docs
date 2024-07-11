# AppMember API Docs

---

1. [AppMember 객체](#AppMember-객체)
2. [API 개요](#api-개요)
3. 엔드포인트
   - [게이트웨이 연결 테스트](#게이트웨이-연결-테스트)
   - [이메일 인증번호 발송](#이메일-인증번호-발송)
   - [이메일 인증번호 확인](#이메일-인증번호-확인)
   - [비밀번호 재설정](#비밀번호-재설정)
   - [App 회원 회원가입](#app-회원-회원가입)
   - [App 회원 로그인](#app-회원-로그인)
   - [App 회원 내 정보](#app-회원-내-정보)
   - [App 회원 프로필 등록 & 수정](#app-회원-프로필-등록--수정)
4. [에러 코드](#에러-코드)
   - [Status Code](#status-code)
   - [CustomErrorCode](#customerrorcode)
     - [System](#system)
     - [Request](#request)
     - [Auth Email](#auth-email)
     - [Member](#member)
     - [App](#app)
     - [Company](#company)
     - [Token](#token)
     - [FeignClient](#feignclient)
     - [Status](#status)
5. [자주 묻는 질문](#자주-묻는-질문)

---
## AppMember 객체

### Response 객체 상세
- **result**
  - **`SUCCESS`**: 요청의 결과 성공을 나타냅니다.
  - **`FAIL`**: 요청에 문제가 있어 실패했음을 나타냅니다.
- **data**: 요청 결과에 대한 데이터를 포함합니다. 예) `data.appCode`
- **message**: 요청의 결과에 추가 메시지나 실패 시 `CustomErrorCode`의 내용을 응답합니다.
- **errorCode**: 발생한 예외의 `CustomErrorCode`를 응답합니다.

### App 회원 객체 상세
- **appCode**
  - **타입**: `String`
  - **설명**: 애플리케이션의 고유 코드를 나타내며, 인증 요청 시 해당 앱을 식별하는 데 사용됩니다.

- **appMemberEmail**
  - **타입**: `String`
  - **설명**: App 회원의 이메일입니다.

- **appMemberPhone**
  - **타입**: `String`
  - **설명**: App 회원의 연락처입니다.

- **appMemberCode**
  - **타입**: `String`
  - **설명**: App 회원의 고유 코드를 나타내며, 인증 요청 시 해당 회원을 식별하는 데 사용됩니다.

- **appMemberName**
  - **타입**: `String`
  - **설명**: App 회원의 이름입니다.

- **appMemberExPassword**
  - **타입**: `String`
  - **설명**: 비밀번호 변경에 사용되며, 변경할 비밀번호를 입력합니다.

- **appMemberNewPassword**
  - **타입**: `String`
  - **설명**: 비밀번호 변경에 사용되며, 변경할 비밀번호를 재입력 받아 일치 여부를 확인합니다.

- **accessToken**
  - **타입**: `String`
  - **설명**: 로그인이 완료된 이후 발급되는 JWT 토큰이며, 이후 인증 과정에서 사용됩니다.

- **emailAuthType**
  - **타입**: `Enum`
  - **설명**: 이메일 인증 요청의 타입을 지정합니다. 두 가지 값이 있습니다:
    - **`JOIN`**: 회원 가입 과정에서 이메일 인증을 요청할 때 사용합니다.
    - **`PW`**: 비밀번호 재설정 과정에서 이메일 인증을 요청할 때 사용합니다.

- **appMemberStatus**
  - **타입**: `Enum`
  - **설명**: App 회원의 상태를 나타냅니다. 다섯 가지 값이 있습니다:
    - **`GREEN`**: 활동 상태의 App 회원을 나타냅니다.
    - **`YELLOW`**: 정지 상태의 App 회원을 나타냅니다.
    - **`BLUE`**: 휴면 상태의 App 회원을 나타냅니다.
    - **`RED`**: 탈퇴 상태의 App 회원을 나타냅니다.
    - **`BLACK`**: 강퇴 상태의 App 회원을 나타냅니다.

---
## API 개요

**Base URL:** `https://api.aiapp.link/api`

**Version:** v1

**Authentication:** Bearer Token

**API Key:** `<ACCESS_TOKEN>`

---

## 엔드포인트


### 게이트웨이 연결 테스트

- **URL:** `/app/health`
- **Method:** `GET`
- **Description:** 게이트웨이를 통한 연결을 확인합니다.

**Example:**

```bash
curl -X GET 'https://api.aiapp.link/api/app/health' \
  -H 'accept: application/json'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 게이트 웨이 상태 양호
```json
{"result": "SUCCESS", "message": "app-service OK"}
```

### 이메일 인증번호 발송

- **URL:** `/app/member/auth/send`
- **Method:** `POST`
- **Description:** 이메일 인증을 요청합니다.


**Request Body:**

```json
{
  "appCode": "string",
  "appMemberEmail": "string",
  "emailAuthType": "JOIN"
}
```
**RequestFields**

| Name                    | Required | Description        |
|-------------------------|----------|--------------------|
| appCode `String`        | `True`   | App 의 고유 Code 입니다. |
| appMemberEmail `String` | `True`   | 인증을 요청할 Email.     |
| emailAuthType `Enum`    | `True`   | 인증 요청의 타입 입니다.     |

**emailAuthType Enum Values**

| Name   | Description            |
|--------|------------------------|
| `JOIN` | 회원 가입 시 이메일 인증 요청 타입   |
| `PW`   | 비밀번호 찾기 시 이메일 인증 요청 타입 |

**Example:**

```bash
curl -X POST 'https://api.aiapp.link/api/app/member/auth/send' \
-H 'Content-Type: application/json;charset=utf-8' \
-H 'Accept: */*' \
-d '{
"appCode" : "testAppCode",
"appMemberEmail" : "jjunmo@mbaas.kr",
"emailAuthType" : "JOIN"
}'
```
**Responses Body:**

- **Status Code:** `200`
- **Description:** 인증코드 발송 완료.
```json
{"result":"SUCCESS","message":"인증코드 발송완료"}
```
---

### 이메일 인증번호 확인

- **URL:** `/app/member/auth/send`
- **Method:** `PUT`
- **Description:** 이메일 인증을 요청합니다.


**Request Body:**

```json
{
  "appMemberEmail": "string",
  "authCode": "string",
  "emailAuthType": "JOIN",
  "appCode": "string"
}
```
**RequestFields**

| Name                    | Required | Description          |
|-------------------------|----------|----------------------|
| appMemberEmail `String` | `True`   | 인증을 확인할 Email 입니다.   |
| authCode `String`       | `True`   | Email 로 받은 인증번호 입니다. |
| emailAuthType `Enum`    | `True`   | 인증 요청의 타입 입니다.       |
| appCode `String`        | `True`   | App 의 고유 Code 입니다.   |

**emailAuthType Enum Values**

| Name   | Description            |
|--------|------------------------|
| `JOIN` | 회원 가입 시 이메일 인증 요청 타입   |
| `PW`   | 비밀번호 찾기 시 이메일 인증 요청 타입 |


**Example:**

```bash
curl -X PUT 'https://api.aiapp.link/api/app/member/auth/send' \
    -H 'Content-Type: application/json;charset=utf-8' \
    -H 'Accept: */*' \
    -d '{
  "appMemberEmail" : "jjunmo@mbaas.kr",
  "authCode" : "123456",
  "emailAuthType" : "JOIN",
  "appCode" : "testAppCode"
}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 인증 확인.
```json
{"result" : "SUCCESS", "message" : "인증 완료"}
```
---


### 비밀번호 재설정

- **URL:** `/app/member/auth`
- **Method:** `POST`
- **Description:** 비밀번호를 재설정 합니다..


**Request Body:**

```json
{
  "appCode": "string",
  "appMemberEmail": "string",
  "appMemberExPassword": "string",
  "appMemberNewPassword": "string"
}
```
**RequestFields**

| Name                          | Required | Description        |
|-------------------------------|----------|--------------------|
| appCode `String`              | `True`   | App 의 고유 Code 입니다. |
| appMemberEmail `String`       | `True`   | 인증을 확인할 Email 입니다. |
| appMemberExPassword `String`  | `True`   | 변경할 비밀번호 입니다.      |
| appMemberNewPassword `String` | `True`   | 변경할 비밀번호를 확인 합니다.  |

**Example:**

```bash
curl -X POST 'https://devapi.aiapp.link/api/app/member/auth' \
    -H 'Content-Type: application/json;charset=utf-8' \
    -H 'Accept: */*' \
    -d '{
  "appCode" : "testAppCode",
  "appMemberEmail" : "update@test.com",
  "appMemberExPassword" : "1234567",
  "appMemberNewPassword" : "1234567"
}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 비밀번호 변경 완료.
```json
{"result" : "SUCCESS", "message" : "비밀번호 변경 완료"}
```
---

### App 회원 회원가입

- **URL:** `/app/member/join`
- **Method:** `POST`
- **Description:** App 에 회원가입 합니다.


**Request Body:**

```json
{
  "appCode": "string",
  "appMemberEmail": "string",
  "appMemberPassword": "string",
  "appMemberPhone": "string",
  "appMemberName": "string",
  "appMemberType": "KAKAO",
  "appMemberPrivateAgree": "Y"
}
```
**RequestFields**

| Name                         | Required | Description        |
|------------------------------|----------|--------------------|
| appCode `String`             | `True`   | App 의 고유 Code 입니다. |
| appMemberEmail `String`      | `True`   | 회원의 Email 입니다.     |
| appMemberPassword `String`   | `True`   | 회원의 비밀번호 입니다.      |
| appMemberPhone `String`      | `True`   | 회원의 연락처 입니다.       |
| appMemberName `String`       | `True`   | 회원의 이름 입니다.        |
| appMemberType `Enum`         | `True`   | 회원가입 타입 입니다.       |
| appMemberPrivateAgree `Enum` | `True`   | 개인정보 제공 동의여부 입니다.  |

**appMemberType Enum Values**

| Name      | Description          |
|-----------|----------------------|
| `KAKAO`   | 카카오 소셜로그인 계정 회원가입 타입 |
| `GOOGLE`  | 구글 소셜로그인 걔정 회원가입 타입  |
| `APPLE`   | 애플 소셜로그인 계정 회원가입 타입  |
| `NAVER`   | 네이버 소셜로그인 계정 회원가입 타입 |
| `GENERAL` | 일반 계정 회원가입 타입        |

**appMemberPrivateAgree Enum Values**

| Name | Description |
|------|-------------|
| `Y`  | Yes         |
| `N`  | No          |


**Example:**

```bash
curl -X POST 'https://devapi.aiapp.link/api/app/member/join' \
    -H 'Content-Type: application/json;charset=utf-8' \
    -H 'Accept: */*' \
    -d '{
  "appMemberEmail" : "register@test.com",
  "appMemberPassword" : "123456",
  "appMemberPhone" : "01091097122",
  "appMemberName" : "회원가입테스트",
  "appMemberType" : "GENERAL",
  "appCode" : "testAppCode",
  "appMemberPrivateAgree" : "Y"
}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 회원가입 완료.
```json
{"result" : "SUCCESS", "message" : "회원가입 완료"}
```

---

### App 회원 로그인

- **URL:** `/app/member/join`
- **Method:** `POST`
- **Description:** App 에 회원가입 합니다.


**Request Body:**

```json
{
  "appMemberEmail" : "test@test.com",
  "appMemberPassword" : "123456",
  "appCode" : "testAppCode",
  "appMemberType" : "GENERAL"
}
```
**RequestFields**

| Name                       | Required | Description        |
|----------------------------|----------|--------------------|
| appCode `String`           | `True`   | App 의 고유 Code 입니다. |
| appMemberEmail `String`    | `True`   | 회원의 Email 입니다.     |
| appMemberPassword `String` | `True`   | 회원의 비밀번호 입니다.      |
| appMemberType `Enum`       | `True`   | 로그인 타입 입니다.        |

**appMemberType Enum Values**

| Name      | Description          |
|-----------|----------------------|
| `KAKAO`   | 카카오 소셜로그인 계정 회원가입 타입 |
| `GOOGLE`  | 구글 소셜로그인 걔정 회원가입 타입  |
| `APPLE`   | 애플 소셜로그인 계정 회원가입 타입  |
| `NAVER`   | 네이버 소셜로그인 계정 회원가입 타입 |
| `GENERAL` | 일반 계정 회원가입 타입        |

**Example:**

```bash
curl -X POST 'https://api.aiapp.link/api/app/member/login' \
    -H 'Content-Type: application/json;charset=utf-8' \
    -H 'Accept: */*' \
    -d '{
  "appMemberEmail" : "test@test.com",
  "appMemberPassword" : "123456",
  "appCode" : "testAppCode",
  "appMemberType" : "GENERAL"
}'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 회원가입 완료.
```json
{
  "result" : "SUCCESS",
  "data" : {
    "accessToken" : "eyJhbGciOiJIUzUxMiJ9.eyJhcHBNZW1iZXJJZHgiOjEsImFwcENvZGUiOiJ0ZXN0QXBwQ29kZSIsImFwcE1lbWJlck5hbWUiOiLthYzsiqTtirgg7ZqM7JuQIiwiYXBwTWVtYmVyQ29kZSI6InRlc3RBcHBNZW1iZXJDb2RlIiwiZXhwIjoxNzIxMjAxMjExfQ.o2wvn8_kKRPOrC5MDnM5XysPEPfNtsW6LA3MZmlHDUlvkgT8evM5OosD9hpEIXxbSERTSIcmB8Dy9dKY1epxtw"
  },
  "message" : "로그인 완료"
}
```

---


### App 회원 내 정보

- **URL:** `/app/member/info`
- **Method:** `GET`
- **Description:** App 회원 내 정보를 가져옵니다.

**RequestHeader**

| Name            | Description    |
|-----------------|----------------|
| `Authorization` | 로그인 회원의 JWT 토큰 |


**Example:**

```bash
curl -X GET 'https://api.aiapp.link/api/app/member/info' \
    -H 'Content-Type: application/json;charset=utf-8' \
    -H 'Authorization: Bearer {token}}' \
    -H 'Accept: */*'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 내 정보.
```json
{
  "result" : "SUCCESS",
  "data" : {
    "appMemberEmail" : "test@test.com",
    "appMemberPhone" : "01087654321",
    "appMemberCode" : "testAppMemberCode",
    "appMemberName" : "테스트 회원",
    "appCode" : "testAppCode",
    "appMemberProfileUrl" : "testURL",
    "appMemberType" : "GENERAL",
    "appMemberStatus" : "GREEN"
  },
  "message" : "내 정보"
}
```
**appMemberType Enum Values**

| Name      | Description          |
|-----------|----------------------|
| `KAKAO`   | 카카오 소셜로그인 계정 회원가입 타입 |
| `GOOGLE`  | 구글 소셜로그인 걔정 회원가입 타입  |
| `APPLE`   | 애플 소셜로그인 계정 회원가입 타입  |
| `NAVER`   | 네이버 소셜로그인 계정 회원가입 타입 |
| `GENERAL` | 일반 계정 회원가입 타입        |

**appMemberStatus Enum Values**

| Name     | Description |
|----------|-------------|
| `GREEN`  | 활동 상태       |
| `YELLOW` | 정지 상태       |
| `BLUE`   | 휴면 상태       |
| `RED`    | 탈퇴 상태       |
| `BLACK`  | 강퇴 상태       |

---


### App 회원 프로필 등록 & 수정

- **URL:** `/app/member/info`
- **Method:** `POST`
- **Description:** App 회원 내 정보를 가져옵니다.

**RequestHeader**

| Name            | Description    |
|-----------------|----------------|
| `Authorization` | 로그인 회원의 JWT 토큰 |


**QueryParameters**

| Name                       | Required | Description |
|----------------------------|----------|-------------|
| file `multipart/form-data` | `True`   | 프로필 이미지.    |

**Example:**

```bash
curl -X POST 'https://api.aiapp.link/api/app/member/info/profile' \
    -H 'Content-Type: multipart/form-data;charset=UTF-8' \
    -H 'Authorization: Bearer {token}}' \
    -F 'file=test.png;type=multipart/form-data'
```

**Responses Body:**

- **Status Code:** `200`
- **Description:** 프로필 이미지 등록.
```json
{
  "result" : "SUCCESS",
  "data" : "fileUrl",
  "message" : "프로필 등록 완료"
}

```

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

#### System

| Error Code                     | Status Code | Description                      |
|--------------------------------|-------------|----------------------------------|
| `COMMON_INTERNAL_SERVER_ERROR` | `500`       | 잘못된 접근입니다. 관리자에게 문의하세요.          |
| `COMMON_ENCRYPT_ERROR`         | `500`       | 암호화 에러                           |
| `COMMON_SYSTEM_ERROR`          | `500`       | 일시적인 오류가 발생했습니다. 잠시 후 다시 시도해주세요. |
| `COMMON_BAD_REQUEST`           | `400`       | 잘못된 요청입니다.                       |
| `COMMON_NON_UNIQUE`            | `404`       | 잘못된 요청입니다. 관리자에게 문의하세요.          |
| `COMMON_UNAUTHORIZED`          | `401`       | 권한이 없습니다.                        |

#### Request

| Error Code                 | Status Code | Description       |
|----------------------------|-------------|-------------------|
| `COMMON_INVALID_PARAMETER` | `400`       | 요청한 값이 올바르지 않습니다. |
| `COMMON_ENTITY_NOT_FOUND`  | `404`       | 존재하지 않는 엔티티입니다.   |
| `COMMON_ILLEGAL_STATUS`    | `400`       | 잘못된 상태값입니다.       |
| `COMMON_FORBIDDEN`         | `403`       | 유저 요청 권한이 없습니다.   |

#### Auth Email

| Error Code               | Status Code | Description         |
|--------------------------|-------------|---------------------|
| `COMMON_AUTH_EMAIL_TIME` | `200`       | 이메일 인증 시간이 만료되었습니다. |
| `COMMON_AUTH_EMAIL`      | `200`       | 이메일 인증을 해주세요.       |
| `COMMON_DUPLICATE_ID`    | `200`       | 이미 존재하는 이메일입니다.     |

#### Member

| Error Code           | Status Code | Description                                 |
|----------------------|-------------|---------------------------------------------|
| `COMMON_NO_ID`       | `200`       | 아이디를 입력하세요.                                 |
| `COMMON_NO_PW`       | `200`       | 비밀번호를 입력하세요.                                |
| `COMMON_NO_LOGIN`    | `200`       | 로그인 하세요.                                    |
| `MEMBER_NOT_FOUND`   | `200`       | 존재하지 않는 회원입니다.                              |
| `MEMBER_LOGIN_FAIL`  | `200`       | 아이디 또는 비밀번호를 잘못 입력했습니다. 입력하신 내용을 다시 확인해주세요. |
| `COMMON_NO_MATCH_PW` | `200`       | 재입력한 비밀번호와 일치하지 않습니다.                       |


#### App

| Error Code                      | Status Code | Description                    |
|---------------------------------|-------------|--------------------------------|
| `APP_OVER_COUNT`                | `200`       | 3개 이상의 앱을 만들 수 없습니다.           |
| `APP_DUPLICATE_PROJECT`         | `200`       | 이미 존재하는 프로젝트 명입니다.             |
| `APP_PROJECT_NAME_PATTERN_FAIL` | `200`       | 대문자나 한글은 프로젝트 이름으로 사용할 수 없습니다. |
| `APP_NAME_PATTERN_FAIL`         | `200`       | 앱 이름은 영문이나 한글 숫자만 사용 가능합니다.    |
| `APP_CODE_NOT_FOUND`            | `200`       | 앱이 존재하지 않거나 사용 중이 아닙니다.        |
| `APP_ICON_NOT_FOUND`            | `200`       | 앱의 해당 아이콘을 찾을 수 없습니다.          |
| `APP_MEMBER_NOT_FOUND`          | `200`       | 존재하지 않는 앱 회원입니다.               |
| `APP_GROUP_NOT_FOUND`           | `200`       | 존재하지 않는 앱 그룹입니다.               |

#### Company

| Error Code           | Status Code | Description      |
|----------------------|-------------|------------------|
| `COMPANY_NO_DATA`    | `200`       | 앱에 등록된 회사가 없습니다. |
| `COMPANY_NO_ADDRESS` | `200`       | 주소를 입력하세요.       |

#### Token

| Error Code                | Status Code | Description        |
|---------------------------|-------------|--------------------|
| `COMMON_JWT_UNAUTHORIZED` | `401`       | 접근 권한이 없음. 토큰이 없음  |
| `COMMON_JWT_MAL_FORM`     | `400`       | 잘못된 JWT 토큰입니다.     |
| `COMMON_JWT_EXPIRED`      | `401`       | 만료된 JWT 토큰입니다.     |
| `COMMON_JWT_UNSUPPORTED`  | `400`       | 지원되지 않는 JWT 토큰입니다. |
| `COMMON_JWT_ILLEGAL`      | `400`       | JWT 토큰이 잘못되었습니다.   |


#### FeignClient

| Error Code             | Status Code | Description  |
|------------------------|-------------|--------------|
| `COMMON_LIMIT_REQUEST` | `429`       | 요청이 초과되었습니다. |

#### Status

| Error Code           | Status Code | Description   |
|----------------------|-------------|---------------|
| `MEMBER_BAN_NO_DATE` | `200`       | 정지 기한을 정해주세요. |

## 자주 묻는 질문

### Q: 인증은 어떻게 하나요?
A: `Authorization` 헤더에 Bearer 토큰을 보내야 합니다.

### Q: 요청 본문은 어떤 형식이어야 하나요?
A: 이미지 업로드를 제외한 모든 요청 본문은 `JSON` 형식이어야 합니다.