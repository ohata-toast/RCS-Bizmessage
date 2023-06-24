## Notification > RCS Bizmessage > API v1.0 Guide

## v1.0 API 소개
### [API 도메인]
```
https://rcs-bizmessage.api.nhncloudservice.com
```

## 메시지 발송

### SMS 타입 발송
[Method, URI]

```
POST /rcs/v1.0/messages/sms
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String,
"X-SECRET-KEY": String
```

[Request Body]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| sendDateTime | String | X | 발송 희망 시간 | 형식 : yyyy-MM-dd HH:mm:ss <br>현재 이전 시간 불가, 기본값: 현재 시간 |
| brandId | String | O | 브랜드 ID |  |
| chatbotId | String | O | 발신 번호 |  |
| recipientNumber | String | O | 수신 번호 |  |
| isAd | Boolean | X | 광고 발송 여부 | 기본값: false |
| unsubscribeNumber | String | X | 수신거부 번호 | 광고 여부 true인 경우, 필수 |
| body | String | O | 본문 | 최대 100자 |
| buttons | List | X | 버튼 | 최대 1개 |
| button.buttonType | String | X | 버튼 타입 | 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR) |
| button.buttonJson | String | X | 버튼 Json | 버튼 타입에 맞는 포맷 확인 |
| isFallback | Boolean | X | 대체 발송 여부 | 기본값: false |

* 요청 예시
```json
{
	"brandId":"sampleBrandId",
	"chatbotId":"15881234",
	"recipientNumber":"01012345678",
	"isAd": false,
	"body":"testBody",
	"buttons" : [
		{
			"buttonType" : "URL",
			"buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
		}
	]
}
```

[Response Body]

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "messageId" : "20220914184500weq0u9pNu30"
}
```
[실패 예시]
```json
{
    "header": {
        "resultCode": -3000,
        "resultMessage": "Invalid button parameter",
        "isSuccessful": false
    }
}
```
	

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |


### LMS 타입 발송
[Method, URI]

```
POST /rcs/v1.0/messages/lms
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String,
"X-SECRET-KEY": String
```

[Request Body]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| sendDateTime | String | X | 발송 희망 시간 | 형식 : yyyy-MM-dd HH:mm:ss <br>현재 이전 시간 불가, 기본값: 현재 시간 |
| brandId | String | O | 브랜드 ID |  |
| chatbotId | String | O | 발신 번호 |  |
| recipientNumber | String | O | 수신 번호 |  |
| isAd | Boolean | X | 광고 발송 여부 | 기본값: false |
| unsubscribeNumber | String | X | 수신거부 번호 | 광고 여부 true인 경우, 필수 |
| title | String | X | 제목 | 최대 30자 |
| body | String | O | 본문 | 최대 1300자 |
| buttons | List | X | 버튼 | 최대 3개 |
| button.buttonType | String | X | 버튼 타입 | 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR) |
| button.buttonJson | String | X | 버튼 Json | 버튼 타입에 맞는 포맷 확인 |
| isFallback | Boolean | X | 대체 발송 여부 | 기본값: false |

* 요청 예시
```json
{
	"brandId":"sampleBrandId",
	"chatbotId":"15881234",
	"recipientNumber":"01012341234",
	"isAd": false,
    "title":"testTitle",
	"body":"testBody",
	"buttons" : [
		{
			"buttonType" : "URL",
			"buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
		}
	]
}
```

[Response Body]

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "messageId" : "20220914184500weq0u9pNu30"
}
```
[실패 예시]
```json
{
    "header": {
        "resultCode": -3000,
        "resultMessage": "Invalid button parameter",
        "isSuccessful": false
    }
}
```
	

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |

### MMS 타입 발송
[Method, URI]

```
POST /rcs/v1.0/messages/mms
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String,
"X-SECRET-KEY": String
```

