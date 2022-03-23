---
layout: post
title: Subnetting
author: Hara Oh
date: 2022-02-08 13:32:00 +0800
categories: [Network, Protocol]
tags: [network, subnetting]
---
# 서브넷팅이란? 
네트워크를 나누기 위해서 IP 주소의 구성을 변경 하는 것으로, 서브넷팅의 반대 개념으로는 여러 네트워크를 하나로 합치는 것 (Summary, Summaraztion)이 있다. 

네트워크를 나눌 때, 나누어진 작은 네트워크를 **서브넷 (Subnet)** 이라고 한다
# 서브넷팅을 하는 경우
- 필요한 IP가 있을 때 : HostID를 맞추기 (단, 2^n 으로만 가능)
- 필요한 서브넷 개수가 있을 때
    - IP address 32bit  = 동일한 Network ID + 유니크 Host ID
    - (IP개수 = 해당 네트워크 크기)
# 서브넷 계산
## Host ID 에 따라서 IP개수 계산해보기
### 192.168.1.0/24
  - host ID 8bit : 2^8 = 256개  (NA,BA 제외하면 254개)
  - host ID 7bit : 2^7 = 128개  (NA,BA 제외하면 126개)
  - host ID 6bit : 2^6 =   64개  (NA,BA 제외하면   62개)
  - host ID 5bit : 2^5 =   32개  (NA,BA 제외하면   30개)
  - host ID 4bit : 2^4 =   16개  (NA,BA 제외하면   14개)
  - host ID 3bit : 2^3 =     8개  (NA,BA 제외하면     6개)
  - host ID 2bit : 2^2 =     4개  (NA,BA 제외하면     2개)  -> 물리interface에서 할당
  - host ID 1bit : 2^1 =     2개  (NA,BA 제외하면     0개) -> 가상interface할당가능
### 예시
  - A class는 라우팅 테이블에 Network 목록 1개
  - A class  서브넷팅 256을 하면 라우팅 테이블 목록 256개
### 예제)  210.1.2.0/24
    - Network address   210.1.2.0
    - subnet mask        255.255.255.0
    - ip대역 	210.1.2.0 ~ 210.1.2.255  ( 256개)
    - subnet 2개로 나누기
        - 첫번째N   : 128개   210.1.2.0 ~ 210.1.2.127   N.a  210.1.2.0/25
        - 두번째N   : 128개   210.1.2.128 ~ 210.1.2.255  N.a 210.1.2.128 /25
    
- IP address 32bit  = 동일한 Network ID + 유니크 Host ID (IP개수 = 해당 네트워크 크기)
# Classful  / Classless
## Classful 
Default subnet mask를 사용한다.
- A/B/C class  (서브넷팅안함)
## Classless 
 A/B/C class개념 없이 서브넷팅, vlsm한 경우를 뜻함.  (CIDR표기)


# VLSM
- 각 서브넷(Sub-Network) 마다 가변 길이의 subnetmask를 적용하는 기법
    - 각 subnetmask이 각기 다른 크기(호스트 수 또는 주소 배정 수)를 갖을 수 있음
    - Classful Addressing 처럼 고정 길이의 subnetmask를 적용하지 않고, 호스트 수가 적은 네트워크에는 긴 마스크, 그 반대에는 짧은 마스크 적용 등
        - 동일 네트워크 주소 공간에서 다른 크기의 서브넷 사용 허용(서브넷의 서브넷팅)
## VLSM특징
### VLSM은 서브넷(Subnet) 지정의 융통성과 성능을 향상시켜줌
- 만일,Class C주소를 할당 시 256개 호스트 주소가 가능하나, 이보다 작은 수의 주소 만이 필요할 때, 적은 수의 주소를 할당 가능하여 주소의 낭비를 막음
    - 이미 서브넷으로 나누어진 네트워크 주소도 더 작은 서브넷으로 나눌 수 있음
        - 예) 먼저 `/16`서브넷 마스크로 나눈 네트워크를, 다시 `/24`서브넷 마스크로          나누고, 이를 또다시 `/27`서브넷 마스크로 추가적으로 나눌 수 있음
        - 2개의 양단간 시리얼(Serial)네트워크도 이용 가능
            - 이때에는 `/31`접두사(Prefix)를 사용하면 됨 (RFC 6164)
            
            ![Untitled](IP%20Address%20ecb06/Untitled%201.png)
                
