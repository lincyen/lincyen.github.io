---
layout: single                                
title: 폐쇄망 환경에서 telegraf 설치하기
date: "2021-08-02 10:00:00 +0900"
toc : false
category: 오픈소스 사용기
tags: [VPN, opensource]
---

인플럭스DB 와 스카우터 에이전트로 사용할 수 있는 텔레그라프에 대해서 알아보았던 내용을 정리해 보았습니다.

개요
============
출처 : 텔레그라프, [https://www.influxdata.com/time-series-platform/telegraf/](https://www.influxdata.com/time-series-platform/telegraf/)

텔레그라프란?
------------
Telegraf는 데이터베이스, 시스템 및 IoT 센서에서 메트릭 및 이벤트를 수집하고 전송하기 위한 플러그인 기반 서버 에이전트입니다.
Telegraf는 Go로 작성되었으며 외부 종속성이 없는 단일 바이너리로 컴파일되며 매우 최소한의 메모리 사용 공간이 필요합니다.

텔레그라프를 사용하는 이유
------------
모든 종류의 데이터 수집 및 전송:
+ 데이터베이스: MongoDB, MySQL, Redis 등과 같은 데이터 소스에 연결하여 메트릭을 수집하고 보냅니다.
+ 시스템: 최신 클라우드 플랫폼, 컨테이너 및 오케스트레이터 스택에서 메트릭을 수집합니다.
+ IoT 센서: IoT 센서 및 장치에서 중요한 상태 저장 데이터(압력 수준, 온도 수준 등)를 수집합니다.
+ Agent : Telegraf는 다양한 입력에서 메트릭을 수집하고 이를 다양한 출력에 쓸 수 있습니다. 데이터 수집 및 출력 모두 플러그인 기반이므로 쉽게 확장할 수 있습니다. Go로 작성되었습니다. 즉, 외부 종속성, npm, pip, gem 또는 기타 패키지 관리 도구 없이 모든 시스템에서 실행할 수 있는 컴파일된 독립 실행형 바이너리입니다.
+ Coverage : 커뮤니티 데이터에 대해 주제 전문가가 이미 작성한 200개 이상의 플러그인을 사용하면 끝점에서 메트릭 수집을 쉽게 시작할 수 있습니다. 더욱이 플러그인 개발이 간편하기 때문에 모니터링 요구 사항에 맞게 플러그인을 빌드할 수 있습니다. Telegraf를 사용하여 입력 데이터 형식을 메트릭으로 구문 분석할 수도 있습니다. 여기에는 InfluxDB 라인 프로토콜, JSON, Graphite, Value, Nagios 및 Collectd가 포함됩니다.
+ Flexible : Telegraf 플러그인 아키텍처는 프로세스를 지원하며 해당 기술을 사용하기 위해 워크플로를 변경하도록 강요하지 않습니다. 엣지에 앉거나 중앙 집중식 방식으로 필요하든지 상관없이 아키텍처에 딱 맞습니다. Telegraf의 유연성 덕분에 구현하기가 쉽습니다.



안내
============
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
============
설치경로 : [https://portal.influxdata.com/downloads/](https://portal.influxdata.com/downloads/)
또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)

```bash
wget https://dl.influxdata.com/telegraf/releases/telegraf-1.19.1-1.x86_64.rpm
```

프로그램 설치 및 최초 실행
============

설치
------------

```bash
[root@downloads]# yum localinstall telegraf-1.19.1-1.x86_64.rpm 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
 
This system is not registered with an entitlement server. You can use subscription-manager to register.
 
Examining telegraf-1.19.1-1.x86_64.rpm: telegraf-1.19.1-1.x86_64
Marking telegraf-1.19.1-1.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package telegraf.x86_64 0:1.19.1-1 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================
 Package                          Arch                           Version                           Repository                                         Size
===========================================================================================================================================================
Installing:
 telegraf                         x86_64                         1.19.1-1                          /telegraf-1.19.1-1.x86_64                         118 M
 
Transaction Summary
===========================================================================================================================================================
Install  1 Package
 
Total size: 118 M
Installed size: 118 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : telegraf-1.19.1-1.x86_64                                                                                                                1/1 
Created symlink from /etc/systemd/system/multi-user.target.wants/telegraf.service to /usr/lib/systemd/system/telegraf.service.
  Verifying  : telegraf-1.19.1-1.x86_64                                                                                                                1/1 
Local_Repo                                                                                                                          | 2.8 kB  00:00:00     
 
Installed:
  telegraf.x86_64 0:1.19.1-1                                                                                                                               
 
Complete!
[root@downloads]# 
```

실행
------------

```bash
[root@downloads]# systemctl start telegraf.service
[root@downloads]# systemctl status telegraf.service
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; vendor preset: disabled)
   Active: active (running) since 금 2021-07-30 08:53:12 KST; 4s ago
     Docs: https://github.com/influxdata/telegraf
 Main PID: 10257 (telegraf)
   CGroup: /system.slice/telegraf.service
           └─10257 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d
 
 7월 30 08:53:12 xxxxxx telegraf[10257]: time="2021-07-30T08:53:12+09:00" level=error msg="failed to create cache directory. /etc/telegraf/....go:120"
 7월 30 08:53:12 xxxxxx telegraf[10257]: time="2021-07-30T08:53:12+09:00" level=error msg="failed to open. Ignored. open /etc/telegraf/.cac....go:120"
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Starting Telegraf 1.19.1
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded inputs: cpu disk diskio kernel mem processes swap system
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded aggregators:
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded processors:
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded outputs: influxdb
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Tags enabled: host=xxxxxx
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"xxxxxx", Flush Interval:10s
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z W! [outputs.influxdb] When writing to [http://localhost:8086]: database "tele...thorized
Hint: Some lines were ellipsized, use -l to show in full.
[root@downloads]# 
```

프로그램 종료
------------

```bash
[root@downloads]# systemctl stop telegraf.service
[root@downloads]# systemctl status telegraf.service
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; vendor preset: disabled)
   Active: inactive (dead) since 금 2021-07-30 08:53:43 KST; 3s ago
     Docs: https://github.com/influxdata/telegraf
  Process: 10257 ExecStart=/usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d $TELEGRAF_OPTS (code=exited, status=0/SUCCESS)
 Main PID: 10257 (code=exited, status=0/SUCCESS)
 
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded processors:
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded outputs: influxdb
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! Tags enabled: host=xxxxxx
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"xxxxxx", Flush Interval:10s
 7월 30 08:53:12 xxxxxx telegraf[10257]: 2021-07-29T23:53:12Z W! [outputs.influxdb] When writing to [http://localhost:8086]: database "tele...thorized
 7월 30 08:53:22 xxxxxx telegraf[10257]: 2021-07-29T23:53:22Z E! [outputs.influxdb] E! [outputs.influxdb] Failed to write metric (will be d...orized):
 7월 30 08:53:32 xxxxxx telegraf[10257]: 2021-07-29T23:53:32Z E! [outputs.influxdb] E! [outputs.influxdb] Failed to write metric (will be d...orized):
 7월 30 08:53:42 xxxxxx telegraf[10257]: 2021-07-29T23:53:42Z E! [outputs.influxdb] E! [outputs.influxdb] Failed to write metric (will be d...orized):
 7월 30 08:53:43 xxxxxx systemd[1]: Stopping The plugin-driven server agent for reporting metrics into InfluxDB...
 7월 30 08:53:43 xxxxxx systemd[1]: Stopped The plugin-driven server agent for reporting metrics into InfluxDB.
Hint: Some lines were ellipsized, use -l to show in full.
[root@downloads]# 
```

삭제(yum remove)
------------

telegraf 종료 후 수행해야 합니다.

```bash
[root@downloads]# yum remove telegraf
Loaded plugins: product-id, search-disabled-repos, subscription-manager
 
This system is not registered with an entitlement server. You can use subscription-manager to register.
 
Resolving Dependencies
--> Running transaction check
---> Package telegraf.x86_64 0:1.19.1-1 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================
 Package                          Arch                           Version                          Repository                                          Size
===========================================================================================================================================================
Removing:
 telegraf                         x86_64                         1.19.1-1                         @/telegraf-1.19.1-1.x86_64                         118 M
 
Transaction Summary
===========================================================================================================================================================
Remove  1 Package
 
Installed size: 118 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Erasing    : telegraf-1.19.1-1.x86_64                                                                                                                1/1 
경고: /etc/telegraf/telegraf.conf(이)가 /etc/telegraf/telegraf.conf.rpmsave(으)로 저장되었습니다
Removed symlink /etc/systemd/system/multi-user.target.wants/telegraf.service.
  Verifying  : telegraf-1.19.1-1.x86_64                                                                                                                1/1 
Local_Repo                                                                                                                          | 2.8 kB  00:00:00     
 
Removed:
  telegraf.x86_64 0:1.19.1-1                                                                                                                               
 
Complete!
[root@downloads]# 
```