[Request Body]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| sendDateTime | String | X | 발송 희망 시간 | 형식 : yyyy-MM-dd HH:mm:ss <br>현재 이전 시간 불가, 기본값: 현재 시간 |
| brandId | String | O | 브랜드 ID |  |
| chatbotId | String | O | 발신 번호 |  |
| recipientNumber | String | O | 수신 번호 |  |
| isAd | Boolean | X | 광고 발송 여부 | 기본값: false |
| unsubscribeNumber | String | X | 수신거부 번호 | 광고 여부 true인 경우, 필수 |
| mmsType | String | O | MMS 타입 | 가로형(HORIZONTAL), 세로형(VERTICAL), 슬라이드 중형(CAROUSEL_MEDIUM), 슬라이드 소형(CAROUSEL_SMALL) |
| cards | List | O | 카드들 | HORIZONTAL(1), VERTICAL(1), CAROUSEL_MEDIUM(3 ~ 6), CAROUSEL_SMALL(3 ~ 6) |
| card.title | String | X |  제목 | 최대 30자 |
| card.description | String | X | 내용 | 슬라이드 X(최대:1300), CAROUSEL_MEDIUM(최대:60), CAROUSEL_SMALL(MAX:30) |
| card.media | String | O | 첨부파일 ID | 첨부파일 업로드 시, 발급되는 ID 값 |
| buttons | List | X | 버튼 | 최대 2개 |
| button.buttonType | String | X | 버튼 타입 | 대화방 열기(COMPOSE), 복사하기(CLIPBOARD), 전화 걸기(DIALER), 지도 보여주기(MAP_SHOW), 지도 검색하기(MAP_QUERY), 현재 위치 공유하기(MAP_SHARE), URL 연결하기(URL), 일정 등록하기(CALENDAR) |
| button.buttonJson | String | X | 버튼 Json | 버튼 타입에 맞는 포맷 확인 |
| isFallback | Boolean | X | 대체 발송 여부 | 기본값:false |

* 요청 예시
```json
{
	"brandId":"sampleBrandId",
	"chatbotId":"15881234",
	"recipientNumber":"01012341234",
	"isAd": false,
    "mmsType": "HORIZONTAL",
	"cards": [
        {
          "title":"testTitle",
          "description":"testBody",
          "media":"fileId",
          "buttons" : [
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            },
            {
              "buttonType" : "URL",
              "buttonJson" : "{ \"action\": { \"urlAction\":{\"openUrl\":{\"url\":\"http://www.test.com\"} },\"displayText\":\"홈페이지로 이동\"}}"
            }
          ]
        }
    ]
}
```


[Response Body]

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "messageId" : "20220914184500weq0u9pNu30"
}
```
[실패 예시]
```json
{
    "header": {
        "resultCode": -3000,
        "resultMessage": "Invalid button parameter",
        "isSuccessful": false
    }
}
```
	

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |

### Template 타입 발송
[Method, URI]

```
POST /rcs/v1.0/messages/template
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String,
"X-SECRET-KEY": String
```

[Request Body]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| sendDateTime | String | X | 발송 희망 시간 | 형식 : yyyy-MM-dd HH:mm:ss <br>현재 이전 시간 불가, 기본값: 현재 시간 |
| brandId | String | O | 브랜드 ID |  |
| chatbotId | String | O | 발신 번호 |  |
| messagebaseId  | String | O | 템플릿 ID | |
| recipientNumber | String | O | 수신 번호 |  |
| body | String | X | 본문 | 최대 90자, Free 템플릿인 경우에만 해당 |
| templateParameter | Map | X | 치환자 key, value |
| isFallback | Boolean | X | 대체 발송 여부 |  |

* 요청 예시
```json
{
	"sendDateTime" : "2022-11-21 00:00:00",
	"brandId":"sampleBrandId",
	"chatbotId":"15881234",
    "messagebaseId":"UBR.AGNtIngI0u-GG000F",
    "templateParameter" : {
        "key1":"value1"
    },
	"recipientNumber":"01012341234"
}
```

[Response Body]

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "messageId" : "20220914184500weq0u9pNu30"
}
```
[실패 예시]
```json
{
    "header": {
        "resultCode": -3000,
        "resultMessage": "Invalid button parameter",
        "isSuccessful": false
    }
}
```
	

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |

