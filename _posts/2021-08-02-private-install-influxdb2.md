---
layout: single                                
title: 폐쇄망 환경에서 influxDB2 설치하기
date: "2021-08-02 10:00:00 +0900"
toc : false
category: 오픈소스 사용기
tags: [VPN, opensource]
---


관제 시스템의 오픈소스 가능성을 알아보기 위해 시계열데이터베이스인 인플럭스DB와 스카우터, 그라파나의 연계를 수행했었는데, 당시 폐쇄망 환경에서 운영을 위해 설치를 수행했었던 기록을 남겨봅니다.

일반
------------
인플럭스DB 에 대한 일반소개 : [https://ko.wikipedia.org/wiki/InfluxDB](https://ko.wikipedia.org/wiki/InfluxDB)

안내
============

해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
============
설치경로 : [https://portal.influxdata.com/downloads/](https://portal.influxdata.com/downloads/)
또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)

```bash
wget https://dl.influxdata.com/influxdb/releases/influxdb2-2.0.7.x86_64.rpm
```

프로그램 설치 및 최초 실행
============

설치
------------

```bash
[root@downloads]# yum list | grep influxdb2
[root@downloads]# yum localinstall influxdb2-2.0.7.x86_64.rpm 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
 
This system is not registered with an entitlement server. You can use subscription-manager to register.
 
Examining influxdb2-2.0.7.x86_64.rpm: influxdb2-2.0.7-1.x86_64
Marking influxdb2-2.0.7.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package influxdb2.x86_64 0:2.0.7-1 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================
 Package                           Arch                           Version                            Repository                                       Size
===========================================================================================================================================================
Installing:
 influxdb2                         x86_64                         2.0.7-1                            /influxdb2-2.0.7.x86_64                         191 M
 
Transaction Summary
===========================================================================================================================================================
Install  1 Package
 
Total size: 191 M
Installed size: 191 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : influxdb2-2.0.7-1.x86_64                                                                                                                1/1Created symlink from /etc/systemd/system/influxd.service to /usr/lib/systemd/system/influxdb.service.
Created symlink from /etc/systemd/system/multi-user.target.wants/influxdb.service to /usr/lib/systemd/system/influxdb.service.
Config file /etc/influxdb/config.toml already exists, writing defaults to /etc/influxdb/config.toml.defaults
  Verifying  : influxdb2-2.0.7-1.x86_64                                                                                                                1/1 
 
Installed:
  influxdb2.x86_64 0:2.0.7-1                                                                                                                               
 
Complete!
[root@downloads]# 
```

실행
------------

```bash
[root@downloads]# systemctl start influxdb.service
[root@downloads]# systemctl status influxdb.service
● influxdb.service - InfluxDB is an open-source, distributed, time series database
   Loaded: loaded (/usr/lib/systemd/system/influxdb.service; enabled; vendor preset: disabled)
   Active: active (running) since 목 2021-07-29 09:50:59 KST; 7h ago
     Docs: https://docs.influxdata.com/influxdb/
 Main PID: 4493 (influxd)
   CGroup: /system.slice/influxdb.service
           └─4493 /usr/bin/influxd
 
 7월 29 16:21:09 xxxxxx influxd[4493]: ts=2021-07-29T07:21:09.160230Z lvl=info msg="Retention policy deletion check (start)" log_id=0Vcwk4...ent=start
 7월 29 16:21:09 xxxxxx influxd[4493]: ts=2021-07-29T07:21:09.160265Z lvl=info msg="Retention policy deletion check (end)" log_id=0Vcwk4h0...d=0.096ms
 7월 29 16:30:50 xxxxxx influxd[4493]: ts=2021-07-29T07:30:50.593512Z lvl=info msg="Cache snapshot (start)" log_id=0Vcwk4h0000 service=sto...ent=start
 7월 29 16:30:50 xxxxxx influxd[4493]: ts=2021-07-29T07:30:50.742818Z lvl=info msg="Snapshot for path written" log_id=0Vcwk4h0000 service=...149.323ms
 7월 29 16:30:50 xxxxxx influxd[4493]: ts=2021-07-29T07:30:50.742847Z lvl=info msg="Cache snapshot (end)" log_id=0Vcwk4h0000 service=stora...149.353ms
 7월 29 16:51:09 xxxxxx influxd[4493]: ts=2021-07-29T07:51:09.160170Z lvl=info msg="Retention policy deletion check (start)" log_id=0Vcwk4...ent=start
 7월 29 16:51:09 xxxxxx influxd[4493]: ts=2021-07-29T07:51:09.160888Z lvl=info msg="Retention policy deletion check (end)" log_id=0Vcwk4h0...d=0.731ms
 7월 29 16:55:24 xxxxxx influxd[4493]: ts=2021-07-29T07:55:24.604292Z lvl=info msg="Cache snapshot (start)" log_id=0Vcwk4h0000 service=sto...ent=start
 7월 29 16:55:24 xxxxxx influxd[4493]: ts=2021-07-29T07:55:24.624348Z lvl=info msg="Snapshot for path written" log_id=0Vcwk4h0000 service=...=20.071ms
 7월 29 16:55:24 xxxxxx influxd[4493]: ts=2021-07-29T07:55:24.624382Z lvl=info msg="Cache snapshot (end)" log_id=0Vcwk4h0000 service=stora...=20.110ms
Hint: Some lines were ellipsized, use -l to show in full.
[root@downloads]# 
```

|제목|화면|비고|
|-------|------|-------|
|최초 화면|![image](https://user-images.githubusercontent.com/23024189/163518676-5f342fe2-3b3a-4ef3-971d-a2d1a1507127.png)|http://<설치서버IP>:8086 접속 및 최초 정보 입력<br>최초 로그인 시 해당 화면으로 진입하여 최초 설정을 진행합니다.|
|초기 설정|![image](https://user-images.githubusercontent.com/23024189/163518706-23e9bb43-846b-4cfc-b628-6b121160b0e7.png)|username, password, initial organization name 및 초기 bucket name 을 입력합니다.<br>해당 가이드에서는 아래와 같이 진행하였습니다.<br>username : admin</br>password :<br>initial organization name :<br>initial bucket name : influxdb-data|
|완료|![image](https://user-images.githubusercontent.com/23024189/163518838-f2fcc8d9-e19f-4535-a9ee-d529b32635c2.png)|최초 데이터 수집 방법을 질의합니다.<br>Quick Start : 초기 설정을 구성합니다. 예제 대시보드 및 예제 수집이 포함됩니다.<br>Advanced : 고급설정을 수행합니다. telegraf 등 설정작업을 수행합니다.<br>Configure Later : 설정을 이후로 미루고 페이지에 진입합니다.|

프로그램 종료
------------

```bash
[root@downloads]# systemctl stop influxdb.service
[root@downloads]# systemctl status influxdb.service
● influxdb.service - InfluxDB is an open-source, distributed, time series database
   Loaded: loaded (/usr/lib/systemd/system/influxdb.service; enabled; vendor preset: disabled)
   Active: inactive (dead) since 목 2021-07-29 17:16:16 KST; 10s ago
     Docs: https://docs.influxdata.com/influxdb/
  Process: 4493 ExecStart=/usr/bin/influxd (code=exited, status=0/SUCCESS)
 Main PID: 4493 (code=exited, status=0/SUCCESS)
 
 7월 29 17:16:15 xxxxxx influxd[4493]: ts=2021-07-29T08:16:15.575958Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=telemetry interval=8h
 7월 29 17:16:15 xxxxxx influxd[4493]: ts=2021-07-29T08:16:15.575983Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=scraper
 7월 29 17:16:15 xxxxxx influxd[4493]: ts=2021-07-29T08:16:15.576119Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=tcp-listener
 7월 29 17:16:16 xxxxxx influxd[4493]: ts=2021-07-29T08:16:16.076144Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=task
 7월 29 17:16:16 xxxxxx influxd[4493]: ts=2021-07-29T08:16:16.076440Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=nats
 7월 29 17:16:16 xxxxxx influxd[4493]: ts=2021-07-29T08:16:16.077189Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=bolt
 7월 29 17:16:16 xxxxxx influxd[4493]: ts=2021-07-29T08:16:16.077522Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=query
 7월 29 17:16:16 xxxxxx influxd[4493]: ts=2021-07-29T08:16:16.079263Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=storage-engine
 7월 29 17:16:16 xxxxxx influxd[4493]: ts=2021-07-29T08:16:16.079278Z lvl=info msg="Closing retention policy enforcement service" log_id=0...retention
 7월 29 17:16:16 xxxxxx systemd[1]: Stopped InfluxDB is an open-source, distributed, time series database.
Hint: Some lines were ellipsized, use -l to show in full.
[root@downloads]# 
```


참고 : 설정초기화
------------
influxDB 설정을 초기화하고 설치과정을 재수행하고 싶을 경우 아래와 같이 수행합니다.   
influxdb 종료 후 수행해야 합니다.

```bash
[root@downloads]# cd /var/lib/influxdb
[root@downloads]# ls -al
합계 48
drwxr-xr-x.  4 influxdb influxdb    54  7월 29 17:26 .
drwxr-xr-x. 31 root     root      4096  7월 29 17:26 ..
drwxr-xr-x.  3 influxdb influxdb    23  7월 29 17:26 .cache
drwxr-xr-x.  3 influxdb influxdb    18  7월 29 17:26 engine
-rw-------.  1 influxdb influxdb 65536  7월 29 17:30 influxd.bolt
[root@downloads]# rm -rf influxd.bolt 
[root@downloads]# 
```


삭제(yum remove)
------------
influxdb 종료 후 수행해야 합니다.

```bash
[root@downloads]# yum list | grep influx
influxdb2.x86_64                        2.0.7-1                    @/influxdb2-2.0.7.x86_64
[root@downloads]# yum remove influxdb2
Loaded plugins: product-id, search-disabled-repos, subscription-manager
 
This system is not registered with an entitlement server. You can use subscription-manager to register.
 
Resolving Dependencies
--> Running transaction check
---> Package influxdb2.x86_64 0:2.0.7-1 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================
 Package                           Arch                           Version                           Repository                                        Size
===========================================================================================================================================================
Removing:
 influxdb2                         x86_64                         2.0.7-1                           @/influxdb2-2.0.7.x86_64                         191 M
 
Transaction Summary
===========================================================================================================================================================
Remove  1 Package
 
Installed size: 191 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Erasing    : influxdb2-2.0.7-1.x86_64                                                                                                                1/1 
Removed symlink /etc/systemd/system/multi-user.target.wants/influxdb.service.
Removed symlink /etc/systemd/system/influxd.service.
  Verifying  : influxdb2-2.0.7-1.x86_64                                                                                                                1/1 
 
Removed:
  influxdb2.x86_64 0:2.0.7-1                                                                                                                               
 
Complete!
[root@downloads]# 
```
