---
layout: post
title: AWS Snowball
author: Hara Oh
date: 2022-03-31 17:28:00 +0800
categories: [AWS, 마이그레이션 및 전송]
tags: [aws, snowball]
---
# Snowball이란?
---
페타바이트*급 대용량 데이터를 전송하기 위한 서비스로 최대 80TB까지 저장 가능하며, Snowball이외에 기능이 추가된 Snowball Edge가 있습니다.

※ 페타바이트란?
테라바이트의 다음 단위, 1024 테라바이트는 1페타바이트


![AWS Direct Connect](/assets/img/aws/snowball.png)

# 서비스의 흐름
1. 위의 사진과 같은 Snowball을 AWS에서 배송 받음
2. Snowball에 온프레미스에 있던 데이터를 이동함
3. Snowball을 다시 AWS로 배송
4. AWS에서 S3 bucket에 Snowball에 있던 자료를 이동

<br>

## 사용 예시
- 페타바이트 규모의 데이터를 AWS로 이송하는 경우
- VPN, Direct Connect, S3를 통한 전송을 이용하기엔 데이터의 양이 많을 경우
- 물리적으로 격리된 환경이거나 인터넷 환경이 좋지 않을 경우
- 평균적으로 AWS로 데이터를 업로드하는데 1주일 이상이 소요되는 경우