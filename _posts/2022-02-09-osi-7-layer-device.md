---
layout: post
title: OSI 7 Layer 장비
author: Hara Oh
date: 2022-02-09 10:00:00 +0800
categories: [Network, OSI7Layer]
tags: [network, device, osi7layer]
---
## L7
---
- 웹 방화벽
- 메일 방화벽
- L7 switch
<br>

## L6
---
## L5
---
## L4
---
### L4 switch
- L1 ~ L4 인식 가능
- UDP, TCP의 port number정보를 보고 세션을 구분함 (session table)
- 로드밸런싱을 위해서 사용
<br>

## L3
---
### Router
- IP의 IP주소를 보고 길 찾기 하여 전달
- IP Routing Table은 관리자가 설정해야함
- Layer 3에서 루핑 looping ->  IP header에 TTL 필드로 라우터를 거치는 수를 제한을 함
    - IP header 의 TTL 필드 (0~255)
    - 라우터를 거칠때 1씩 감소
    - 라우터가 “0”이 되면 해당 패킷을 drop
    - 라우터가 출발지에게 ICMP 에러메시지를 전송함
    - 예시) 192.168.1.10에서 192.168.2.10으로 ping
        1. 라우터 fa0/0 인터페이스로 들어감(인바운드) 
        2. 라우팅 테이블 비교
        3. fa0/1 인터페이스로 전달됨(아웃바운드)
- 라우팅 테이블과 비교해서 어느 인터페이스로 전달할지 결정
    - Longest prefix match
        - subnetmask가 여러가지 라우터랑 매치될 때, 가장 subnetmask 일치율이 높은 라우터에 보내는 알고리즘
<br>

### L3 switch
- L2 스위치 기능과 L3 라우터 기능 모두를 갖춘 장비
- L1 ~ L3  인식 가능
- 이더넷/IP 프로토콜 인식 가능
- 우리나라는 L3 switch를 많이 사용
<br>

## L2
---
### switch
- L1 ~ L2 인식 가능
- 이더넷의 mac주소를 보고 데이터를 전달
- L2에서 루핑(looping) -> 스위치들이 STP를 동작하여 예방 (비효율적)
- 시스코의 이더채널 등으로 여러개를 하나의 링크처럼 인식되게 함 (효율적)
- Collision Domain 을 나누어 줌
- Broadcast Domain 내에 있음
- 이더넷 프로토콜 인식 가능
<br>

### 브릿지
- 이더넷 프로토콜 인식 가능
- Collision Domain 을 나누어 줌
- Broadcast Domain 내에 있음
<br>

## L1
---
### Hub
- Data <-> 전기 신호 변환을 해주지만 변환된 Data는 인식 하지 못함
- arp시, 2계층인 mac address를 읽지 못하기 때문에 전체에 메세지를 뿌린다(Flooding)
- CSMA/CD방식으로 동작하기 때문에 2개 이상 시스템이 동시에 보내면 충돌이남
- Collision Domain 내에 있음
<br>

### 리피터
Data <-> 전기 신호 변환을 해주는 장치입니다.