## 메시지 조회

### SMS 메시지 조회 API
[Method, URI]
```
GET /rcs/v1.0/messages/sms
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String
"X-SECRET-KEY" : String
```

[Query Parameter]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| messageId | String | O(선택적 필수) | 메시지 ID | 요청 시 발급되는 메시지 ID |
| brandId | String | X | 브랜드 ID |  |
| chatbotId | String | X | 발신 번호 |  |
| messageStatus | String | X | 메시지 상태 | READY, IN_PROGRESS, DELIVERED, FAILED, CANCELED |
| startSendDateTime | String | O(선택적 필수) | 요청 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endSendDateTime | String | O(선택적 필수) | 요청 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| startReceiveDateTime | String | O(선택적 필수) | 수신 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endReceiveDateTime | String | O(선택적 필수) | 수신 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| limit | Integer | X | Limit | 기본값: 15 max : 1000 |
| offset | Integer | X | offset | 기본값: 0 |

* messageId 또는 startSendDateTime / endSendDateTime 또는 startReceiveDateTime / endReceiveDateTime 중 1개를 필수로 입력해야 합니다.
* 요청 시간과 수신 시간 날짜를 동시에 검색은 불가능합니다.


[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "data": [
        {
            "messageId": "20230503100623Uc3C0JDd0u0",
            "recipientSequence": 0,
            "messageType": "SMS",
            "brandId": "sampleBrandId",
            "chatbotId": "15881234",
            "recipientNumber": "01012341234",
            "messagebaseId": "SS000000",
            "title": "",
            "body": "testBody",
            "messageStatus": "DELIVERED",
            "sendDateTime": "2023-05-03T10:06:23.000+09:00"
        }
    ],
    "pagination": {
        "offset": 0,
        "limit": 15,
        "total": 1
    }
}
```


[실패 예시]
```json
{
    "header": {
        "resultCode": 500,
        "resultMessage": "Internal Error. It is not handled. Please report this. 'https://toast.com/support/inquiry.",
        "isSuccessful": false
    }
}
```

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |
| data | - | 메시지 정보 |
| data.messageId | String | 메시지 ID |
| data.recipientSeq | Integer | 수신자 순서 | 
| data.messageType | String | 메시지 타입 |
| data.brandId | String | 브랜드 ID|
| data.chatbotId | String | 챗봇 ID | 
| data.recipientNumber | String | 수신자 번호 |
| data.messagebaseId | String | 메시지 타입 |
| data.title | String | 제목 |
| data.body | String | 본문 |
| data.messageStatus | String | 메시지 상태 |
| sendDateTime | dateTime | 요청 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) | 
| receiveDateTime | dateTime | 수신 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) |


### LMS 메시지 조회 API
[Method, URI]

```
GET /rcs/v1.0/messages/lms
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String
"X-SECRET-KEY" : String
```

[Query Parameter]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| messageId | String | O(선택적 필수) | 메시지 ID | 요청 시 발급되는 메시지 ID |
| brandId | String | X | 브랜드 ID |  |
| chatbotId | String | X | 발신 번호 |  |
| messageStatus | String | X | 메시지 상태 | READY, IN_PROGRESS, DELIVERED, FAILED, CANCELED |
| startSendDateTime | String | O(선택적 필수) | 요청 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endSendDateTime | String | O(선택적 필수) | 요청 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| startReceiveDateTime | String | O(선택적 필수) | 수신 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endReceiveDateTime | String | O(선택적 필수) | 수신 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| limit | Integer | X | Limit | 기본값: 15 max : 1000 |
| offset | Integer | X | offset | 기본값: 0 |

* messageId 또는 startSendDateTime / endSendDateTime 또는 startReceiveDateTime / endReceiveDateTime 중 1개를 필수로 입력해야 합니다.
* 요청 시간과 수신 시간 날짜를 동시에 검색은 불가능합니다.

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "data": [
        {
            "messageId": "20230503100623Uc3C0JDd0u0",
            "recipientSequence": 0,
            "messageType": "LMS",
            "brandId": "sampleBrandId",
            "chatbotId": "15881234",
            "recipientNumber": "01012341234",
            "messagebaseId": "SS000000",
            "title": "",
            "body": "testBody",
            "messageStatus": "DELIVERED",
            "sendDateTime": "2023-05-03T10:06:23.000+09:00"
        }
    ],
    "pagination": {
        "offset": 0,
        "limit": 15,
        "total": 1
    }
}
```


