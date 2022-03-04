---
layout: default
title: 비디오 분석 결과
nav_order: 8
parent: v2
has_children: false
# permalink: /docs/v2
---


비디오 분석 결과는 **[gRPC](https://grpc.io/docs/what-is-grpc/introduction/)**를 통해 스트리밍 방식으로 클라이언트에게 전송됩니다.

 - gRPC는 Google의 **[protocol buffers version 3 (proto3)](https://developers.google.com/protocol-buffers/docs/proto3)** 문법으로 작성되어 있습니다.

아래 버튼링크를 통해 gRPC용 proto3 IDL파일을 확인해주십시오.

[비디오 분석결과 gRPC 연동 인터페이스 보기](https://github.com/nextk-developer/protobuf/blob/master/sendMetadata.proto){: .btn .btn-blue }