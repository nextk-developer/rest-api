---
layout: default
title: 채널 관리
nav_order: 4
parent: v2
has_children: false
# permalink: /docs/v2
---


채널에 대한 API입니다. 채널은 1개의 비디오에 대한 정보이며, 영상분석을 수행하는 단위입니다.


----

<br><br>

# 채널 등록하기

비디오 분석을 수행할 채널을 등록합니다.

<br>

### Request
```
POST /v2/va/register-channel

{
  "nodeId": "5c009c52",
  "channelName": "TEST_CHANNEL_NAME",
  "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
  "inputType": null,
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelName | String | 채널 별칭 | O |
| inputUri | String | 입력 영상 URI (RTSP 주소, 파일 경로) | O |
| inputType | Enum | 입력 영상 종류 (**[InputType](models.md#inputtype)**) | O |


<br>

### Response
```
// Ok
{
    "channelId": "X1ashF0t",
    "code": 0,
}
// Fail
{
    "code": 400,
    "message": "Authentication failed"
}
```
| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | String | 채널 ID |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

<!-- ### Remarks

#### nodeId
채널의 입력 영상에 대해 비디오 분석을 수행 할 컴퓨팅 노드의 ID 입니다. 비디오 분석을 수행하기 위해서는 최소 1개의 컴퓨팅 노드가 필요합니다. -->

<!-- #### siblings

동일한 목표지점을 촬영하는 채널인 경우, sibling 관계가 될 수 있습니다. 예를 들어, 같은 위치에서 같은 목표지점을 촬영하도록 일반카메라와 열화상카메라 CCTV가 각각 설치 된 경우입니다. 이 때, 두 CCTV 영상들의 분석결과는 서로 상관관계가 있으므로, 이것을 응용 앱에서 활용하기 위해 본 파라메터를 이용하여 sibling 관계를 관리할 수 있습니다. -->

<br><br>

# 채널 보기
채널의 상세 정보를 조회합니다.

<br>

### Request
```
POST /v2/va/get-channel

{
  "nodeId": "5c009c52",
  "channelId": "X1ashF0t"
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |

<br>

### Response
```
//Ok
{
  "channelId": "6a694f0e",
  "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
  "channelName": "TEST_CHANNEL_NAME",
  "inputType": 0,
  "status": 0,
  "code": 0,
}

//Fail
{
    "code" : 202
    "message" : "ChannelId not exists"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | string | 채널 ID |
| inputUri | string | 입력 영상 주소 |
| channelName | string | 채널 이름 |
| inputType | int | 입력 영상 종류(**[InputType](models.md#inputtype)**) |
| status | Enum | 채널 상태 (**[ChannelStatus](#channelstatus)**)|


<br><br>

# 채널 목록보기
전체 채널 상세정보를 조회합니다.

```
POST /v2/va/list-channel

{
    "nodeId" : "5c009c52"
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
<br>


### Response
```
{ 
    "channels" : [
        {
            "channelId": "6a694f0e",
            "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
            "channelName": "TEST_CHANNEL_NAME",
            "inputType": 0,
            "status": 0
        },
        {
            "channelId": "6a694f0e",
            "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
            "channelName": "TEST_CHANNEL_NAME",
            "inputType": 0,
            "status": 0
        }
    ]
}
```
"[Channel](models.md#channel)"의 배열을 반환합니다.

<br><br>

# 채널 수정하기
채널의 정보를 수정합니다.

<br>

### Request

```
POST /v2/va/update-channel

{
  "nodeId" : "5c009c52"
  "channelId": "6a694f0e",
  "inputUri": "rtsp://192.168.0.70/vod/pertest_5m_15m_fall",
  "channelName": "TEST_CHANNEL_NAME",
  "inputType": 0
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelId | String | 채널 ID | O |
| inputUri | String | 입력 비디오 URI(RTSP 주소 또는 로컬파일 경로) | X |
| channelName | String | 채널 별칭 | X |
| inputType | Enum | 입력 비디오 타입 (**[InputType](models.md#inputtype)**) | X |

<br>

### Response
```
// Ok
{
  "channelId": "6a694f0e",
  "code": 0
}

// Fail
{
   "code": 400,
   "message" : "Not Found ChannelId"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br><br>

# 채널 삭제하기
채널의 정보를 삭제합니다.
<br>

### Request

```
POST /v2/va/remove-channel

{
    "nodeId" : "5c009c52",
    "channelId": "6a694f0e",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | string | 컴퓨팅 노드 ID | O |
| channelId | string | 채널 ID | O |

<br>

### Response

```
// Ok
{
  "channelId": "8cc0a5ec",
  "code": 0
}
// Fail
{
  "code": 404,
  "message": "not founded channel"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br>

### Remarks
비디오 분석이 실행 중인 채널은 삭제할 수 없으며, 삭제하려면 먼저 분석 실행을 중단해야 합니다.

<br><br>

# 영상 캘리브레이션

해당 채널의 영상 좌표 정보를 획득하여, 좌표 왜곡 보정 기능을 지원합니다.<p>
* 캘리브레이션 지원 라이센스를 발급 받아야 사용 가능합니다.(현재 개발중)
* 추가 객체 실제사이즈,거리 및 추적 성능 개선이 가능합니다.

<br>

### Request
```
POST /v2/va/callibrate

{
    "nodeId" : "5c009c52",
    "channelId": "6a694f0e",
    "firstLine" : 
    {
        "startPointX" : 0.3,
        "startPointY" : 0.1,
        "endPointX" : 0.35,
        "endPointY" : 0.6,
    },
    "secondLine" : 
    {
        "startPointX" : 0.7,
        "startPointY" : 0.3,
        "endPointX" : 0.76,
        "endPointY" : 0.72,
    }
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |
| firstLine | JsonObject | 왜곡 보정을 위한 첫번째 직선 (**[Line](#Line)**)| O |
| secondLine | JsonObject | 왜곡 보정을 위한 두번째 직선 (**[Line](#Line)**)| O |

### Line ###
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| startPointX | double | 시작 위치 X좌표 | O |
| startPointY | double | 시작 위치 X좌표 | O |
| endPointX | double | 종료 위치 X좌표 | O |
| endPointY | double | 종료 위치 X좌표 | O |

<br>

### Response
```
// Ok
{
    "channelId": "6a694f0e",
    "code" : 0
}

// Fail
{
    "code" : 204,
    "messgae" : "failed create focal length"
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |

<br><br>

# 스냅샷

채널의 영상 스냅샷을 반환합니다.

<br>

### Request
```
POST /v2/va/snapshot

{
    "channelId" : "6a694f0e"
}
```
| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| channelId | String | 채널 ID | O |

<br>

### Response
```
// Ok
{
    "imageData" : "x35hj34Bd239...."
    "code" : 0
}

// Fail
{
    "code": 1,
    "message": "Channel X1ashF0t not exists"
}
```
| Name | Type | Description |
| :---- | :---- |:---- |
| imageData | String | 영상 데이터 (jpeg -> base64인코딩) |
| code | Integer | 오류 코드 (**[Error Code](models.md#error-code)**) |
| message | String | 오류 메시지 |