[실패 예시]
```json
{
    "header": {
        "resultCode": 500,
        "resultMessage": "Internal Error. It is not handled. Please report this. 'https://toast.com/support/inquiry.",
        "isSuccessful": false
    }
}
```

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |
| data | - | 메시지 정보 |
| data.messageId | String | 메시지 ID |
| data.recipientSeq | Integer | 수신자 순서 | 
| data.messageType | String | 메시지 타입 | 
| data.brandId | String | 브랜드 ID|
| data.chatbotId | String | 챗봇 ID | 
| data.recipientNumber | String | 수신자 번호 |
| data.messagebaseId | String | 메시지 타입 |
| data.title | String | 제목 |
| data.body | String | 본문 |
| data.messageStatus | String | 메시지 상태 |
| sendDateTime | dateTime | 요청 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) | 
| receiveDateTime | dateTime | 수신 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) |

### MMS 메시지 조회 API
[Method, URI]

```
GET /rcs/v1.0/messages/mms
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String
"X-SECRET-KEY" : String
```

[Query Parameter]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| messageId | String | O(선택적 필수) | 메시지 ID | 요청 시 발급되는 메시지 ID |
| brandId | String | X | 브랜드 ID |  |
| chatbotId | String | X | 발신 번호 |  |
| messageStatus | String | X | 메시지 상태 | READY, IN_PROGRESS, DELIVERED, FAILED, CANCELED |
| startSendDateTime | String | O(선택적 필수) | 요청 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endSendDateTime | String | O(선택적 필수) | 요청 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| startReceiveDateTime | String | O(선택적 필수) | 수신 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endReceiveDateTime | String | O(선택적 필수) | 수신 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| limit | Integer | X | Limit | 기본값: 15 max : 1000 |
| offset | Integer | X | offset | 기본값: 0 |

