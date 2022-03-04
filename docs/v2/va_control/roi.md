---
layout: default
title: ROI
nav_order: 2
parent: 영상 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/roi
---


영상 내 ROI(Region of interest) 설정 API입니다.

------------------------

# ROI 생성
지정한 채널에 관심 영역을 정의하고, 관심 영역 내 분석 알고리즘을 설정합니다.
(다각형 영역만을 지원)

<br>

### Request
```
POST /v2/va/create-roi

{
  "nodeId": "184fcb3c",
  "channelId": "72040f36",
  "eventType": "EVT_LOITERING",
  "roiName": "ROI_NAME",
  "description": "Loitering Event",
  "roiDots": [
    {
      "X": 0.0,
      "Y": 0.0
    },
    {
      "X": 1.0,
      "Y": 0.0
    },
    {
      "X": 1.0,
      "Y": 1.0
    },
    {
      "X": 0.0,
      "Y": 1.0
    }
  ],
  "eventFilter": {
    "objectsTarget":
    [
      "PERSON"
    ]
  }
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiName | String | 이벤트 이름 | O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| eventType | Enum | 영역 속성([EventType](models.md#EventType))| O |
| description | String | 관심 영역 설명 | X |
| eventFilter | JsonObject[] | 이벤트 상세 필터링 설정([EventFilter](models.md#EventFilter)) | X | 
<!-- | stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X | -->

<br/>

### Response
```
// Ok
{
  "roiId": "88e2a515",
  "code": 0
}
// Fail
{
    "code" : 300,
    "message" : "Failed Create Roi"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br/>

### Roi Dot

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| X | Integer | X 좌표 | O |
| Y | Integer | Y 좌표 | O |
| lineUntilNextDot | JsonObject[] | 검출 객체([RoiLine](#roi-line)) | O |

<br/>

### Roi Line

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| disable | boolean | 비활성화 | O |
| direction | String | 방향 설정 | O |
| target | JsonObject[] | 검출 객체([ObjectType](#object-type)) | O |

<br><br>

# ROI 조회
ROI를 조회합니다.
<br>

### Request
```
POST /v2/va/get-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiId": "88e2a515"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |

<br>

### Response
```
{
  "roiId": "88e2a515",
  "name": "ROI_NAME",
  "description": "Loitering Event",
  "stayTime": 0.0,
  "numberOf": 0,
  "eventType": "EVT_LOITERING",
  "roiDots": [
    {
      "x": 0.0,
      "y": 0.0
    },
    {
      "x": 1.0,
      "y": 0.0
    },
    {
      "x": 1.0,
      "y": 1.0
    },
    {
      "x": 0.0,
      "y": 1.0
    }
  ],
  "code": 0
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| roiNmae | String | 이벤트 이름 | O |
| description | String | 관심 영역 설명 | O |
| stayTime | Integer | 발생 지연 시간 | O |
| numberOf | Integer | 최소 발생 객체수 조건 | O |
| eventType | Enum | 영역 속성([EventType](models.md#EventType))| O |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | O |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) | O|
| message | String | 오류 메시지 |X|

<br><br>

# 채널 내 ROI 목록 조회
지정한 채널에 추가 된 모든 ROI들을 조회합니다.

<br>

### Request
```
POST /v2/va/list-roi

{
    "nodeId":"c6a45bc6"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |

<br>

### Response
```
{
  "channels": [
    {
      "channelId": "e84fcac4",
      "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
      "channelName": "TEST_CHANNEL_NAME",
      "inputType": 0,
      "status": 0
    }
  ],
  "code": 0
}
```

[ROI 조회](#roi-조회) 응답의 배열입니다.

<br><br>

# ROI 수정

(추적기 리셋 오류 발생중..)
ROI 설정을 수정합니다.

<br>

### Request

```
POST /v2/va/update-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiId": "88e2a515",
  "roiNmae" : "UPDATE_ROI",
  "roiDots": [
    {
      "x": 0.0,
      "y": 0.0
    },
    {
      "x": 0.84,
      "y": 0.0
    },
    {
      "x": 0.84,
      "y": 0.22
    },
    {
      "x": 0.0,
      "y": 0.5
    }
  ],
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String | 관심 영역 ID | O |
| roiNmae | String | 이벤트 이름 | X |
| description | String | 관심 영역 설명 | X |
| stayTime | Integer | 발생 지연 시간 | X |
| numberOf | Integer | 최소 발생 객체수 조건 | X |
| feature | string | 영역 속성([RoiFeature](#roi-feature)) | X |
| roiDots | JsonObject[] | ROI 라인 설정([RoiDot](#roi-dot)) | X |



<br>

### Response
```
{
    "roiId": "88e2a515",
    "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>

# ROI 삭제
ROI 설정을 삭제합니다.

### Request
```
POST /v2/va/remove-roi

{
  "nodeId": "c6a45bc6",
  "channelId": "e84fcac4",
  "roiIds": [
       "88e2a515",
       "19389bdc"
    ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| roiId | String[] | 관심 영역 ID | O |


<br>

### Response
```
{
  "roiId": "e84fcac4",
  "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| roiId | String | 관심 영역 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br><br>
