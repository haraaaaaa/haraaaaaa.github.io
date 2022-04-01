---
layout: post
title: 서브넷팅 (Subnetting)
author: Hara Oh
date: 2022-02-08 13:32:00 +0800
categories: [Network, Protocol]
tags: [network, subnetting]
---
## 서브넷팅이란? 
---
네트워크를 나누기 위해서 IP 주소의 구성을 변경 하는 것으로, 서브넷팅의 반대 개념으로는 여러 네트워크를 하나로 합치는 것 (Summary, Summaraztion)이 있습니다.

네트워크를 나눌 때, 나누어진 작은 네트워크를 **서브넷 (Subnet)** 이라고 합니다.
## 서브넷팅을 하는 경우
---
- 필요한 IP가 있을 때 : HostID를 맞추기 (단, 2^n 으로만 가능)
- 필요한 서브넷 개수가 있을 때
    - IP address 32bit  = 동일한 Network ID + 유니크 Host ID
    - (IP개수 = 해당 네트워크 크기)
<br>

## 서브넷 계산
---
### Host ID 에 따라서 IP개수 계산해보기
#### 192.168.1.0/24
- host ID 8bit : 2^8 = 256개  (NA,BA 제외하면 254개)
- host ID 7bit : 2^7 = 128개  (NA,BA 제외하면 126개)
- host ID 6bit : 2^6 =  64개  (NA,BA 제외하면  62개)
- host ID 5bit : 2^5 =  32개  (NA,BA 제외하면  30개)
- host ID 4bit : 2^4 =  16개  (NA,BA 제외하면  14개)
- host ID 3bit : 2^3 =   8개  (NA,BA 제외하면   6개)
- host ID 2bit : 2^2 =   4개  (NA,BA 제외하면   2개) -> 물리interface에서 할당
- host ID 1bit : 2^1 =   2개  (NA,BA 제외하면   0개) -> 가상interface할당가능
<br>

### 예시
#### 210.1.2.0/24 네트워크르 서브넷 2개로 나누기
```plaintext
Network Address   210.1.2.0
Subnet Mask       255.255.255.0
IP 대역           210.1.2.0 ~ 210.1.2.255  (256개)
```
- 첫번째N   : 128개   210.1.2.0 ~ 210.1.2.127   N.a  210.1.2.0/25
- 두번째N   : 128개   210.1.2.128 ~ 210.1.2.255  N.a 210.1.2.128 /25  
- IP address 32bit  = 동일한 Network ID + 유니크 Host ID (IP개수 = 해당 네트워크 크기)
<br>

## Classful  / Classless
---
### Classful 
Default subnet mask를 사용합니다.
- A/B/C class  (서브넷팅안함)
<br>

### Classless 
 A/B/C class개념 없이 서브넷팅, VLSM한 경우를 뜻합니다.  (CIDR표기)


## VLSM이란?
---
각 서브넷(Sub-Network) 마다 가변 길이의 subnetmask를 적용하는 기법입니다.
  - 각 subnetmask이 각기 다른 크기(호스트 수 또는 주소 배정 수)를 갖을 수 있음
  - Classful Addressing 처럼 고정 길이의 subnetmask를 적용하지 않고, 호스트 수가 적은 네트워크에는 긴 마스크, 그 반대에는 짧은 마스크 적용 등
      - 동일 네트워크 주소 공간에서 다른 크기의 서브넷 사용 허용(서브넷의 서브넷팅)
<br>

### VLSM특징
#### VLSM은 서브넷(Subnet) 지정의 융통성과 성능을 향상시켜줌
- Class C주소를 할당 시 256개 호스트 주소가 가능하나, 이보다 작은 수의 주소만 필요할 때, 적은 수의 주소를 할당 가능하여 주소의 낭비를 막음
- 이미 서브넷으로 나누어진 네트워크 주소도 더 작은 서브넷으로 나눌 수 있음
  - 예) 먼저 `/16`서브넷 마스크로 나눈 네트워크를, 다시 `/24`서브넷 마스크로 나누고, 이를 또다시 `/27`서브넷 마스크로 추가적으로 나눌 수 있음
- 2개의 양단간 시리얼(Serial)네트워크도 이용 가능하며, 이때에는 `/31`접두사(Prefix)를 사용하면 됨 (RFC 6164)

#### 주소 축약(Address Aggregation,경로 요약)도 가능
- 여러 서브넷으로 나누어진 네트워크를 하나의 네트워크로 다시 묶어 표현 가능
- VLSM을 사용하기 위해서는 이를 지원하는라우팅 프로토콜이 필수적
  - VLSM 지원 불가능 (Classful Routing) :  RIPv1,IGRP
  - VLSM 지원 가능 (Classless Routing)  :RIPv2,EIGRP,OSPF,IS-IS,BGP
- 표준 :RFC 1878

## CIDR란?
---
사이더(Classless Inter-Domain Routing, CIDR)는 클래스 없는 도메인 간 라우팅 기법입니다.