* messageId 또는 startSendDateTime / endSendDateTime 또는 startReceiveDateTime / endReceiveDateTime 중 1개를 필수로 입력해야 합니다.
* 요청 시간과 수신 시간 날짜를 동시에 검색은 불가능합니다.

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "data": [
        {
            "messageId": "20230503100623Uc3C0JDd0u0",
            "recipientSequence": 0,
            "messageType": "MMS",
            "brandId": "sampleBrandId",
            "chatbotId": "15881234",
            "recipientNumber": "01012341234",
            "messagebaseId": "SS000000",
            "title": "",
            "body": "testBody",
            "messageStatus": "DELIVERED",
            "sendDateTime": "2023-05-03T10:06:23.000+09:00"
        }
    ],
    "pagination": {
        "offset": 0,
        "limit": 15,
        "total": 1
    }
}
```


[실패 예시]
```json
{
    "header": {
        "resultCode": 500,
        "resultMessage": "Internal Error. It is not handled. Please report this. 'https://toast.com/support/inquiry.",
        "isSuccessful": false
    }
}
```

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |
| data | - | 메시지 정보 |
| data.messageId | String | 메시지 ID |
| data.recipientSeq | Integer | 수신자 순서 | 
| data.messageType | String | 메시지 타입 |
| data.brandId | String | 브랜드 ID|
| data.chatbotId | String | 챗봇 ID | 
| data.recipientNumber | String | 수신자 번호 |
| data.messagebaseId | String | 메시지 타입 |
| data.title | String | 제목(첫번째 카드) |
| data.body | String | 본문(첫번째 카드) |
| data.messageStatus | String | 메시지 상태 |
| sendDateTime | dateTime | 요청 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) | 
| receiveDateTime | dateTime | 수신 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) |

### TEMPLATE 메시지 조회 API
[Method, URI]

```
GET /rcs/v1.0/messages/template
Content-Type: application/json
```

[Header]
```
"X-TC-APP-KEY" : String
"X-SECRET-KEY" : String
```

[Query Parameter]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| messageId | String | O(선택적 필수) | 메시지 ID | 요청 시 발급되는 메시지 ID |
| brandId | String | X | 브랜드 ID |  |
| chatbotId | String | X | 발신 번호 |  |
| messageStatus | String | X | 메시지 상태 | READY, IN_PROGRESS, DELIVERED, FAILED, CANCELED |
| startSendDateTime | String | O(선택적 필수) | 요청 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endSendDateTime | String | O(선택적 필수) | 요청 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| startReceiveDateTime | String | O(선택적 필수) | 수신 시간 from | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| endReceiveDateTime | String | O(선택적 필수) | 수신 시간 to | 형식 : yyyy-MM-dd HH:mm:ss <br>from ~ to 최대 31일 |
| limit | Integer | X | Limit | 기본값: 15 max : 1000 |
| offset | Integer | X | offset | 기본값: 0 |

* messageId 또는 startSendDateTime / endSendDateTime 또는 startReceiveDateTime / endReceiveDateTime 중 1개를 필수로 입력해야 합니다.
* 요청 시간과 수신 시간 날짜를 동시에 검색은 불가능합니다.

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "data": [
        {
            "messageId": "20230503100623Uc3C0JDd0u0",
            "recipientSequence": 0,
            "messageType": "TEMPLATE",
            "brandId": "sampleBrandId",
            "chatbotId": "15881234",
            "recipientNumber": "01012341234",
            "messagebaseId": "SS000000",
            "title": "",
            "body": "testBody",
            "messageStatus": "DELIVERED",
            "sendDateTime": "2023-05-03T10:06:23.000+09:00"
        }
    ],
    "pagination": {
        "offset": 0,
        "limit": 15,
        "total": 1
    }
}
```


[실패 예시]
```json
{
    "header": {
        "resultCode": 500,
        "resultMessage": "Internal Error. It is not handled. Please report this. 'https://toast.com/support/inquiry.",
        "isSuccessful": false
    }
}
```

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |
| data | - | 메시지 정보 |
| data.messageId | String | 메시지 ID |
| data.recipientSeq | Integer | 수신자 순서 | 
| data.messageType | String | 메시지 타입 |
| data.brandId | String | 브랜드 ID|
| data.chatbotId | String | 챗봇 ID | 
| data.recipientNumber | String | 수신자 번호 |
| data.messagebaseId | String | 템플릿 ID |
| data.title | String | 제목 |
| data.body | String | 본문 |
| data.messageStatus | String | 메시지 상태 |
| sendDateTime | dateTime | 요청 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) | 
| receiveDateTime | dateTime | 수신 시간(yyyy-MM-ddThh:mm:ss.SSS+09:00) |

## 리소스 API

### 첨부파일 업로드 API
[Method, URI]

```
POST /rcs/v1.0/media
Content-Type: multipart/form-data
```

[Header]
```
"X-TC-APP-KEY" : String
"X-SECRET-KEY" : String
```

* 첨부파일 유효기간은 7일 입니다.
* 파일 용량제한은 1MB입니다.
* 이미지 첨부는 'jpg', 'jpeg', 'png', 'gif', 'bmp' 확장자만 지원합니다.

[Request Body]

| 필드 | 타입 | 필수 여부 | 설명 | 비고 |
| --- | --- | --- | --- | --- |
| uploadFile | MultipartFile | O | 첨부 파일 |  |
| uploadUser | String | X | 업로드 사용자 명 |  |

[Response Body]

[성공 예시]
```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    }
}
```

