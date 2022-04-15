---
layout: single                                
title: 폐쇄망 환경에서 Scouter2 설치하기
date: "2021-07-29 10:00:00 +0900"
toc : false
category: 오픈소스 사용기
tags: [VPN, opensource]
---

회사에서 WAS 모니터링 용도로 Jennifer 를 사용하고 있는데, 서비스가 늘어남에 따라 늘어나는 비용 소모를 줄일 방법을 모색하게 되었습니다.
이를 위해 오픈소스 APM 툴을 몇가지 찾아보았는데, 그중 Scouter2 를 쓰고 있는 지인에게 추천 받아 최초 설치 테스트 및 그 결과를 가이드라인으로 남기게 되었습니다.
기본적인 내용은 Scouter2 사이트에 모두 소개되어 있지만 정리하는 차원에서 내용을 남깁니다.

안내
=============
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 서비스계정에서 수행하였습니다.

개요
=============
오픈소스 APM인 Scouter는 JVM(WAS, Standalone application)을 사용하는 어플리케이션 및 OS 자원에 대한 모니터링 모니터링 기능을 제공합니다.

SCOUTER의 주요 모니터링 항목 :
사용자 : Active User, Recent User, Today Visitor 등
서비스 : Active Service, TPS, Response Time, Transaction Profile(class,sql,apicall) 등
자원 : Cpu, Memory, Network and Heap usage, Connection pool 등

다운로드
=============
설치 경로 : [https://github.com/scouter-project/scouter/releases/](https://github.com/scouter-project/scouter/releases/)

download 대상 파일 :
+ scouter-all-x.xx.x.x.SNAPSHOT.tar.gz : Agent 및 Server
+ scouter.client.product-macosx.cocoa.x86_64.tar.gz : MAC 용 접속 프로그램
+ scouter.client.product-win32.win32.x86_64.zip : Windows 용 접속 프로그램

또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)

```bash
wget https://github.com/scouter-project/scouter/releases/download/vx.x.x/scouter-all-x.xx.x.x.SNAPSHOT.tar.gz
```

설치 및 실행
=============

