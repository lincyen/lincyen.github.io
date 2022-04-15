---
layout: single                                
title: 오픈소스를 활용한 모니터링 환경 구축하기
date: "2021-09-28 10:00:00 +0900"
toc : false
category: 오픈소스 사용기
tags: [VPN, opensource]
---

시작하면서
================

오픈소스들을 이용해서 관제 환경을 구성할 수 있는 방법이 있을까 해서 개인적으로 수행했던 프로젝트의 일부입니다.
구성 가능함을 확인했고 그 일부 내용들을 지속적으로 정리해놓고자 합니다.

구성도
================

기본적인 구성도는 아래와 같습니다.
+ APM 으로 scouter2 를 이용하고, 스위치 등 네트워크 장비는 telegraf 등을 이용해서 정보를 수집합니다.
+ 수집된 정보는 시계열데이터베이스인 influxDB 에 적재하고, influxDB 로 어려운 부분들에 대해서는 Prometheus 를 활용할 수도 있습니다.
+ 수집된 정보들은 Grafana 에서 데이터시각화를 수행합니다.

![image](https://user-images.githubusercontent.com/23024189/163524583-860564e8-f32c-42b9-ab4d-c3f274771a30.png)


참고자료
================
지속적으로 업데이트 예정입니다.

[폐쇄망 환경에서 Scouter2 설치하기](https://lincyen.github.io/%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4%20%EC%82%AC%EC%9A%A9%EA%B8%B0/private-install-scouter2/)
[폐쇄망 환경에서 telegraf 설치하기](https://lincyen.github.io/%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4%20%EC%82%AC%EC%9A%A9%EA%B8%B0/private-install-telegraf/)
[폐쇄망 환경에서 influxDB2 설치하기](https://lincyen.github.io/%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4%20%EC%82%AC%EC%9A%A9%EA%B8%B0/private-install-influxdb2/)
[폐쇄망 환경에서 grafana 설치하기](https://lincyen.github.io/%EC%98%A4%ED%94%88%EC%86%8C%EC%8A%A4%20%EC%82%AC%EC%9A%A9%EA%B8%B0/private-install-grafana/)



