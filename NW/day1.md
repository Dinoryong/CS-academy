# day1

-----

[toc]

# Intro

요즘엔 모든 것이 HTTP 기반으로 진행되지

BUT 인터넷에는 잘못된 정보들도 많고 정보들이 많이 흩어져있어

"개발자는 평생 HTTP 기반 위에서 개발한다! 그러니까 (must) 언젠가! 한번은! HTTP 를 정리해야 한다!ㅎㅎ"



### 강의목표

HTTP 전체 흐름을 이해하자

실무에 꼭 필요한 핵심 내용들을

예시와 그림을 같이 보면서 이해력 높이기

- 강의흐름 : 인터넷 네트워크 → URI 외  웹 브라우저 요청 흐름 → HTTP 기본 → HTTP 메서드 → HTTP 메서드 활용 → HTTP 상태코드 → HTTP 헤더1(일반헤더) → HTTP 헤더2 (캐시와 조건부 요청) →

  

# 인터넷 네트워크

## 인터넷 통신

> 사전 기본 학습

- 인터넷에서 컴퓨터 둘은 어떻게 통신할까?

컴퓨터 2대가 꼬옥 붙어 있으면 통신방법 고민할 이유가 없겠지

멀리 떨어져있으니고민 ( 클라이언스 pc 랑 서버 pc 랑 )

클라이언트 - 인터넷 ( 복잡 방대 인공위성 해저광케이블 노드 ) - 서버

인터넷으로 어떤 규칙으로 어떻게 클라이언트의 데이터들이 서버로 넘어갈까

- 인터넷

## IP(Internet Protocol)

- 인터넷 프로토콜, 아이피프로토콜
- 인터넷망 통한 데이터 전송을 위한 최소한의 규칙 - IP 주소 부여
- 지정하 IP 주소 ( IP ADREESS ) 에 데이터 전달
- 패킷(PACKET)이라는 통신 단위로 데이터 전달
- IP 패킷 정보 : 우리가 주소 던지듯이 적는다. 그리고 이 주소와 메세지를 (=IP패킷정보) 던진다 . 서로 노드끼리 던진다 . ( 야 ㅁ200.200.200.2 어디야? 저기 잇대 어디어디 )
- 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70638021-bc66-4865-9dfc-7e15a6d299e7/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/70638021-bc66-4865-9dfc-7e15a6d299e7/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/159e34e7-c54d-4e43-a067-7bcc660e95a2/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/159e34e7-c54d-4e43-a067-7bcc660e95a2/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccb3e1cd-c7b0-401c-b6ed-4c09b764229d/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccb3e1cd-c7b0-401c-b6ed-4c09b764229d/Untitled.png)

노드들끼리 서로 저 주소 어디냐ㅑ고 물어보면서 던지다가 목적에 도달한다.

### IP 프로토콜의 한계

- 비연결성

  - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송 (내 틴구 컴터가 꺼져 있을 경우)

- 비신뢰성

  - 중간에 패킷이 사라지면 ? (  )
  - 패킷이 순서대로 안 오면 ? (패킷을 여러개 보냈을 때, 순서대로 도착하지 않을 수 있기 때문,

  프로그램 구분

  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면 ? 동시에 여러 애플리케이션 실행 시에도 동일한 IP 주소를 사용하기 땜ㄴ에 구분이 안된다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/13b80549-33f3-449a-b040-12bf1ca0aaa6/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/13b80549-33f3-449a-b040-12bf1ca0aaa6/Untitled.png)

노드끼리 열심히 물어봐서 던지다가 저 주소에 맞게 도착했어. 그런데 저 서버가 꺼져있어. 그러면 전달 못 받음

전달되던 와중에 노드가 꺼져버렸다.(소실) 이것도 답 없다. ㅎ . EX) 광케이블

을 중간에 맷돼지가 끊어 먹어부렷어

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/905e5349-5cc5-4519-b882-e672de45c004/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/905e5349-5cc5-4519-b882-e672de45c004/Untitled.png)

각 패킷이 다른 노드를 따로 따로 타면서 갈 수 있다.

그럼 최종적으로 도착한 순서가 달라질 수 있다.

난 Hello World 로 보냈는데 상대방은 World Hello 로 바등ㅁ

이런 문제를 해결해주는 것이 TCP, UDP

## TCP, UDP

### 인터넷 프로토콜 스택의 4계층

> 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5303cac0-f9be-4743-b3d3-7fa620407c05/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5303cac0-f9be-4743-b3d3-7fa620407c05/Untitled.png)

### 프로토콜 계층

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e1549f7-d2b5-47ff-ae71-64d58d7285eb/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e1549f7-d2b5-47ff-ae71-64d58d7285eb/Untitled.png)

데이터 위에 TCP 씌우고 밑으로 내려서 IP 를 또 씌우고 해서 LAN 카드를 통해서 나간다 .

이때, 이더넷 프레임까지 (물리적정보?) 씌워서 나간다.

패킷 : 패키지(수하물) + 버킷(덩어리) 의 합성어

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d5c5c56d-5ccc-478c-bfdb-4a1aaa6a4fef/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d5c5c56d-5ccc-478c-bfdb-4a1aaa6a4fef/Untitled.png)

### TCP 특징

> 전송 제어 프로토콜 (Transmission Control Protocol)

- 연결지향 -  TCP 3 way handshake (가상 연결)
- 데이터 전달 보증 (만약 데이터가 누락되면 알 수 있다.)
- 순서 보장 (뒤에 나옴)
- 신뢰할 수 있는 프로토콜 (대부분 application에서 사용한다.)
- 현재는 대부분 TCP 사용

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f117ab4d-577f-415b-85be-cb599b17393b/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f117ab4d-577f-415b-85be-cb599b17393b/Untitled.png)