참고자료
-------------
설치 매뉴얼(한글) : [https://github.com/scouter-project/scouter/blob/master/scouter.document/main/Setup_kr.md](https://github.com/scouter-project/scouter/blob/master/scouter.document/main/Setup_kr.md)

사전 작업
-------------
+ bash_profile 에 JAVA_PATH 설정 필요
+ 다운로드한 파일을 임의의 위치에 업로드 후 압축 해제

Server
-------------
### 설정
+ 압축해제 한 디렉토리 내의 server , webapp 디렉토리 확인
+ server/conf/scouter.conf 내 아래 정보 입력

```bash
#database directory
db_dir=/data/scouter/server/database #데이터베이스 파일 생성 디렉토리
# log directory
log_dir=/data/scouter/server/logs #scouter 로그 파일 디렉토릭
# udp port
net_udp_listen_port=6100 #collector 에서 전달하는 정보를 수신받을 udp port
# tcp port
net_tcp_listen_port=6100 #collector 에서 전달하는 정보를 수신받을 tcp port
 
net_http_server_enabled=true #scouter http server 실행 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_api_enabled=true #scouter http API 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_port=6180 #scouter RESTful API port 정보
counter_recentuser_valid_ms=300000 #recentuser(현재접속자) 검증 시간(밀리세컨드 단위)
```

### 실행
+ server/startup.sh 수행

### 종료
+ server/stop.sh 실행

Client : OS agent (OS 데이터 수집용)
-------------

### 설정
+ 압축해제 한 디렉토리 내의 agent.host 디렉토리 확인
+ agent.host/conf/scouter.conf 내 아래 정보 입력

```bash
### scouter host configruation sample
net_collector_ip=127.0.0.1 #scouter 서버의 IPv4 Address
net_collector_udp_port=6100 #scouter 서버의 listen port(UDP)
net_collector_tcp_port=6100 #scouter 서버의 listen port(TCP)
counter_interaction_enabled=true #paper topology 를 활성화하기 위한 인터랙션 카운터 활성화
```

### 실행
+ agent.host/host.sh 수행

### 종료
+ agent.host/stop.sh 실행

Client : WAS agent (WAS 데이터 수집용)
-------------

### 설정
+ 압축해제 한 디렉토리 내의 agent.host 디렉토리 확인
+ agent.java/conf/scouter.conf 내 아래 정보 입력

```bash
### scouter java agent configuration sample
obj_name=objectName #해당 instance 의 object name
net_collector_ip=127.0.0.1 #scouter 서버의 IPv4 Address
net_collector_udp_port=6100 #scouter 서버의 listen port(UDP)
net_collector_tcp_port=6100 #scouter 서버의 listen port(TCP)
counter_interaction_enabled=true #paper topology 를 활성화하기 위한 인터랙션 카운터 활성화
```
instance 내 JAVA_OPTS 설정 파일에 아래 내용 추가

```bash
# scouter option
export AGENT_HOME=agent.java 의 위치 지정 # scouter.agent.jar 의 파일 위치 지정
export JAVA_OPTS="$JAVA_OPTS -javaagent:$AGENT_HOME/scouter.agent.jar"
export JAVA_OPTS="$JAVA_OPTS -Dscouter.config=$AGENT_HOME/conf/scouter.conf"
```

### 실행
+ 설정한 WAS 실행

### 종료
+ 설정한 WAS 종료

3rd paraty : 페이퍼 
=============

개요
-------------
[https://scouter-contrib.github.io/scouter-paper/](https://scouter-contrib.github.io/scouter-paper/) 참고

SCOUTER PAPER 프로젝트는 오픈 소스 APM인 SCOUTER WEB API를 활용하여, 성능 데이터를 웹을 통해 확인할 수 있도록 제공하는 대시보드 소프트웨어입니다.
많은 사람들과 기업에서 사용하는 APM인 SCOUTER 클라이언트가 성능과 사용성면에서 매우 훌륭하지만, 플랫폼의 특성으로인한 접근성의 한계가 존재하여, 이를 보완하는 보조 도구의 역할로 사용될 수 있도록 하기 위해 다양한 디바이스에서 접근 가능한 형태의 웹 클라이언트를 만들어 배포하며 시작되었습니다.
PAPER 2.0 부터는 Telegraf 데이터를 지원하고 전체 시스템 성능 상황을 한눈에 파악할 수 있는 토폴로지 뷰를 탑재하면서, 어플리케이션과 인프라 소프트웨어를 아우르는 통합 모니터링 대시보드로 발전하고 있습니다.
SCOUTER PAPER는 아파치 라이선스 2.0을 따르는 오픈 소스 소프트웨어입니다. 해당 라이선스의 배포시 의무사항을 준수하는 방식으로 상업/비상업적인 용도로 자유롭게 사용, 수정 및 재배포가 가능합니다.

다운로드
-------------
+ 설치 경로 : [https://github.com/scouter-contrib/scouter-paper/releases](https://github.com/scouter-contrib/scouter-paper/releases)

설치 및 실행
-------------
### 참고
+ 설치 매뉴얼 : [https://scouter-contrib.github.io/scouter-paper/manual.html](https://scouter-contrib.github.io/scouter-paper/manual.html)

### 설정
+ scouter server 와 같은 경로상의 webapp 를 확인
 
```bash
server/conf/scouter.conf 내 아래 정보 입력(기존 설정 밑에 추가)
net_http_server_enabled=true #scouter http server 실행 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_api_enabled=true #scouter http API 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_port=6180 #scouter RESTful API port 정보
```

+ 다운로드 받은 파일을 scouter/webapp/extweb 밑에 복사 및 scouter 재시작
+ 웹 API 동작 여부 확인

```bash
curl http://{SERVER-ADDRESS}:6180/scouter/v1/info/server
```

+ 아래 주소로 접속 후 동작 여부 확인
+ 접속 url
http://(SERVER-ADDRESS):6188/extweb/index.html

+ net_http_port(6180) 를 pager - setting - scouter web api server info 에 등록
![image](https://user-images.githubusercontent.com/23024189/163379312-3f4d8878-a295-420e-b7d0-8166f76dca8a.png)