[실패 예시]
```json
{
    "header": {
        "resultCode": 500,
        "resultMessage": "Internal Error. It is not handled. Please report this. 'https://toast.com/support/inquiry.",
        "isSuccessful": false
    }
}
```

| 필드 | 타입 | 설명 |
| --- | --- | --- |
| header.resultCode | Integer | 결과 코드 |
| header.resultMessage | String | 결과 메시지 |
| header.isSuccessful | Boolean | 성공 여부 |


## 버튼 유형

### 대화방 열기

```json
{
    "action": {
        "composeAction": {
            "composeTextMessage": {
                "phoneNumber": "01000000000",
                "text": "전송할 메시지"
            }
        },
        "displayText": "대화방 열기"
    }
}
```


| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.composeAction.composeTextMessage.phoneNumber | 메시지 수신 번호 | |
| action.composeAction.composeTextMessage.text | 전송할 메시지 | 최대 100자 |

### 복사하기

```json
{
    "action": {
        "clipboardAction": {
            "copyToClipboard": {
                "text": "복사할 메시지"
            }
        },
        "displayText": "복사하기"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.clipboardAction.copyToClipboard.text | 클립보드로 복사할 내용 | 최대 200자 |

### 전화 걸기

```json
{
    "action": {
        "dialerAction": {
            "dialPhoneNumber": {
                "phoneNumber": "16446114"
            }
        },
        "displayText": "전화 걸기"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.dialerAction.dialPhoneNumber.phoneNumber | 전화 번호 | |

### 지도 보여주기

```json
{
    "action": {
        "mapAction": {
            "showLocation": {
                "location": {
                    "latitude": "37.400977",
                    "longitude": "127.104239",
                    "label": "NHN"
                },
                "fallbackUrl": "https://www.google.co.kr/maps"
            }
        },
        "displayText": "지도 보여주기"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.mapAction.showLocation.location.latitude | 위도 | |
| action.mapAction.showLocation.location.longitude | 경도 | |
| action.mapAction.showLocation.location.label | 위치 이름 | 최대 200자 |
| action.mapAction.showLocation.fallbackUrl | 액션 실패 시 호출 할 링크 | |

### 지도 검색하기

```json
{
    "action": {
        "mapAction": {
            "showLocation": {
                "location": {
                    "query": "NHN"
                },
                "fallbackUrl": "https://www.google.co.kr/maps"
            }
        },
        "displayText": "지도 검색하기"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.mapAction.showLocation.location.query | 검색 키워드 | 최대 200자 |
| action.mapAction.showLocation.fallbackUrl | 해당 위치를 조회할 사이트 | |

### 현재 위치 공유하기

```json
{
    "action": {
        "mapAction": {
            "requestLocationPush": {
                "currentLocation": true
            }
        },
        "displayText": "현재 위치 공유하기"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.mapAction.requestLocationPush.currentLocation | 현재위치 공유 여부 | 버튼의 기능을 정상적으로 사용하기 위해 해당 값은 true 로 지정되어야 함 |

### URL 연결하기

```json
{
    "action": {
        "urlAction": {
            "openUrl": {
                "url": "http://www.test.com"
            }
        },
        "displayText": "페이지로 이동"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.urlAction.openUrl.url | 연결할 URL 주소 | |

### 일정 등록하기

```json
{
    "action": {
        "calendarAction": {
            "createCalendarEvent": {
                "startTime": "2020-03-31T15:00:00.000Z",
                "endTime": "2020-03-31T15:00:00.000Z",
                "title": "일정 등록",
                "description": "기념일등록입니다."
            }
        },
        "displayText": "일정 등록하기"
    }
}
```

| 필드 | 설명 | 비고 |
| --- | --- | --- |
| action.displayText | 버튼 명 | 최대 17자 |
| action.calendarAction.createCalendarEvent.startTime | 시작일 | |
| action.calendarAction.createCalendarEvent.endTime | 종료일 | |
| action.calendarAction.createCalendarEvent.title | 제목 | 최대 17자 |
| action.calendarAction.createCalendarEvent.description | 내용 | 최대 500자 |
