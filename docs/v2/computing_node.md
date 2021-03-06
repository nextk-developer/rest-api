---
layout: default
title: 컴퓨팅 노드
nav_order: 3
parent: v2
has_children: false
# permalink: /docs/v2
---

실시간 영상 분석을 수행할 컴퓨팅 노드를 관리하는 API입니다.<p>
컴퓨팅 노드는 NK-AI 프로세스를 논리적으로 지칭합니다.

----


# 컴퓨팅 노드 등록하기
## Request
```
POST /v2/va/create-computing-node

{
  "host": "192.168.0.39",
  "httpPort": 8880,
  "nodeName": "TEST_SYSTEM_PC",
  "license": "license-test-code-nkai"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| host | String | 호스트주소 | O |
| httpPort | Integer | HTTP 포트번호 | O |
| rpcPort | Integer | RPC 포트번호 | O |
| nodeName | String | 노드 닉네임 | X |
| licnese | String | 라이선스 값 | O |

<br>

### Response
```
//Ok
{
  "nodeId": "350d8934",
  "nodeName": "TEST_SYSTEM_PC",
  "httpHost": "192.168.0.36",
  "httpPort": 8880,
  "rpcHost": "192.168.0.36",
  "rpcPort": 33300,
  "license": "license-test-code-nkai",
  "productCode": "NK_API_V2",
  "releaseDate": "2021-11-09 17:51:55",
  "code" : 0
}
//Already
{
  "nodeId": "4945bb32",
  "message": "ComputeNode that already exists",
  "code": 0
}
//Fail
{
  "message": "Failed Create Node ID",
  "code": 100
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----|
| nodeId | String | 컴퓨팅 노드 ID | O |
| nodeName | String | 컴퓨팅 노드 이름| O |
| httpHost | String | http 호스트 | O |
| httpPort | Integer | http 포트 | O |
| rpcHost | String | rpc 호스트 | O |
| rpcPort | Integer | rpc 포트 | O |
| license | String | 라이선스 | O |
| productCode | String | 제품 코드 | O |
| releaseDate | String | 제품 정보 | O |
| code | Integer | 요청 응답 | O |
| message | String | 처리 메시지 | X |

<br><br>

# 컴퓨팅 노드 조회하기
### Request
```
POST /v2/va/get-computing-node

{
  "nodeId": "4945bb32",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String |노드 ID | O |


<br>

### Response
```
// Ok
{
  "nodeId": "350d8934",
  "nodeName": "TEST_SYSTEM_PC",
  "httpHost": "192.168.0.36",
  "httpPort": 8880,
  "rpcHost": "192.168.0.36",
  "rpcPort": 33300,
  "license": "license-test-code-nkai",
  "productCode": "NK_API_V2",
  "releaseDate": "2021-11-09 17:51:55",
  "code": 0
}

// Fail
{
    "code": 101
    "message": "Not Found NodeId"
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- | :----|
| nodeId | String | 컴퓨팅 노드 ID | O |
| nodeName | String | 컴퓨팅 노드 이름| O |
| httpHost | String | http 호스트 | O |
| httpPort | int | http 포트 | O |
| rpcHost | String | rpc 호스트 | O |
| rpcPort | int | rpc 포트 | O |
| license | String | 라이선스 값 | O |
| productCode | String | 제품 코드 | O |
| releaseDate | String | 제품 정보 | O |
| code | Integer | 요청 응답 | O |
| message | String | 처리 메시지 | X |


<br><br>


# 컴퓨팅 노드 목록 조회하기
모든 컴퓨팅 노드를 조회합니다.

### Reqeust
```
POST /v2/va/list-computing-node

{

}
```
### Response
```
[
  {
    "nodeId": "350d8934",
    "nodeName": "TEST_SYSTEM_PC",
    "httpHost": "192.168.0.36",
    "httpPort": 8880,
    "rpcHost": "192.168.0.36",
    "rpcPort": 33300,
    "license": "license-test-code-nkai",
    "productCode": "NK_API_V2",
    "releaseDate": "2021-11-09 17:51:55"
  },
  {
    "nodeId": "350d8934",
    "nodeName": "TEST_SYSTEM_PC",
    "httpHost": "192.168.0.36",
    "httpPort": 8880,
    "rpcHost": "192.168.0.36",
    "rpcPort": 33300,
    "license": "license-test-code-nkai",
    "productCode": "NK_API_V2",
    "releaseDate": "2021-11-09 17:51:55"
  }
]
```

"[컴퓨팅 노드 조회하기](#컴퓨팅-노드-조회하기)"와 동일한 응답이 배열로 반환 됩니다.


<br><br>


# 컴퓨팅 노드 수정하기

```
POST /v2/va/update-computing-node
{
  "nodeId": "14f502f2",
  "nodeName": "TEST_NODE",
  "license" : "license-test-code-nkai"
}
```

### Request

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 노드 ID |
| nodeName | String | 노드 닉네임 |
| license | String | 라이선스 값 |

<br>

### Response
```
{
  "nodeId": "14f502f2",
  "code": 0
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |




<br><br>

# 컴퓨팅 노드 삭제하기
### Request

```
POST /v2/va/remove-computing-node

{
  "nodeId": "4945bb32",
}
```

| Name | Type | Description | Required |
| :---- | :---- |:---- |:---- |
| nodeId | String |노드 ID | O |

<br>

### Response
```
//ok
{
  "nodeId": "14f502f2",
  "code": 0
}
//fail
{
  "code": 400
}
```

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String |노드 ID |

