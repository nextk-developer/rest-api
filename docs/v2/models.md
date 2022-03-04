---
layout: default
title: JSON Objects and Enums
nav_order: 5
parent: v2
has_children: false
# permalink: /docs/v2
---


REST API 파라메터로 사용되는 JSON 오브젝트와 Enum들입니다.

------------------------

# Channel

| Name | Type | Description |
| :---- | :---- |:---- |
| channelId | string | 채널 ID |
| inputUri | string | 입력 영상 주소 |
| channelName | string | 채널 이름 |
<!-- | inputType | int | 입력 영상 종류(**[InputType](models.md#inputtype)**) | -->
<!-- | status | Enum | 채널 상태 (**[ChannelStatus](#channelstatus)**)| -->

<br><br>

# ChannelStatus

| Enum | Description |
| :---- | :---- |
| CH_STATUS_NORMAL | 정상 |
| CH_STATUS_INPUT_DEVICE_CONNECTION_LOST | 입력장치 연결 끊김 |

<br>

# ObjectType

| Enum | Description |
| :---- | :---- |
| PERSON | 사람 |
| BIKE | 자전거 |
| CAR | 일반 차량 |
| MOTORCYCLE | 오토바이 |
| BUS | 대형 버스 |
| TRUCK | 트럭 |
| EXCAVATOR | 굴착기 |
| TANKTRUCK | 탱크트럭 |
| FORKLIFT | 지게차 |
| LEMICON | 레미콘 |
| CULTIVATOR | 경운기 |
| TRACTOR | 트랙터 |
| SMOKE | 불꽃 |
| FLAME | 연기 |
| FACE_MAN | 얼굴_남자 |
| FACE_WOMAN | 얼굴_여자 |

<br>

# Roi Feature  

| Enum | Description |
| :---- | :---- |
| ALL | 내부/외부 객체 감지 |
| INSIDE | 내부 발생 감지 |
| OUTSIDE | 외부 발생 감지 |
| IGNORE | 비감지 |

<br>

# EventType

| Enum | Description |
| :---- | :---- |
| EVT_LONGSTAY | 체류 |
| EVT_LOITERING | 배회 |
| EVT_INTRUSION | 침입 |
| EVT_FALLDOWN | 쓰러짐 |
| EVT_ABANDONMENT | 유기 |
| EVT_VIOLENCE | 싸움 |
| EVT_PEOPLE_COUNTING | 사람 카운트 |
| EVT_QUEUEING | 대기열 |
| EVT_ABNORMAL_CONGESTION | 혼잡도 |
| EVT_ABNORMAL_OBJ_COUNT | 영역 과밀집 |
| EVT_ROI_COUNT | 영역 ROI 카운팅 |
| EVT_LINE_COUNT | LINE 양방향 카운팅 |
| EVT_ILLEGAL_PARKING | 불법 주정차 |
| EVT_WRONG_WAY | 역주행 |
| EVT_DIRECTION_COUNTING | 방향성 이동(직전, 좌/우회전, 유턴) 카운팅 |
| EVT_PEOPLE_CONGESTION_LEVEL | 사람 혼잡도 수준 |
| EVT_VEHICLE_SPEED | 차량 속도 |
| EVT_VEHICLE_DENSITY | 차량 밀도 |
| EVT_STOP_VEHICLE_COUNTING | 정지 차량 카운팅 |
| EVT_LINE_ENTER | LINE 단방향 통과 |
| EVT_FLAME | 화재(불꽃, 연기) |
| EVT_FACE_MATCHING | 얼굴 등록 매칭 |
| EVT_FACE_MASKED | 얼굴 마스크 미착용 |

<br><br>

# Functions

컴퓨팅 노드가 사용 가능한 기능들

| Enum | Description |
| :---- | :---- |
| FNC_CORE | 핵심 기능 |

<!-- | FNC_ITS | 지능형 교통 시스템 | -->


# InputType
입력 비디오 타입

| Enum | Description |
| :---- | :---- |
| SRC_IPCAM_NORMAL | 일반 카메라 (Default) 영상 |
| SRC_IPCAM_THERMAL | 열화상 카메라 영상 |
| SRC_IPCAM_DEPTH | 깊이센서 카메라 영상 |
| SRC_ETC | 기타 영상 |

<br><br>



# SystemWarnings

| Enum | Description |
| :---- | :---- |
| SYS_RESOURCE_FULL | 시스템 리소스 한계 사용 중 |
| SYS_UNSTABLE_NETWORK | 네트워크 불안정 |
| SYS_NO_LICENSE | 라이센스 없음 |
| SYS_LICENSE_EXPIRED | 라이센스 만료 |

<br>

# Performance

| Name | Type | Description |
| :---- | :---- |:---- |
| cpuUsage | Double | CPU 사용률 |
| gpuUsage | Double | GPU 사용률 |
| memoryUsage | Double | Memory 사용률 |
| diskUsage | Double | Disk 사용률 |


<br>

# Version

| Name | Type | Description |
| :---- | :---- |:---- |
| software | String | NK 프로그램 버전 |
| detectorModel | Dynaimc Dictionary | model version |
| firmware | String | 펌웨어 버전 (OS) |
| gpuModel | String | GPU 모델 |
| gpuVersion | String | GPU 버전 |


<br>

# Calibration
| Name | Type | Description |
| :---- | :---- |:---- |
| focalLengthX | Double | 초첨거리 X | 
| focalLengthY | Double | 초첨거리 Y |
| principalX | Double | 원리좌표 X |
| principalY | Double | 원리좌표 Y |
| fov         | Double | 화각 |
| imageWorldX | Double | 이미지 월드좌표 X|
| imageWorldY | Double | 이미지 월드좌표 Y|
| imageWorldZ | Double | 이미지 월드좌표 Z|
| cameraPanDegree | Double | 카메라 Pan 각도 |
| cameraTiltDegree | Double | 카메라 Pan 각도 |
| cameraHorizontalAngle | Double | 카메라 수평각 |

<br>

# EventFilter

| Name | Type | Description |
| :---- | :---- |:---- |
| objectsTarget | ObjectType[] | 검출 객체 대상(**[ObjectType](models.md#ObjectType)**) | 

<br>


<!-- # RecentCrashLogs
최근 비정상 종료 된 컴퓨팅 노드 기록정보

| Name | Type | Description |
| :---- | :---- |:---- |
| nodeId | String | 컴퓨팅 노드 ID |
| crashTime | String | 비정상 종료 시각 |

<br><br> -->



# Operations

비디오 분석 제어 명령들

| Enum | Description |
| :---- | :---- |
| VA_START | 비디오 분석 시작/재개 |
| VA_STOP | 비디오 분석 중지 |
| VA_RESET | 비디오 분석 중 누적 집계된 값들을 모두 초기화 (즉, ROI 설정 직후 상태로 초기화) |


# Error code

| Value | Description |
| :---- | :---- |
| 0 | 성공 |
| 10 | api uri path 문제 |
| 11 | api 요청 데이터 포맷 문제 |
| 12 | 지원하지 않는 기능 |
| 20 | 라이선스 비활성화 |
| 21 | 라이선스 기간 만료 |
| 22 | 지원하지 않는 API 버전 |
| 23 | RPC 포트 문제 |
| 24 | HTTP 포트 문제 |
| 100 | 컴퓨팅 노드 생성 실패|
| 200 | 채널 영상 수신 실패|
| 201 | 채널 생성 실패 |
| 210 | 캘리브레이션 실패 |
| 220 | 스냅샷 생성 실패 |
| 300 | ROI 설정 실패 |
| 400 | 얼굴 등록 실패 |