tcp 로 연결햇을 때 가장 먼저 위의 과정 시행.

클라이언트도 서버도 syn을 버리고 서로 수락 ack ack 한다. 즉 3번 주고받는다.

따라서 서로 신뢰할 수 있다.

이렇게 3번 연결한 후에 데이터를 전송한다.

BUT 중요한 점  :  이게 물리적으로 연결된 것(=레알 전화 랜선 전화기에 연결하는 거)이 아니라 개념적으로만 걍 논리적으로 생각하기에  연결된 것이다.

나를 위한 전용 랜선이 고정되는 것은 아니다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4597081b-96eb-41d3-a1f0-51abcbe13dd3/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4597081b-96eb-41d3-a1f0-51abcbe13dd3/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7571c60d-cc5d-449d-bf82-c64c75eaf0b1/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7571c60d-cc5d-449d-bf82-c64c75eaf0b1/Untitled.png)

내부적으로 최적화 로직은 다 다르겟지만

어쨌든 전체 로직은 저거임 (순서 보장)

위의 모든 tcp 과정은 검증 데이터가 추가 되기 때문에 가능핟.

### UDP 특징

> 사용자 데이터그램 프로토콜 (User Datagram Protocol)

ip protocol 일아 다 같은데 port 추가

- 하얀 도화지에 비유 (기능이 거의 없음)
- 연결지향 - TCP 3 way handshake X
- 데이터 전달 보ㅈ증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만 , 단순하고 빠름 (왜냐ㅁ하면 3way handshaking을 안 하니까)
- 정리
  - IP 와 거의 같다 + PORT 추가 (why? 여러 애플리케이션 사용 시에 구분을 해준다) + 체크섬 정도만 추가
  - 애플리케이션에서 추가 작업 필요

나 혼자 최적화를 더 하고 싶다면 UDP로 하묜 된다.

최근 각광 받는다. why? 웹 브라우저에서 웹 통신할 때, http 3 로 하는데  , syn ack 보내고 이런거를 다 줄이면서 최적화를 해보자 해서 UDP 를 사용하려고 한다.

ㄹ

## PORT

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab258bc2-eae7-4e62-8f45-3cae0825296c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ab258bc2-eae7-4e62-8f45-3cae0825296c/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db008c6d-07ba-4e36-9192-800daad537d8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db008c6d-07ba-4e36-9192-800daad537d8/Untitled.png)

패킷에서 출발지의ip , 출발지의 port 까지 다 내장해서 서버에게 보낸기 때문에

ㅅㅓ버가 클라이언트 주소를 다 알고 보낸다

비유

ip  :  신현대아파트

port  :  101동 102호

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bd4e56c9-968a-4f51-aa80-6fc053b65e63/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bd4e56c9-968a-4f51-aa80-6fc053b65e63/Untitled.png)

## DNS

IP 의 문제 1

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b0cedda-8b68-44ec-b4c4-a5bb40e00dc8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b0cedda-8b68-44ec-b4c4-a5bb40e00dc8/Untitled.png)

IP 의 문제 2

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f42c5d1e-9f80-40db-967a-58eb0c6b2c01/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f42c5d1e-9f80-40db-967a-58eb0c6b2c01/Untitled.png)

위의 2 가지 문제  모두 해결 by DNS

how ? 중간에 전화번호부 같은 서버르 제공해준다

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e7293495-d855-48cc-867b-2a4164d4ba69/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e7293495-d855-48cc-867b-2a4164d4ba69/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/58d7ab9f-56df-4a65-811e-015f0c6dc698/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/58d7ab9f-56df-4a65-811e-015f0c6dc698/Untitled.png)

위 인터넷 네트워크 정리 ppt 키워드만 보고서

강의처럼 다 설명할 수 있게 반복하자 !

# URI

> Uniform Resource Identifier

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04f665e6-b5d4-4fba-b3b6-2115f280d23b/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04f665e6-b5d4-4fba-b3b6-2115f280d23b/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18c0fdd5-cc89-443d-ab4c-6bdaa52721d4/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18c0fdd5-cc89-443d-ab4c-6bdaa52721d4/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1576c5c-a2e8-4a95-b51e-a0b18e474215/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1576c5c-a2e8-4a95-b51e-a0b18e474215/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c2e04eb-f08c-4ccc-8787-6e63ec2709dc/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c2e04eb-f08c-4ccc-8787-6e63ec2709dc/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80a00958-0e3f-4db0-9c1a-c061b560fc1e/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80a00958-0e3f-4db0-9c1a-c061b560fc1e/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c0de8dbe-8090-4f50-9584-a8559ebbd88f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c0de8dbe-8090-4f50-9584-a8559ebbd88f/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46c10f48-8016-4d71-80fe-9227a010f41c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46c10f48-8016-4d71-80fe-9227a010f41c/Untitled.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ca0a604-7ab9-4b2a-990b-2a2fa5309ac1/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ca0a604-7ab9-4b2a-990b-2a2fa5309ac1/Untitled.png)

User info

host

보통 도메인명이아나 ip를 직접 입ㄹㅕㄱ 가능

port

특정 서버에 따로 접근해야 하면 입력

path

계층적 구조로 되어 있다.

query

key=value 형태

query string으로도 불리는 이유 - 다 문자로 넘어감

fragment

# 웹 브라우저 요청 흐름

HTTP 요청 메시지

HTTP 응답 메시지

OK : 잘 했어

content type 중요 : 데이터의 형식

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18323156-8466-4706-b65e-1fccf4575096/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18323156-8466-4706-b65e-1fccf4575096/Untitled.png)

## TCP, UDP

## PORT

## DNS