### 주소 축약(Address Aggregation,경로 요약)도 가능
  - 여러서브넷으로 나누어진네트워크를 하나의네트워크로 다시 묶어 표현 가능
- VLSM을 사용하기 위해서는 이를 지원하는라우팅 프로토콜이 필수적임
  - VLSM 지원 불가능 (Classful Routing) :  RIPv1,IGRP
  - VLSM 지원 가능 (Classless Routing)  :RIPv2,EIGRP,OSPF,IS-IS,BGP
- 표준 :RFC 1878

### 예)  major network  195.10.20.0/24
```
network A  : 100개+2  -> 128개,  n 195.10.20.0/25

network B : 50개+2 ->64개,         N 195.10.20.128/26

network C :  10개+2 ->16개,       n 195.10.20.192/28

network D : 10개+2->16개,        n 195.10.20.160/28

network E : 2개   (라우터와 라우터 사이)+2=4개  195.10.20.224/30

network   F : 2개 (라우터와 라우터 사이)+2=4개   195.10.20.228/30

가장 큰 서브넷을 서브넷팅 하고 나머지를 다시 함.

C     D

0		A		       128	B	     192	         224   240    255  (256개)

{----------------|--------|--|--|--|--}

       128개			  64개	16 16 16 16개

A는 195.10.20.0/25를 할당 (0~127, 128개)

A 하고 나머지 195.10.20.128/25  (128~255) 128개

B  N 195.10.20.128/26 (128~191)

B하고 나머지 195.10.20.192/26 (64개)   (192-255)  64개

32개  195.10.20.192/27  (192~223, 32개)

16개  195.10.20.192/28  (192~207, 16개)  -C

16개  195.10.20.208/28  (208~223, 16개) -D

32개  195.10.20.224/27  (224~ 255, 32개) -나머지

195.10.20.224/28 , 195.10.20.240/28

C  n 195.10.20.192/28  (192-207) 16개

D  n 195.10.20.208/28 (208-223) 16개

D하고 나머지  195.10.20.224/28 , 195.10.20.240/28  (16개 ip subnet이 2개)

=  195.10.20.224/27 (224 ~ 255, 32개)

E n  195.10.20.224/30  (224~227, 4개)

F n 195.10.20.228/30   (228~231)

나머지  195.10.20.232/30 (232~235) , 195.10.20.236/30  (236~239)

또는 195.10.20.232/29 (232~239 , 8개)

나머지  195.10.20.240/28 (240~255, 16개)

Network A—[Router1]------------------[Router2]----Network B

Network address

Router1  ip

ROuter2 ip

broadcast address		/ 4개

10.0.0.0/8

10.1.1.0/24
```


## CIDR
[CIDR (ktword.co.kr)](http://www.ktword.co.kr/test/view/view.php?nav=2&no=1144&sh=cidr)

cmd>  ipconfig /all   (L2, L3 주소, gateway 주소, dns server주소)

cmd> ping [gateway_ip]

cmd> ping [dnsserver_ip]

cmd> ping 8.8.8.8 (외부망-구글dns)

cmd> tracert  [8.8.8.8]

경로추적  traceroute 의 약자

IP header TTL 필드 (Time to Live)-라우터를 거칠 수 있는 수 (값이 1인 패킷을 수신하면 버림)

pc—-R1—----R2—-----R3—-목적지

pc> tracert [목적지]

ping echo 전송 IP.ttl=1   -> 게이트웨이가 받음 ttl=0, 게이트이가 drop, 에러발생

R1이 발생한 에러메시지를 수신

ping echo 전송 IP.ttl=2  -> R1 ttl=1 -> R2 ttl=0, R2가 버리고 ,pc에게 에러 전송

ping echo 전송 IP.ttl=3  -> R1 ttl=2 -> R2 ttl=1 , R3 ttl=0, R3가 버리고 ,pc에게 에러 전송

ping echo 전송 IP.ttl=4  -> R1 ttl=3 -> R2 ttl=2 -> R3=ttl2 -> 목적지 응답메시지 전송

pc>  R1 ip,

R2  ip

R3 ip

목적지 ip