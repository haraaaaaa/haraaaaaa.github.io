---
layout: post
title: OSI 7 Layer PDU
author: Hara Oh
date: 2022-02-09 11:00:00 +0800
categories: [Network, OSI7Layer]
tags: [network, pdu, osi7layer]
---
## PDU(Protocol Data Unit)란?
---
각 계층 별 프로토콜의 데이터 단위

|계층|                              구성                            |   PDU   |
|:--:|:------------------------------------------------------------:|:-------:|
| L7 |                                                             |   Data  |
| L6 | Data + Service                                              |   Data  |
| L5 | [Request] + http                                            |   Data  |
| L4 | [Request + http] + TCP header                               | Segment |
| L3 | [Request + http + TCP header] + IP header                   |  Packet |
| L2 | Tailer [Request + http + TCP header + IP] + Ethernet header |  Frame  |
| L1 |                                                             |   Bit   |

![PDU](/assets/img/network01/pdu.png)