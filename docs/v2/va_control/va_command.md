---
layout: default
title: VA Control
nav_order: 3
parent: 영상 분석 설정
grand_parent: v2
permalink: /docs/v2/va_control/va_command
---

# 영상 분석 제어

이 API를 이용하여 지정 채널에 대해 영상 분석을 시작/중지/재시작을 할 수 있습니다. 

또한 영상 분석 중 누적 된 데이터들을 초기화 할 수 있습니다. 예를 들어, ROI 영역의 검출객체 누적 카운팅 값을 초기화 할 수 있습니다.

#### Request

```
POST /v2/va/control

# VA_START
{
    "nodeId":"a46147f4",
    "channelIds": ["19fa5688"],
    "operation": "VA_START"
}

# VA_STOP
{
    "nodeId":"a46147f4",
    "channelIds": ["19fa5688"],
    "operation": "VA_STOP"
}

# VA_RST
{
    "nodeId":"a46147f4",
    "channelIds" : ["X1ashF0t"],
    "operation" : "VA_RST",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| channelIds | String[] | 채널 ID 리스트 | O |
| parameter | String[] | 필요시 파라미터 전달 | X |

<br>

#### Response
```
//VA_START
{
  "sourceIp": "192.168.0.36",
  "sourcePort": 33300,
  "code": 0
}
//VA_STOP
{
  "code": 0
}
//VA_RESET
{
  "code": 0
}
//Fail
{
    "code" : 0,
    "message" : "reason"
}

```

| Name | Type | Description |
| :---- | :---- |:---- |
| sourceIp | String | Channel GRPC IP |
| sourcePort | Integer | Channel GRPC Port |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>

# 얼굴 등록

이 API를 이용하여 관심 얼굴을 지정 할 수 있습니다.

#### Request

```
POST /v2/va/register-facedb

{
    "nodeId":"6d286401",
    "faceImages":[
        "/9j/4AAQSkZJRgABAQEAYABgAAD/...",
        "/9j/4AAQSkZJRgABAQEAYABgAAD/...",
        "/9j/4AAQSkZJRgABAQEAYABgAAD/...",
        "/9j/4AAQSkZJRgABAQEAYABgAAD/..."
    ]
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID | O |
| faceImages | String[] | 등록 얼굴 이미지 (Jpeg -> Base64 Encoding) | O |

* TIP
1) 얼굴 등록 이미지는 1~4장 이미지 등록 가능 (2장 이상 권장)
2) 얼굴 등록 예시
<br>
<br>
<img src="../../../images/doc_regist_face.jpg" width="420px" height="100px" title="검출 이벤트 결과" alt="flowImage"/>
    * 이목구비 확인 및 정면이 아닐 경우 매칭 성능 저하 요인
<br/>

<br>

#### Response
```
//Ok
{
{
  "faceId": "bd7ea613",
  "code" : 0
}
}
//Fail
{
    "code" : 0,
    "message" : "reason"
}

```

| Name | Type | Description |
| :---- | :---- |:---- |
| faceId | String | 등록 얼굴 ID |
| code | Integer | 오류 코드 ([Error Code](models.md#error-code)) |
| message | String | 오류 메시지 |

<br>