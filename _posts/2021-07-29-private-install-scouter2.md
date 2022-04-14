---
layout: single                                
title: 폐쇄망 환경에서 Scouter2 설치하기
date: "2021-07-29 10:00:00 +0900"
toc : false
category: 오픈소스 사용기
tags: [VPN, opensource]
---

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
설치 경로 : https://github.com/scouter-project/scouter/releases/

download 대상 파일 :

•	scouter-all-x.xx.x.x.SNAPSHOT.tar.gz : Agent 및 Server

•	scouter.client.product-macosx.cocoa.x86_64.tar.gz : MAC 용 접속 프로그램

•	scouter.client.product-win32.win32.x86_64.zip : Windows 용 접속 프로그램

또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)

```bash
wget https://github.com/scouter-project/scouter/releases/download/vx.x.x/scouter-all-x.xx.x.x.SNAPSHOT.tar.gz
```

설치 및 실행
=============

참고자료
-------------
설치 매뉴얼(한글) : https://github.com/scouter-project/scouter/blob/master/scouter.document/main/Setup_kr.md

사전 작업
-------------
.bash_profile 에 JAVA_PATH 설정 필요
다운로드한 파일을 임의의 위치에 업로드 후 압축 해제

Server
-------------
설정
압축해제 한 디렉토리 내의 server , webapp 디렉토리 확인
server/conf/scouter.conf 내 아래 정보 입력

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

실행

server/startup.sh 수행

종료

server/stop.sh 실행

Client : OS agent (OS 데이터 수집용)
-------------

설정

압축해제 한 디렉토리 내의 agent.host 디렉토리 확인

agent.host/conf/scouter.conf 내 아래 정보 입력

```bash
### scouter host configruation sample
net_collector_ip=127.0.0.1 #scouter 서버의 IPv4 Address
net_collector_udp_port=6100 #scouter 서버의 listen port(UDP)
net_collector_tcp_port=6100 #scouter 서버의 listen port(TCP)
counter_interaction_enabled=true #paper topology 를 활성화하기 위한 인터랙션 카운터 활성화
```

실행

agent.host/host.sh 수행

종료

agent.host/stop.sh 실행

Client : WAS agent (WAS 데이터 수집용)
-------------

설정

압축해제 한 디렉토리 내의 agent.host 디렉토리 확인

agent.java/conf/scouter.conf 내 아래 정보 입력


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

실행

설정한 WAS 실행

종료

설정한 WAS 종료


3rd paraty : 페이퍼 
=============

개요
-------------
SCOUTER PAPER 프로젝트는 오픈 소스 APM인 SCOUTER WEB API를 활용하여, 성능 데이터를 웹을 통해 확인할 수 있도록 제공하는 대시보드 소프트웨어입니다.
많은 사람들과 기업에서 사용하는 APM인 SCOUTER 클라이언트가 성능과 사용성면에서 매우 훌륭하지만, 플랫폼의 특성으로인한 접근성의 한계가 존재하여, 이를 보완하는 보조 도구의 역할로 사용될 수 있도록 하기 위해 다양한 디바이스에서 접근 가능한 형태의 웹 클라이언트를 만들어 배포하며 시작되었습니다.
PAPER 2.0 부터는 Telegraf 데이터를 지원하고 전체 시스템 성능 상황을 한눈에 파악할 수 있는 토폴로지 뷰를 탑재하면서, 어플리케이션과 인프라 소프트웨어를 아우르는 통합 모니터링 대시보드로 발전하고 있습니다.
SCOUTER PAPER는 아파치 라이선스 2.0을 따르는 오픈 소스 소프트웨어입니다. 해당 라이선스의 배포시 의무사항을 준수하는 방식으로 상업/비상업적인 용도로 자유롭게 사용, 수정 및 재배포가 가능합니다.

다운로드
-------------
설치 경로 : https://github.com/scouter-contrib/scouter-paper/releases

설치 및 실행
-------------
참고
설치 매뉴얼 : https://scouter-contrib.github.io/scouter-paper/manual.html

설정
scouter server 와 같은 경로상의 webapp 를 확인
 
```bash
server/conf/scouter.conf 내 아래 정보 입력(기존 설정 밑에 추가)
net_http_server_enabled=true #scouter http server 실행 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_api_enabled=true #scouter http API 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_port=6180 #scouter RESTful API port 정보
```

다운로드 받은 파일을 scouter/webapp/extweb 밑에 복사 및 scouter 재시작
웹 API 동작 여부 확인

```bash
curl http://{SERVER-ADDRESS}:6180/scouter/v1/info/server
```

