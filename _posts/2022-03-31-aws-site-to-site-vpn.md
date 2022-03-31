---
layout: post
title: AWS Site-to-Site VPN
author: Hara Oh
date: 2022-03-31 17:28:00 +0800
categories: [AWS, 네트워킹 및 콘텐츠 전송]
tags: [aws, site_to_site_vpn]
---
# AWS Site-to-Site VPN
---
![AWS Site-to-Site VPN](/assets/img/aws/vpn.png)
일반적으로 Virtual Private Network의 약자로 가설사설망을 뜻하지만, AWS Site-to-Site VPN에서의 VPN 연결은 VPC와 자체 온프레미스 네트워크 간의 연결을 의미함

AWS Site-to-Site VPN은 네트워크와 VPC 또는 Transit Gateway 사이에 암호화된 2개의 터널을 생성하여 사용
인터넷 프로토콜 보안(IPsec) VPN 연결을 지원
최대 1.25Gbps의 처리량을 지원

## 사용 예시

### 하이브리드 네트워크 구축
AWS와 온프레미스 네트워크를 연결하여 성능의 저하 없이 여러 환경에 걸친 애플리케이션을 구축할 수 있습니다.

## 요금
Site-to-Site VPN 연결당 0.05 USD(시간당)

# AWS Direct Connect와의 차이점
---
![Difference of VPN and DC](/assets/img/aws/diff_dc_vpn.png)

## 결론
보안에서는 Direct Connect가, 금액에서는 Site-to-Site VPN이 저렴하기 때문에 유리
