---
layout: post
title: OSI 7 Layer PDU
author: Hara Oh
date: 2022-02-09 11:00:00 +0800
categories: [Network, OSI7Layer]
tags: [network, pdu, osi7layer]
---
# PDU

L7  

L6		  data + 서비스

L5 		  [ [www.naver.com](http://www.naver.com/) 요청 ] + http

L4		  [	   요청 + http             ] + TCP header		>  segment 세그먼트

L3		  [	       요청+http+tcp		       ] + IP header		>  packet 패킷

L2	 tailer [	            요청+http+tcp+ip		  ] + ethernet header    > frame 프레임

L1