---
layout: post
title: AWS CloudFront
author: Hara Oh
date: 2022-03-31 17:28:00 +0800
categories: [AWS, 네트워킹 및 콘텐츠 전송]
tags: [aws, cloudfront]
---
## CloudFront란?
---
html, css, js 및 이미지 파일과 같은 정적 및 동적 웹 컨텐츠를 전세계에 배치된 Edge Location을 이용하여 사용자에게 더 빨리 배포하도록 지원하는 웹서비스
<br>
→ 어디서든 웹페이지를 빠르게 띄워주는 서비스


![AWS Direct Connect](/assets/img/aws/cf.png)

## Origin Server
---
- 원본 데이터를 가지고 있는 서버
- 보통 AWS에서의 Origin Server는 S3, EC2 instance

<br>

## Edge Server (Edge Location)
---
- AWS에서 실질적으로 제공하는 전 세계에 퍼져 있는 서버
- Edge Server에는 요청 받은 데이터에 대해서 같은 요청에 대해  빠르게 응답해주기 위해 Cache 기능을 제공 (기본 TTL은 24시간)
- 요청 받은 데이터가 없는 경우에는 오리진 서버로 요청
- 각 지역마다 있기 때문에 오리진 서버로의 부하가 분산되어 빠른 처리가 가능
