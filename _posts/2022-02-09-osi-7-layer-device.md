---
title: OSI 7 Layer Device
author: Hara Oh
date: 2022-02-08 13:32:00 +0800
categories: [Network, OSI7Layer]
tags: [network, device, osi7layer]
---
# 장비

- L7
    - 웹 방화벽
    - 메일 방화벽
    - L7 switch
- L6
- L5
- L4
    - L4 switch
        - L1 ~ L4 인식 가능
        - UDP, TCP의 port number정보를 보고 세션을 구분함 (session table)
        - 로드밸런싱을 위해서 사용
- L3
    - Router
        - IP의 IP주소를 보고 길 찾기 하여 전달
        - Layer 3에서 루핑 looping ->  IP header에 TTL 필드로 라우터를 거치는 수를 제한을 함
            - IP header 의 TTL 필드 (0~255)
            - 라우터를 거칠때 1씩 감소
            - 라우터가 “0”이 되면 해당 패킷을 drop
            - 라우터가 출발지에게 ICMP 에러메시지를 전송함
            - 예시 - 192.168.1.10에서 192.168.2.10으로 ping
                1. 라우터 fa0/0 인터페이스로 들어감(인바운드) 
                2. 라우팅 테이블 비교
                3. fa0/1 인터페이스로 전달됨(아웃바운드)
        - 라우팅 테이블과 비교해서 어느 인터페이스로 전달할지 결정
            - Longest prefix match
                - subnetmask가 여러가지 라우터랑 매치될 때, 가장 subnetmask 일치율이 높은 라우터에 보내는 알고리즘
    - L3 switch
        - L2 스위치 기능과 L3 라우터 기능 모두를 갖춘 장비
        - L1 ~ L3  인식 가능
        - 우리나라는 L3 switch를 많이 사용
- L2
    - switch
        - L1 ~ L2 인식 가능
        - 이더넷의 mac주소를 보고 데이터를 전달
        - Layer 2 에서 루핑 looping -> 스위치들이 STP를 동작하여 예방 (비효율적)
        - 또는 시스코의 이더채널 등으로 여러개를 하나의 링크처럼 인식되게 함 (효율적)
        - Collision Domain 을 나누어 줌
        - Broadcast Domain 내에 있음
    - 브릿지
        - 데이터와 전기신호 변환
        - 이더넷 프로토콜 인식 가능
        - Collision Domain 을 나누어 줌
        - Broadcast Domain 내에 있음
- L1
    - Hub
        - Data <-> 신호 변환
        - arp시, 2계층인 mac address를 읽지 못하기 때문에, 전체에 메세지를 뿌린다(Flooding)
        - 2개 이상 시스템이 동시에 보내면 충돌이남. CSMA/CD
        - Collision Domain 내에 있음
    - 리피터
        - Data <-> 신호 변환

네트워크 장비

리피터 : L1  , 데이터와 전기신호 변환

허브 : L1  , 데이터와 전기신호 변환 , 변환된 data를 인식할 수 없음. flooding

2개 이상 시스템이 동시에 보내면 충돌이남. CSMA/CD

Collision Domain 내에 있음.

브릿지 : L2  , 데이터와 전기신호 변환, 이더넷 프로토콜 인식 가능

Collision Domain 을 나누어 줌.  Broadcast Domain 내에 있음

스위치 : L2  , 데이터와 전기신호 변환, 이더넷 프로토콜 인식 가능

Collision Domain 을 나누어 줌.  Broadcast Domain 내에 있음

src/dst MAC 주소로 스위칭함. MAC Address Table (learning,flooding,forwarding,filtering,aging)

라우터 : L3 , 데이터와 전기신호 변환, 이더넷/IP 프로토콜 인식 가능

IP Routing Table(관리자가 설정 필요)

Broadcast Domain을 나누어줌.