아래 주소로 접속 후 동작 여부 확인
접속 url
http://(SERVER-ADDRESS):6188/extweb/index.html

net_http_port(6180) 를 pager - setting - scouter web api server info 에 등록
![image](https://user-images.githubusercontent.com/23024189/163379312-3f4d8878-a295-420e-b7d0-8166f76dca8a.png)

[Scouter2] third-party : plugin-server-alert-telegram
개요
scouter 메시지를 telegram 으로 전송하기 위한 plugin
다운로드
설치 경로 : https://github.com/scouter-contrib/scouter-plugin-server-alert-telegram/releases
설치 및 진행
참고자료
설치 매뉴얼(한글) : https://github.com/scouter-contrib/scouter-plugin-server-alert-telegram/blob/master/README.md
사전작업
•	telegram bot id 및 chat id 확인
•	api.telegram.org 방화벽 허용 필요
•	cURL 이용하여 아래 메시지 전송 및 테스트 필요
send
curl --location --request GET 'https://api.telegram.org/bot${bot_id}/sendMessage?${chat_id}=-441809740&text=${sampleText}'
 
 
result
{"ok":true,
"result":{"message_id":30125,
    "from":{"id":1055725386,
            "is_bot":true,
            "first_name":"\ub098\uc774\uc2a4\ud398\uc774 \ubaa8\ub2c8\ud130\ub9c1",
            "username":"nicepay_telegram_bot"
        },
    "chat":{"id":-441809740,
            "title":"\uc2a4\ud50c\ub801\ud06c \ud14c\uc2a4\ud2b8",
            "type":"group",
            "all_members_are_administrators":true
        },
    "date":1627287023,
    "text":"test send"
    }
}
Code Block 7 cURL example
설정
Dependency 라이브러리 및 커스터마이징 라이브러리를 스카우터 서버 설치 경로 하위의 lib/ 폴더에 저장한다.
파일명	대상 파일

commons-codec-1.9.jar	commons-codec-1.9.jar

commons-logging-1.2.jar	commons-logging-1.2.jar

gson-2.6.2.jar	gson-2.6.2.jar


httpclient-4.5.2.jar

	httpclient-4.5.2.jar

httpcore-4.4.4.jar	httpcore-4.4.4.jar

scouter-plugin-server-alert-telegram-for-nicepay.jar	scouter-plugin-server-alert-telegram-for-nicepay.jar

server/conf/scouter.conf 내 아래 정보 입력
#telegram plugin
ext_plugin_telegram_send_alert=true #Telegram 메시지 발송 여부 (true / false) - 기본 값은 false
ext_plugin_telegram_debug=true #로깅 여부 - 기본 값은 false
ext_plugin_telegram_level=0 #수신 레벨(0 : INFO, 1 : WARN, 2 : ERROR, 3 : FATAL) - 기본 값은 0
ext_plugin_telegram_bot_token=${bot_id} #Telegram Bot Token
ext_plugin_telegram_chat_id=${chat_id} #chat_id(Integer) 또는 채널 이름(String)
 
ext_plugin_elapsed_time_threshold=5000 #응답시간의 임계치 (ms) - 기본 값은 0으로, 0일때 응답시간의 임계치 초과 여부를 확인하지 않는다.
ext_plugin_gc_time_threshold=5000 #GC Time의 임계치 (ms) - 기본 값은 0으로, 0일때 GC Time의 임계치 초과 여부를 확인하지 않는다.
ext_plugin_thread_count_threshold=300 #Thread Count의 임계치 - 기본 값은 0으로, 0일때 Thread Count의 임계치 초과 여부를 확인하지 않는다.
 
ext_plugin_ignore_name_patterns=*drnpgwas10*,*pg_was_test2* #Alert 메시지 발송에서 제외할 NAME 패턴 목록 (',' 구분자 사용, * (wildcard) 사용 가능)
ext_plugin_ignore_continuous_dup_alert=true #연속된 동일 Alert을 아래 설정시간 동안 제외 - 기본 값은 false
ext_plugin_ignore_continuous_dup_alert_time=60000 #연속된 동일 Alert을 해당 설정시간 동안 제외 - 기본값은 1시간(3600000)
Code Block 8 server/conf/scouter/conf

server/plugin 내 해당 파일(ActiveService.alert) 생성하여 upload
int value = $counter.getIntValue(); //ActiveService count 값
String objName = $counter.getObjName(); //object 이름
 
///openwast01/myTomcat1 object 가 Active Service enable queue 가 3 초과시 alert 발생
if("/openwast01/myTomcat1".equals(objName) && value > 3){
    String title = "Active Service EQ Over";
    title = "Active Service EQ 한계치 초과";
    String message = objName+" is Active Service EQ Count : "+ value;
    $counter.error(title, message);
}
Code Block 9 ActiveService.alert

실행
적용 완료 후 server 재시작
결과
상태	종류	메시지 예시
서비스 기동 완료(최초)	telegram	 
서비스 기동 완료(재기동)	telegram	 
서비스 기동 종료(또는 Out of Memory 발생)	telegram	 
Active Service EQ	client	 
Active Service EQ	paper	 
Active Service EQ	telegram	 
[Scouter2] third-party : scouter-plugin-server-influxdb
개요
scouter 의 성능카운터, object 정보를 influxDB2 에 저장하기 위한 plugin
다운로드
gson-fire-1.8.4.jar
influxdb-client-core-3.1.0.jar
influxdb-client-java-3.1.0.jar
kotlin-stdlib-1.3.70.jar
logging-interceptor-4.7.2.jar
okhttp-4.7.2.jar
okio-2.6.0.jar
reactive-streams-1.0.3.jar
retrofit-2.9.0.jar
rxjava-2.2.19.jar
scouter-plugin-server-influxdb.jar
converter-gson-2.9.0.jar
converter-scalars-2.9.0.jar
gson-2.6.2.jar
설치 및 진행
scouter-plugin-server-influxdb
Scouter server plugin to send influxDB2
•	본 프로젝트는 스카우터 서버 플러그인으로 counter 와 objent 의 값을 influxDB 에 저장하는 역할을 합니다.
Properties (스카우터 서버 설치 경로 하위의 conf/scouter.conf)
•	ext_plugin_influxdb_server : influxDB 의 server url
•	ext_plugin_influxdb_token : influxDB 의 token 값
•	ext_plugin_influxdb_bucket : influxDB 에 저장될 bucket 이름
•	ext_plugin_influxdb_org : influxDB 의 organization 이름
•	ext_plugin_influxdb_counter_enabled : scouter server counter 저장 여부 (true / false) - 기본 값은 true
•	ext_plugin_influxdb_object_enabled : scouter server object 저장 여부 (true / false) - 기본 값은 true
•	ext_plugin_influxdb_counter_measurement : influxDB 에 저장되는 scouter server counter measurement 이름
•	ext_plugin_influxdb_object_measurement : influxDB 에 저장되는 scouter server object measurement 이름
•	ext_plugin_influxdb_debug : 로그 디버깅 옵션(true / false) - 기본 값은 false
•	ext_plugin_influxdb_ignore_name_patterns : 로직에서 제외할 NAME 패턴 목록 (',' 구분자 사용, * (wildcard) 사용 가능)
Example
#influxdb plugin
ext_plugin_influxdb_server=http://127.0.0.1:8086
ext_plugin_influxdb_token=5mV_taCqQozFskRobzxpaZx2s8eiXH3tJnO1HkQ==
ext_plugin_influxdb_bucket=test-data
ext_plugin_influxdb_org=nicepayments
ext_plugin_influxdb_counter_enabled=true
ext_plugin_influxdb_object_enabled=false

ext_plugin_influxdb_counter_measurement=scouter_counter
ext_plugin_influxdb_object_measurement=scouter_object

ext_plugin_influxdb_debug=true
ext_plugin_influxdb_ignore_name_patterns=*myTomcat1*
Dependencies
•	Project
o	scouter.common
o	scouter.server
•	Library
o	converter-gson-2.9.0.jar
o	converter-scalars-2.9.0.jar
o	gson-2.6.2.jar
o	gson-fire-1.8.4.jar
o	influxdb-client-core-3.1.0.jar
o	influxdb-client-java-3.1.0.jar
o	kotlin-stdlib-1.3.70.jar
o	logging-interceptor-4.7.2.jar
o	okhttp-4.7.2.jar
o	okio-2.6.0.jar
o	reactive-streams-1.0.3.jar
o	retrofit-2.9.0.jar
o	rxjava-2.2.19.jar
Build & Deploy
•	Build
o	프로젝트 내의 build.xml을 실행합니다.
•	Deploy
o	빌드 후 프로젝트 하위에 out 디렉토리가 생기며, 디펜던시 라이브러리와 함께 scouter-plugin-server-influxdb.jar 파일을 복사하여 스카우터 서버 설치 경로 하위의 lib/ 폴더에 저장 후 재기동 합니다.

