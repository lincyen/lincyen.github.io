
하위페이지
APM : Scouter
•	[Scouter2] 설치/실행 안내
•	[Scouter2] Client 실행 방법
•	[Scouter2] third-party : 페이퍼
•	[Scouter2] third-party : plugin-server-alert-telegram
•	[Scouter2] third-party : scouter-plugin-server-influxdb
•	_temp:WAS 설치
•	[Scouter2] Trubleshooting
TSDB : InfluxDB
•	[InfluxDB2] 설치/실행 안내
•	[InfluxDB2] GUI 사용법
o	[InfluxDB2] Load Data
	[InfluxDB2] Sources
	[InfluxDB2] Buckets
	[InfluxDB2] Telegraf
	[InfluxDB2] TBD - Scrapers
	[InfluxDB2] Tokens
o	[InfluxDB2] Data Explorer
o	[InfluxDB2] Dashboards
•	[InfluxDB2] CLI Command
Agent : Telegraf
•	[Telegraf] 설치/실행 안내
•	[Telegraf] inputs plugin
•	[Telegraf] output plugin 설정 - InfluxDB2
•	[Telegraf] Trubleshooting
Dashboard : Grafana
•	[Grafana] 설치/실행 안내
•	[Grafana] GUI 사용법
•	[Grafana] Data source 연동 - InfluxDB2
데이터 처리 어플리케이션
•	ELK Stack
o	[Elasticsearch] 설치/실행 안내
o	[Kibana] 설치/실행 안내
o	[Kibana] 화면 기능
o	[ELK Stack] Trubleshooting
o	[ELK] 기타
	[작업중][Elasticsearch] 추가설정
•	Opensearch
o	[opensearch] 설치/실행 안내
o	[logstash] 환경설정 방법
o	[OpenSearch] 대시보드 사용방법
o	[Opensearch] Trubleshooting
o	_temp [opensearch] 설치/실행 안내
•	Beats
o	[Filebeat] 설치/실행 안내
o	[Filebeat] 환경설정 방법
OSS 기반 관제 시스템 구성도
__temp
Maven dependencies download
Container : docker
•	[docker] 디스크 볼륨 관리
•	[docker] 설치/실행 안내
o	[docker] compose v2 설치/실행 안내
•	[docker] 이미지 관리
•	[docker] 컨테이너 관리
o	[docker] compose 구성 및 실행
CI/CD : GitLab
•	[Gitlab] 운영자 가이드
o	[Gitlab] 설치/실행 안내
o	[Gitlab] SMTP 설정
o	[Gitlab] 계정관리
•	[Gitlab] 사용자 가이드
o	[Gitlab] 계정 만들기
o	[Gitlab] Gitlab 에 ssh key 적용
o	[Gitlab] 그룹
o	[Gitlab] 프로젝트
•	[Gitlab] 기타
o	[Gitlab] Eclipse 에서 git 다루기
o	[Gitlab] 기본적인 git 안내
o	[Gitlab] .gitignore
o	_temp gitlab 학습하기
APM : Scouter
개요
오픈소스 APM인 Scouter는 JVM(WAS, Standalone application)을 사용하는 어플리케이션 및 OS 자원에 대한 모니터링 모니터링 기능을 제공한다.
APM : Application performance montoring / application performance management
모니터링 대상 (전용 agent)
Java Agent : Web application (on Tomcat, JBoss, Resin ...), Standalone java application
Host Agent : Linux, Windows, Unix
모니터링 대상 (Telegraf support)
Redis, nginX, apache httpd, haproxy, Kafka, MySQL, MongoDB, RabbitMQ, ElasticSearch, Kube, Mesos ...
모니터링 대상 (Zipkin-Scouter storage)
zipkin instrumentations (C#, Go, Python, Javascript, PHP...)를 XLog 차트를 통해 디스플레이합니다.
see the zipkin-scouter-storage documentation.
see the zipkin instrumentations.
screen
 
사용자는 시스템에 서비스 요청을 보내고, 이를 통해 서비스는 시스템의 자원을 사용하게 된다. 시스템 성능을 잘 이해하고 관리하기 위해서는 사용자와 서비스, 자원간의 관계를 이해하고 접근하는 것이 중요하며 SCOUTER를 활용하여 보다 쉽게 이에 대한 접근이 가능하다.
SCOUTER의 주요 모니터링 항목 :
사용자 : Active User, Recent User, Today Visitor 등
서비스 : Active Service, TPS, Response Time, Transaction Profile(class,sql,apicall) 등
자원 : Cpu, Memory, Network and Heap usage, Connection pool 등.
하위페이지
•	[Scouter2] 설치/실행 안내
•	[Scouter2] Client 실행 방법
•	[Scouter2] third-party : 페이퍼
•	[Scouter2] third-party : plugin-server-alert-telegram
•	[Scouter2] third-party : scouter-plugin-server-influxdb
•	_temp:WAS 설치
•	[Scouter2] Trubleshooting
[Scouter2] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 서비스계정(pg)에서 수행하였습니다.

다운로드
설치 경로 : https://github.com/scouter-project/scouter/releases/
download 대상 파일 :
•	scouter-all-x.xx.x.x.SNAPSHOT.tar.gz : Agent 및 Server 
•	scouter.client.product-macosx.cocoa.x86_64.tar.gz : MAC 용 접속 프로그램
•	scouter.client.product-win32.win32.x86_64.zip : Windows 용 접속 프로그램

또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)
wget https://github.com/scouter-project/scouter/releases/download/vx.x.x/scouter-all-x.xx.x.x.SNAPSHOT.tar.gz
설치 및 실행
참고자료
설치 매뉴얼(한글) : https://github.com/scouter-project/scouter/blob/master/scouter.document/main/Setup_kr.md
사전 작업
.bash_profile 에 JAVA_PATH 설정 필요
다운로드한 파일을 임의의 위치에 업로드 후 압축 해제
Server
설정
압축해제 한 디렉토리 내의 server , webapp 디렉토리 확인
server/conf/scouter.conf 내 아래 정보 입력
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
Code Block 1 server/conf/scouter/conf

실행
server/startup.sh 수행
종료
server/stop.sh 실행
Client : OS agent (OS 데이터 수집용)
설정
압축해제 한 디렉토리 내의 agent.host 디렉토리 확인
agent.host/conf/scouter.conf 내 아래 정보 입력
### scouter host configruation sample
net_collector_ip=127.0.0.1 #scouter 서버의 IPv4 Address
net_collector_udp_port=6100 #scouter 서버의 listen port(UDP)
net_collector_tcp_port=6100 #scouter 서버의 listen port(TCP)
counter_interaction_enabled=true #paper topology 를 활성화하기 위한 인터랙션 카운터 활성화
Code Block 2 agent.host/conf/scouter/conf

실행
agent.host/host.sh 수행
종료
agent.host/stop.sh 실행
Client : WAS agent (WAS 데이터 수집용)
설정
압축해제 한 디렉토리 내의 agent.host 디렉토리 확인
agent.java/conf/scouter.conf 내 아래 정보 입력
### scouter java agent configuration sample
obj_name=objectName #해당 instance 의 object name
net_collector_ip=127.0.0.1 #scouter 서버의 IPv4 Address
net_collector_udp_port=6100 #scouter 서버의 listen port(UDP)
net_collector_tcp_port=6100 #scouter 서버의 listen port(TCP)
counter_interaction_enabled=true #paper topology 를 활성화하기 위한 인터랙션 카운터 활성화
Code Block 3 agent.java/conf/scouter/conf

instance 내 JAVA_OPTS 설정 파일에 아래 내용 추가
# scouter option
export AGENT_HOME=agent.java 의 위치 지정 # scouter.agent.jar 의 파일 위치 지정
export JAVA_OPTS="$JAVA_OPTS -javaagent:$AGENT_HOME/scouter.agent.jar"
export JAVA_OPTS="$JAVA_OPTS -Dscouter.config=$AGENT_HOME/conf/scouter.conf"
Code Block 4 tomcat option

실행
설정한 WAS 실행
종료
설정한 WAS 종료
Client : Batch agent (독립실행형 수집용)
 TBD 
[Scouter2] Client 실행 방법
다운로드
설치 경로 : https://github.com/scouter-project/scouter/releases/
download 대상 파일 :
•	scouter-all-x.xx.x.x.SNAPSHOT.tar.gz : Agent 및 Server 
•	scouter.client.product-macosx.cocoa.x86_64.tar.gz : MAC 용 접속 프로그램
•	scouter.client.product-win32.win32.x86_64.zip : Windows 용 접속 프로그램
설치 및 실행
사전작업
•	JDK1.8+ 설치 필요
실행
1.	OS 에 맞는 버전의 압축파일 해제 후 scouter.client 디렉토리 내 scouter 실행파일 클릭
2.	IP:Port 입력 및 계정/패스워드 입력(초기값: admin/admin)
 

[Scouter2] third-party : 페이퍼
개요
SCOUTER PAPER 프로젝트는 오픈 소스 APM인 SCOUTER WEB API를 활용하여, 성능 데이터를 웹을 통해 확인할 수 있도록 제공하는 대시보드 소프트웨어입니다.
많은 사람들과 기업에서 사용하는 APM인 SCOUTER 클라이언트가 성능과 사용성면에서 매우 훌륭하지만, 플랫폼의 특성으로인한 접근성의 한계가 존재하여, 이를 보완하는 보조 도구의 역할로 사용될 수 있도록 하기 위해 다양한 디바이스에서 접근 가능한 형태의 웹 클라이언트를 만들어 배포하며 시작되었습니다.
PAPER 2.0 부터는 Telegraf 데이터를 지원하고 전체 시스템 성능 상황을 한눈에 파악할 수 있는 토폴로지 뷰를 탑재하면서, 어플리케이션과 인프라 소프트웨어를 아우르는 통합 모니터링 대시보드로 발전하고 있습니다.
SCOUTER PAPER는 아파치 라이선스 2.0을 따르는 오픈 소스 소프트웨어입니다. 해당 라이선스의 배포시 의무사항을 준수하는 방식으로 상업/비상업적인 용도로 자유롭게 사용, 수정 및 재배포가 가능합니다.
다운로드
설치 경로 : https://github.com/scouter-contrib/scouter-paper/releases
설치 및 실행
참고
설치 매뉴얼 : https://scouter-contrib.github.io/scouter-paper/manual.html
설정
scouter server 와 같은 경로상의 webapp 를 확인
 
server/conf/scouter.conf 내 아래 정보 입력(기존 설정 밑에 추가)
net_http_server_enabled=true #scouter http server 실행 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_api_enabled=true #scouter http API 옵션 실행(third-party 솔루션 사용 및 RESTful API 활성화 용도)
net_http_port=6180 #scouter RESTful API port 정보
Code Block 5 server/conf/scouter/conf

다운로드 받은 파일을 scouter/webapp/extweb 밑에 복사 및 scouter 재시작
웹 API 동작 여부 확인
curl http://{SERVER-ADDRESS}:6180/scouter/v1/info/server
Code Block 6 web api call

아래 주소로 접속 후 동작 여부 확인
접속 url
http://(SERVER-ADDRESS):6188/extweb/index.html

net_http_port(6180) 를 pager - setting - scouter web api server info 에 등록
 
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
_temp:WAS 설치
싸이웰-setenv.sh 추가
# scouter option
export AGENT_HOME=/home/${TOMCAT_USER}/agent/agent.java/ # the location of scouter.agent.jar
if [ "$1" = "start" -o "$1" = "run" ]; then
export JAVA_OPTS="$JAVA_OPTS -javaagent:$AGENT_HOME/scouter.agent.jar"
export JAVA_OPTS="$JAVA_OPTS -Dscouter.config=$AGENT_HOME/conf/scouter.conf"
fi

sia.conf 추가
# scouter option
export AGENT_HOME=/home/jboss/agent/scouter/agent.java/ # the location of scouter.agent.jar
if [ "$2" = "start" -o "$2" = "run" ]; then
  export JAVA_OPTS="$JAVA_OPTS -javaagent:$AGENT_HOME/scouter.agent.jar"
  export JAVA_OPTS="$JAVA_OPTS -Dscouter.config=$AGENT_HOME/conf/scouter.conf"
fi

host	agent dir	설정파일 위치	agent.java	agent.host	agent.batch
					
pg_was_test2	/home/jboss/agent/scouter/	/home/jboss/was/instance/pgtest/conf/sia.conf			
drnpgwas10	/home/jboss/agent/scouter/	/home/jboss/was/instance/pgtest/conf/	O	O	
java.io.IOException : 소켓 데이터 전송을 위한 메시지가 너무 깁니다.(sendto failed)

version	1.19.1-1
영향도	 높음 
원인	UDP Packet Size 초과 문제 (이슈번호 #433)
내용	java.io.IOException : Message too long UDP
java.io.IOException : 소켓 데이터 전송을 위한 메시지가 너무 깁니다.(sendto failed)


참고	https://github.com/scouter-project/scouter/issues/433

해결방법	conf/scouter.conf 내 net_udp_packet_max_bytes 값 변경(기본 6000)
커널 udp 전송 버퍼 세팅값도 확인 필요
TSDB : InfluxDB
개요
일반
개발자	인플럭스데이터(InfluxData)
발표일	2013년 9월 24일
프로그래밍 언어	Go
종류	시계열 데이터베이스
라이선스	MIT
웹사이트	influxdata.com


InfluxDB는 인플럭스데이터가 개발한 오픈 소스 시계열 데이터베이스(TSDB)이다.
Go 언어로 작성되었으며 운영 모니터링, 애플리케이션 매트릭스, 사물인터넷 센서 데이터, 실시간 분석 등 분야에서 시계열 데이터의 고속의 고가용성(HA)의 저장 및 검색에 최적화되어 있다.
그래파이트로부터 데이터를 처리하는 기능도 지원한다.
역사
Y 콤비네이터의 지원을 받는 Errplane[4]은 2013년 말 성능 모니터링 및 경보 처리를 위한 오픈 소스 프로젝트의 하나로서 InfluxDB를 개발하기 시작했다.
Errplane은 2014년 11월 메이필드 펀드와 트리니티 벤처스가 주도하는 $8.1M 시리즈 A 파이낸싱 수익을 거두었다.
2015년 말, Errplane은 공식적으로 사명을 InfluxData Inc로 변경하였다.
InfluxData는 2016년 9월 $16M의 시리즈 B 펀딩 라운드 수익을 거두었다. 2018년 2월, InfluxData는 사파이어 벤처스 주도의 $35,000,000 시리즈 C 라운드 펀딩을 마무리했다.
기술 개요
InfluxDB는 외부 의존성이 없으며 SQL 계열 언어를 제공하고 8086 포트를 리스닝하며, 메저먼트(measurement), 시리즈(series), 포인트(point)으로 구성되는 자료 구조를 조회하기 위한 시간 중심 함수를 내장하고 있다.
각 포인트는 필드셋으로 불리는 여러 키-값 쌍, 그리고 타임스탬프를 구성한다.
키-값 쌍으로 함께 묶으면 이를 태그셋(tagset)이라 부르며 이를 통해 시리즈를 정의한다.
끝으로, 문자열 식별자를 통해 시리즈를 함께 묶으면 메저먼트가 된다.
값은 64비트 정수, 64비트 부동소수점, 문자열, 불리언(참/거짓)이 될 수 있다.
포인트는 시간과 태그셋으로 인덱싱된다.

출처 : 한글위키디피아, https://ko.wikipedia.org/wiki/InfluxDB
하위페이지
•	[InfluxDB2] 설치/실행 안내
•	[InfluxDB2] GUI 사용법
o	[InfluxDB2] Load Data
	[InfluxDB2] Sources
	[InfluxDB2] Buckets
	[InfluxDB2] Telegraf
	[InfluxDB2] TBD - Scrapers
	[InfluxDB2] Tokens
o	[InfluxDB2] Data Explorer
o	[InfluxDB2] Dashboards
•	[InfluxDB2] CLI Command
[InfluxDB2] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
설치경로 : https://portal.influxdata.com/downloads/
또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)
wget https://dl.influxdata.com/influxdb/releases/influxdb2-2.0.7.x86_64.rpm
프로그램 설치 및 최초 실행
설치
[root@openwast01 downloads]# yum list |grep influxdb2
[root@openwast01 downloads]# yum localinstall influxdb2-2.0.7.x86_64.rpm 
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
[root@openwast01 downloads]# 
Code Block 10 influxdb2 install

실행
[root@openwast01 downloads]# systemctl start influxdb.service
[root@openwast01 downloads]# systemctl status influxdb.service
● influxdb.service - InfluxDB is an open-source, distributed, time series database
   Loaded: loaded (/usr/lib/systemd/system/influxdb.service; enabled; vendor preset: disabled)
   Active: active (running) since 목 2021-07-29 09:50:59 KST; 7h ago
     Docs: https://docs.influxdata.com/influxdb/
 Main PID: 4493 (influxd)
   CGroup: /system.slice/influxdb.service
           └─4493 /usr/bin/influxd
 
 7월 29 16:21:09 openwast01 influxd[4493]: ts=2021-07-29T07:21:09.160230Z lvl=info msg="Retention policy deletion check (start)" log_id=0Vcwk4...ent=start
 7월 29 16:21:09 openwast01 influxd[4493]: ts=2021-07-29T07:21:09.160265Z lvl=info msg="Retention policy deletion check (end)" log_id=0Vcwk4h0...d=0.096ms
 7월 29 16:30:50 openwast01 influxd[4493]: ts=2021-07-29T07:30:50.593512Z lvl=info msg="Cache snapshot (start)" log_id=0Vcwk4h0000 service=sto...ent=start
 7월 29 16:30:50 openwast01 influxd[4493]: ts=2021-07-29T07:30:50.742818Z lvl=info msg="Snapshot for path written" log_id=0Vcwk4h0000 service=...149.323ms
 7월 29 16:30:50 openwast01 influxd[4493]: ts=2021-07-29T07:30:50.742847Z lvl=info msg="Cache snapshot (end)" log_id=0Vcwk4h0000 service=stora...149.353ms
 7월 29 16:51:09 openwast01 influxd[4493]: ts=2021-07-29T07:51:09.160170Z lvl=info msg="Retention policy deletion check (start)" log_id=0Vcwk4...ent=start
 7월 29 16:51:09 openwast01 influxd[4493]: ts=2021-07-29T07:51:09.160888Z lvl=info msg="Retention policy deletion check (end)" log_id=0Vcwk4h0...d=0.731ms
 7월 29 16:55:24 openwast01 influxd[4493]: ts=2021-07-29T07:55:24.604292Z lvl=info msg="Cache snapshot (start)" log_id=0Vcwk4h0000 service=sto...ent=start
 7월 29 16:55:24 openwast01 influxd[4493]: ts=2021-07-29T07:55:24.624348Z lvl=info msg="Snapshot for path written" log_id=0Vcwk4h0000 service=...=20.071ms
 7월 29 16:55:24 openwast01 influxd[4493]: ts=2021-07-29T07:55:24.624382Z lvl=info msg="Cache snapshot (end)" log_id=0Vcwk4h0000 service=stora...=20.110ms
Hint: Some lines were ellipsized, use -l to show in full.
[root@openwast01 downloads]# 
Code Block 11 influxdb2 start

제목	화면	비고
최초 화면	 	http://<설치서버IP>:8086 접속 및 최초 정보 입력
최초 로그인 시 해당 화면으로 진입하여 최초 설정을 진행합니다.

초기 설정	 	username, password, initial organization name 및 초기 bucket name 을 입력합니다.
해당 가이드에서는 아래와 같이 진행하였습니다.
username : admin
password : skdltm100%
initial organization name : nicepayments
initial bucket name : influxdb-data
완료	 	최초 데이터 수집 방법을 질의합니다.
Quick Start : 초기 설정을 구성합니다. 예제 대시보드 및 예제 수집이 포함됩니다.
Advanced : 고급설정을 수행합니다. telegraf 등 설정작업을 수행합니다.
Configure Later : 설정을 이후로 미루고 페이지에 진입합니다.

프로그램 종료

[root@openwast01 downloads]# systemctl stop influxdb.service
[root@openwast01 downloads]# systemctl status influxdb.service
● influxdb.service - InfluxDB is an open-source, distributed, time series database
   Loaded: loaded (/usr/lib/systemd/system/influxdb.service; enabled; vendor preset: disabled)
   Active: inactive (dead) since 목 2021-07-29 17:16:16 KST; 10s ago
     Docs: https://docs.influxdata.com/influxdb/
  Process: 4493 ExecStart=/usr/bin/influxd (code=exited, status=0/SUCCESS)
 Main PID: 4493 (code=exited, status=0/SUCCESS)
 
 7월 29 17:16:15 openwast01 influxd[4493]: ts=2021-07-29T08:16:15.575958Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=telemetry interval=8h
 7월 29 17:16:15 openwast01 influxd[4493]: ts=2021-07-29T08:16:15.575983Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=scraper
 7월 29 17:16:15 openwast01 influxd[4493]: ts=2021-07-29T08:16:15.576119Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=tcp-listener
 7월 29 17:16:16 openwast01 influxd[4493]: ts=2021-07-29T08:16:16.076144Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=task
 7월 29 17:16:16 openwast01 influxd[4493]: ts=2021-07-29T08:16:16.076440Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=nats
 7월 29 17:16:16 openwast01 influxd[4493]: ts=2021-07-29T08:16:16.077189Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=bolt
 7월 29 17:16:16 openwast01 influxd[4493]: ts=2021-07-29T08:16:16.077522Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=query
 7월 29 17:16:16 openwast01 influxd[4493]: ts=2021-07-29T08:16:16.079263Z lvl=info msg=Stopping log_id=0Vcwk4h0000 service=storage-engine
 7월 29 17:16:16 openwast01 influxd[4493]: ts=2021-07-29T08:16:16.079278Z lvl=info msg="Closing retention policy enforcement service" log_id=0...retention
 7월 29 17:16:16 openwast01 systemd[1]: Stopped InfluxDB is an open-source, distributed, time series database.
Hint: Some lines were ellipsized, use -l to show in full.
[root@openwast01 downloads]# 
Code Block 12 influxdb2 stop


참고 : 설정초기화

influxDB 설정을 초기화하고 설치과정을 재수행하고 싶을 경우 아래와 같이 수행합니다.

influxdb 종료 후 수행해야 합니다.

[root@openwast01 influxdb]# cd /var/lib/influxdb
[root@openwast01 influxdb]# ls -al
합계 48
drwxr-xr-x.  4 influxdb influxdb    54  7월 29 17:26 .
drwxr-xr-x. 31 root     root      4096  7월 29 17:26 ..
drwxr-xr-x.  3 influxdb influxdb    23  7월 29 17:26 .cache
drwxr-xr-x.  3 influxdb influxdb    18  7월 29 17:26 engine
-rw-------.  1 influxdb influxdb 65536  7월 29 17:30 influxd.bolt
[root@openwast01 influxdb]# rm -rf influxd.bolt 
[root@openwast01 influxdb]# 
Code Block 13 influxdb2 initial


삭제(yum remove)

influxdb 종료 후 수행해야 합니다.

[root@openwast01 ~]# yum list | grep influx
influxdb2.x86_64                        2.0.7-1                    @/influxdb2-2.0.7.x86_64
[root@openwast01 ~]# yum remove influxdb2
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
[root@openwast01 ~]# 
Code Block 14 influxdb2 remove

[InfluxDB2] GUI 사용법
로그인
1.	url : http://<SERVER-IP>:8086/signin 접속
2.	생성된 username 과 패스워드 입력
 


계정 생성 및 패스워드 변경은 [InfluxDB2] CLI Command 를 참고하시기 바랍니다.
로그아웃
1.	Getting Started 오른쪽 상단 Account 의 logout 선택
2.	계정 정보 클릭 후 Logout 클릭
 

페이지 기능
•	[InfluxDB2] Load Data
o	[InfluxDB2] Sources
o	[InfluxDB2] Buckets
o	[InfluxDB2] Telegraf
o	[InfluxDB2] TBD - Scrapers
o	[InfluxDB2] Tokens
•	[InfluxDB2] Data Explorer
•	[InfluxDB2] Dashboards
[InfluxDB2] Load Data
개요
InfluxDB 로 데이터를 입력할 수 있는 Source 목록에 대해서 가이드하는 페이지.
해당 페이지 자체로 어떤 기능을 수행하지는 않습니다.
Client Libraries
언어별 라이브러리 제공을 통해 클라이언트 구현 및 연동할 수 있도록 가이드 하는 페이지
라이브러리 다운로드 방법 및 소스코드 가이드를 제공합니다.
Telegraf Plugins
경량 Agent 프로젝트인 Telegraf 를 통해서 수집 가능한 데이터 목록을 제공합니다.
Telegraf 설정 정보를 제공하여 손쉽게 telegraf 와 influxdb 간 연동 가능합니다.
참고 : [Telegraf] inputs plugin
[InfluxDB2] Buckets
개요
데이터가 저장되는 장소로 검색의 기본 단위가 됩니다.
Bucket 생성
1.	Create Bucket 버튼 클릭
 

2.	Bucket 이름과 데이터 보관주기 선택(1시간 에서 1년까지 지정된 주기 선택 가능, 또는 Never 선택하여 영구 보관 가능)
 

3.	Bucket 의 이름은 앞에 _ 를 붙일 수 없음(system bucket 만 가능)
4.	생성 후 bucket 의 데이터 보관주기와 이름을 Setting 버튼을 통해 변경 가능
5.	+Add data 버튼을 통해 데이터 적재 가능
[InfluxDB2] Telegraf
개요
경량 OSS Agent 인 Telegraf 를 이용하여 수집된 데이터를 InfluxDB2 에 적재 가능

사전 준비
1.	telegraf 가 설치되어 있어야 함
2.	[Telegraf] 설치/실행 안내 참고
설정 생성
1.	Create Configuration 클릭
2.	수집된 데이터를 저장할 Bucket 선택
3.	Bucket 생성은 [InfluxDB2] Buckets 참고
4.	수집할 대상 데이터를 선택(중복 선택 가능)
 

5.	설정 이름 및 설명 등록
 

6.	제공된 정보를 통해 데이터 수집 가능(영구 수집 설정을 위해서는 텔레그라프 설정 정보 등록 필요)

 
[pg@openwast01 ~]$ export INFLUX_TOKEN=$INFLUX_TOKEN
[pg@openwast01 ~]$ telegraf --config http://172.30.23.221:8086/api/v2/telegrafs/07e976cb7700f000
2021-07-30T05:24:56Z I! Starting Telegraf 1.19.1
2021-07-30T05:24:56Z I! Loaded inputs: cpu disk diskio mem net processes swap system
2021-07-30T05:24:56Z I! Loaded aggregators: 
2021-07-30T05:24:56Z I! Loaded processors: 
2021-07-30T05:24:56Z I! Loaded outputs: influxdb_v2
2021-07-30T05:24:56Z I! Tags enabled: host=openwast01
2021-07-30T05:24:56Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"openwast01", Flush Interval:10s
Code Block 15 telegraf output test calll
7.	수집 데이터는 Explore 메뉴 또는 System Dashboard 를 통해 확인 가능
[InfluxDB2] TBD - Scrapers
 TO BE DETERMINED 
[InfluxDB2] Tokens
개요
InfluxDB 의 자원을 사용하기 위한 인증Token 관리 페이지
Token 생성

Token 생성 권한이 있는 계정으로 생성 가능합니다.(예: admin)

1.	Bucket 별 Read/write 권한 부여
a.	Generate Token 선택 후 Read/Write Token 선택
 

b.	Read / Write 대상 Bucket 선택 후 생성
 

 

2.	전체 권한 부여
a.	Generate Token 선택 후 All Access Token 선택
 

Token 조회

1.	InfluxDB 로그인 후 Load Data - Tokens  확인
 

2.	필요한 토큰 확인하여 해당 토큰 클릭
3.	해당 토큰의 값을 확인/복사
 


Token Active/Inactive
1.	토큰 사용 중지 시, 토큰 목록에서 Inactive 선택 가능
 

Token 삭제
1.	Delete 버튼으로 삭제 가능
 

[InfluxDB2] Data Explorer
[InfluxDB2] Dashboards
[InfluxDB2] CLI Command
사용자 추가/조회/변경/삭제

TOKEN 사용
authorizations, users 의 read / write 권한이 있는 TOKEN 을 필요로 합니다.(일반적으로 admin`s Token)
아래 CLI command 에서 $INFLUX_TOKEN 으로 표기합니다.

CLI 모드만 가능
사용자 추가/변경/삭제는 CLI 모드에서만 가능합니다. GUI 모드에서 사용자 조회는 가능하나, 삭제 시 실제 ID 가 삭제되지는 않습니다.

토큰 확인 방법
[InfluxDB2] Tokens 의 조회 참고
사용자 추가
[pg@openwast01 ~]$ influx user create -n hsyou -o nicepayments -t $INFLUX_TOKEN
ID                  Name
07e93e2d29c4b000    hsyou
2021-07-30T01:15:48.778501Z warn    Initial password not set for user, use `influx user password` to set it {"log_id": "0VeFYpe0000", "user": "hsyou"}
[pg@openwast01 ~]$ 
Code Block 16 user create

사용자 추가(패스워드 포함)
[pg@openwast01 ~]$ influx user create -n hsyou -p XXXXXXXX -o nicepayments -t $INFLUX_TOKEN
ID                  Name
07e93fb11e84b000    hsyou
[pg@openwast01 ~]$ 
Code Block 17 user create with password

사용자 조회
[pg@openwast01 ~]$ influx user list -t $INFLUX_TOKEN
ID                  Name
07e85cb78644b000    admin
07e93fb11e84b000    hsyou
Code Block 18 user read

사용자 변경
[pg@openwast01 ~]$ influx user list -t $INFLUX_TOKEN
ID                  Name
07e85cb78644b000    admin
07e93fb11e84b000    hsyou
[pg@openwast01 ~]$ influx user update -i 07e93fb11e84b000 -n hsyou2 -t $INFLUX_TOKEN
ID                  Name
07e93fb11e84b000    hsyou2
[pg@openwast01 ~]$ 
[pg@openwast01 ~]$ influx user list -t $INFLUX_TOKEN
ID                  Name
07e85cb78644b000    admin
07e93fb11e84b000    hsyou2
Code Block 19 user update

사용자 패스워드 변경
[pg@openwast01 ~]$ influx user password -n hsyou2 -t $INFLUX_TOKEN
Please type your new password: 
 
Please type your new password again: 
 
Your password has been successfully updated.
[pg@openwast01 ~]$ 
Code Block 20 user update at password

사용자 삭제
[pg@openwast01 ~]$ influx user list -t $INFLUX_TOKEN
ID                  Name
07e85cb78644b000    admin
07e93e2d29c4b000    hsyou
[pg@openwast01 ~]$ influx user delete -i 07e93e2d29c4b000 -t $INFLUX_TOKEN
ID                  Name    Deleted
07e93e2d29c4b000    hsyou   true
[pg@openwast01 ~]$ influx user list -t $INFLUX_TOKEN
ID                  Name
07e85cb78644b000    admin
[pg@openwast01 ~]$ 
Code Block 21 user delete

Bucket 데이터 관리
데이터 삭제
[pg@openwast01 server]$ influx delete --bucket $BUCKET_NAME -o nicepayments --start 2020-03-01T00:00:00Z --stop 2021-08-03T00:00:00Z -t $INFLUX_TOKEN
[pg@openwast01 server]$ 
Code Block 22 data delete

Agent : Telegraf
개요
텔레그라프란?
Telegraf는 데이터베이스, 시스템 및 IoT 센서에서 메트릭 및 이벤트를 수집하고 전송하기 위한 플러그인 기반 서버 에이전트입니다.
Telegraf는 Go로 작성되었으며 외부 종속성이 없는 단일 바이너리로 컴파일되며 매우 최소한의 메모리 사용 공간이 필요합니다.
텔레그라프를 사용하는 이유
모든 종류의 데이터 수집 및 전송:
데이터베이스: MongoDB, MySQL, Redis 등과 같은 데이터 소스에 연결하여 메트릭을 수집하고 보냅니다.
시스템: 최신 클라우드 플랫폼, 컨테이너 및 오케스트레이터 스택에서 메트릭을 수집합니다.
IoT 센서: IoT 센서 및 장치에서 중요한 상태 저장 데이터(압력 수준, 온도 수준 등)를 수집합니다.
Agent : Telegraf는 다양한 입력에서 메트릭을 수집하고 이를 다양한 출력에 쓸 수 있습니다. 데이터 수집 및 출력 모두 플러그인 기반이므로 쉽게 확장할 수 있습니다. Go로 작성되었습니다. 즉, 외부 종속성, npm, pip, gem 또는 기타 패키지 관리 도구 없이 모든 시스템에서 실행할 수 있는 컴파일된 독립 실행형 바이너리입니다.
Coverage : 커뮤니티 데이터에 대해 주제 전문가가 이미 작성한 200개 이상의 플러그인을 사용하면 끝점에서 메트릭 수집을 쉽게 시작할 수 있습니다. 더욱이 플러그인 개발이 간편하기 때문에 모니터링 요구 사항에 맞게 플러그인을 빌드할 수 있습니다. Telegraf를 사용하여 입력 데이터 형식을 메트릭으로 구문 분석할 수도 있습니다. 여기에는 InfluxDB 라인 프로토콜, JSON, Graphite, Value, Nagios 및 Collectd가 포함됩니다.
Flexible : Telegraf 플러그인 아키텍처는 프로세스를 지원하며 해당 기술을 사용하기 위해 워크플로를 변경하도록 강요하지 않습니다. 엣지에 앉거나 중앙 집중식 방식으로 필요하든지 상관없이 아키텍처에 딱 맞습니다. Telegraf의 유연성 덕분에 구현하기가 쉽습니다.
출처 : 텔레그라프, https://www.influxdata.com/time-series-platform/telegraf/
하위페이지
•	[Telegraf] 설치/실행 안내
•	[Telegraf] inputs plugin
•	[Telegraf] output plugin 설정 - InfluxDB2
•	[Telegraf] Trubleshooting
[Telegraf] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
설치경로 : https://portal.influxdata.com/downloads/
또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)
wget https://dl.influxdata.com/telegraf/releases/telegraf-1.19.1-1.x86_64.rpm
프로그램 설치 및 최초 실행
설치
[root@openwast01 downloads]# yum localinstall telegraf-1.19.1-1.x86_64.rpm 
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
[root@openwast01 downloads]# 
Code Block 23 telegraf install

실행
[root@openwast01 downloads]# systemctl start telegraf.service
[root@openwast01 downloads]# systemctl status telegraf.service
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; vendor preset: disabled)
   Active: active (running) since 금 2021-07-30 08:53:12 KST; 4s ago
     Docs: https://github.com/influxdata/telegraf
 Main PID: 10257 (telegraf)
   CGroup: /system.slice/telegraf.service
           └─10257 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d
 
 7월 30 08:53:12 openwast01 telegraf[10257]: time="2021-07-30T08:53:12+09:00" level=error msg="failed to create cache directory. /etc/telegraf/....go:120"
 7월 30 08:53:12 openwast01 telegraf[10257]: time="2021-07-30T08:53:12+09:00" level=error msg="failed to open. Ignored. open /etc/telegraf/.cac....go:120"
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Starting Telegraf 1.19.1
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded inputs: cpu disk diskio kernel mem processes swap system
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded aggregators:
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded processors:
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded outputs: influxdb
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Tags enabled: host=openwast01
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"openwast01", Flush Interval:10s
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z W! [outputs.influxdb] When writing to [http://localhost:8086]: database "tele...thorized
Hint: Some lines were ellipsized, use -l to show in full.
[root@openwast01 downloads]# 
Code Block 24 telegraf start

프로그램 종료

[root@openwast01 downloads]# systemctl stop telegraf.service
[root@openwast01 downloads]# systemctl status telegraf.service
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; vendor preset: disabled)
   Active: inactive (dead) since 금 2021-07-30 08:53:43 KST; 3s ago
     Docs: https://github.com/influxdata/telegraf
  Process: 10257 ExecStart=/usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d $TELEGRAF_OPTS (code=exited, status=0/SUCCESS)
 Main PID: 10257 (code=exited, status=0/SUCCESS)
 
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded processors:
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Loaded outputs: influxdb
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! Tags enabled: host=openwast01
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"openwast01", Flush Interval:10s
 7월 30 08:53:12 openwast01 telegraf[10257]: 2021-07-29T23:53:12Z W! [outputs.influxdb] When writing to [http://localhost:8086]: database "tele...thorized
 7월 30 08:53:22 openwast01 telegraf[10257]: 2021-07-29T23:53:22Z E! [outputs.influxdb] E! [outputs.influxdb] Failed to write metric (will be d...orized):
 7월 30 08:53:32 openwast01 telegraf[10257]: 2021-07-29T23:53:32Z E! [outputs.influxdb] E! [outputs.influxdb] Failed to write metric (will be d...orized):
 7월 30 08:53:42 openwast01 telegraf[10257]: 2021-07-29T23:53:42Z E! [outputs.influxdb] E! [outputs.influxdb] Failed to write metric (will be d...orized):
 7월 30 08:53:43 openwast01 systemd[1]: Stopping The plugin-driven server agent for reporting metrics into InfluxDB...
 7월 30 08:53:43 openwast01 systemd[1]: Stopped The plugin-driven server agent for reporting metrics into InfluxDB.
Hint: Some lines were ellipsized, use -l to show in full.
[root@openwast01 downloads]# 
Code Block 25 telegraf stop

삭제(yum remove)

telegraf 종료 후 수행해야 합니다.

[root@openwast01 ~]# yum remove telegraf
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
[root@openwast01 ~]# 
Code Block 26 telegraf remove

[Telegraf] inputs plugin
개요
telegraf 의 데이터 수집을 위한 telegraf.conf 설정 방법 모음
상세한 가이드는 telegraf guide 참고 (https://docs.influxdata.com/telegraf/v1.19/plugins/)
cpu 설정

# Read metrics about cpu usage
[[inputs.cpu]]
  ## Whether to report per-cpu stats or not
  percpu = true
  ## Whether to report total system cpu stats or not
  totalcpu = true
  ## If true, collect raw CPU time metrics
  collect_cpu_time = false
  ## If true, compute and report the sum of all non-idle CPU states
  report_active = false
Code Block 27 inputs.cpu

disk 설정

# Read metrics about disk usage by mount point
[[inputs.disk]]
  ## By default stats will be gathered for all mount points.
  ## Set mount_points will restrict the stats to only the specified mount points.
  # mount_points = ["/"]
 
  ## Ignore mount points by filesystem type.
  ignore_fs = ["tmpfs", "devtmpfs", "devfs", "iso9660", "overlay", "aufs", "squashfs"]
 
 
# Read metrics about disk IO by device
[[inputs.diskio]]
  ## By default, telegraf will gather stats for all devices including
  ## disk partitions.
  ## Setting devices will restrict the stats to the specified devices.
  # devices = ["sda", "sdb", "vd*"]
  ## Uncomment the following line if you need disk serial numbers.
  # skip_serial_number = false
  #
  ## On systems which support it, device metadata can be added in the form of
  ## tags.
  ## Currently only Linux is supported via udev properties. You can view
  ## available properties for a device by running:
  ## 'udevadm info -q property -n /dev/sda'
  ## Note: Most, but not all, udev properties can be accessed this way. Properties
  ## that are currently inaccessible include DEVTYPE, DEVNAME, and DEVPATH.
  # device_tags = ["ID_FS_TYPE", "ID_FS_USAGE"]
  #
  ## Using the same metadata source as device_tags, you can also customize the
  ## name of the device via templates.
  ## The 'name_templates' parameter is a list of templates to try and apply to
  ## the device. The template may contain variables in the form of '$PROPERTY' or
  ## '${PROPERTY}'. The first template which does not contain any variables not
  ## present for the device is used as the device name tag.
  ## The typical use case is for LVM volumes, to get the VG/LV name instead of
  ## the near-meaningless DM-0 name.
  # name_templates = ["$ID_FS_LABEL","$DM_VG_NAME/$DM_LV_NAME"]
Code Block 28 inputs.disk / inputs.diskio

network 설정
ifconfig 로 NIC 확인
[root@openwast01 downloads]# ifconfig
ens192: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.30.23.221  netmask 255.255.255.0  broadcast 172.30.23.255
        ether 00:50:56:aa:2f:84  txqueuelen 1000  (Ethernet)
        RX packets 40720042  bytes 7639545713 (7.1 GiB)
        RX errors 0  dropped 159  overruns 0  frame 0
        TX packets 18006069  bytes 4408696784 (4.1 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
 
lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 49888373  bytes 13167477657 (12.2 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 49888373  bytes 13167477657 (12.2 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
 
[root@openwast01 downloads]#
Code Block 29 ifconfig

ifconfig 로 확인된 NIC 정보로 telegraf.conf 설정
# # Read metrics about network interface usage
[[inputs.net]]
#   ## By default, telegraf gathers stats from any up interface (excluding loopback)
#   ## Setting interfaces will tell it to gather these explicit interfaces,
#   ## regardless of status.
#   ##
#   # interfaces = ["eth0"]
interfaces = ["ens192"]
#   ##
#   ## On linux systems telegraf also collects protocol stats.
#   ## Setting ignore_protocol_stats to true will skip reporting of protocol metrics.
#   ##
#   # ignore_protocol_stats = false
#   ##
Code Block 30 inputs.net

[Telegraf] output plugin 설정 - InfluxDB2
최초 설치 시 telegraf 는 InfluxDB version 1 으로 설정되어 있습니다. 아래 환경설정을 통해 InfluxDB version 2 로 변경 진행해야 합니다.

환경설정
InfluxDB2 bucket 확인
[InfluxDB2] Buckets 의 Bucket 생성 참고
InfluxDB2 token 확인
[InfluxDB2] Tokens 의 Token 조회 참고
환경설정
환경변수 파일 위치 : etc/telegraf/telegraf.conf
influxdb output inactive
[[outputs.influxdb]] 를 주석 처리
# Configuration for sending metrics to InfluxDB
# [[outputs.influxdb]]
  ## The full HTTP or UDP URL for your InfluxDB instance.
  ##
  ## Multiple URLs can be specified for a single cluster, only ONE of the
  ## urls will be written to each interval.
  # urls = ["unix:///var/run/influxdb.sock"]
  # urls = ["udp://127.0.0.1:8089"]
  # urls = ["http://127.0.0.1:8086"]
Code Block 31 telegraf.conf / inactive influxdb

influxdb_v2 output active
아래 환경 변수 입력(예시)
아래 예시는 InfluxDB 의 Telegraf configuration 을 설정 했을 경우 해당 설정 정보를 클릭하여 정보 확인 가능
 
Token 의 경우 InfluxDB 의 Telegraf 에서 생성한 Token 의 값을 사용
 
[[outputs.influxdb_v2]] 
  ## The URLs of the InfluxDB cluster nodes.
  ##
  ## Multiple URLs can be specified for a single cluster, only ONE of the
  ## urls will be written to each interval.
  ## urls exp: http://127.0.0.1:8086
  urls = ["http://172.30.23.221:8086"]
 
  ## Token for authentication.
  token = "$INFLUX_TOKEN"
 
  ## Organization is the name of the organization you wish to write to; must exist.
  organization = "nicepayments"
 
  ## Destination bucket to write into.
  bucket = "resource-data"
Code Block 32 telegraf.conf / influxdb_v2 active

재기동

[root@openwast01 telegraf]# systemctl stop telegraf.service
[root@openwast01 telegraf]# systemctl start telegraf.service
[root@openwast01 telegraf]# systemctl status telegraf.service
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; vendor preset: disabled)
   Active: active (running) since 금 2021-07-30 15:26:31 KST; 3s ago
     Docs: https://github.com/influxdata/telegraf
 Main PID: 30938 (telegraf)
   CGroup: /system.slice/telegraf.service
           └─30938 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d
 
 7월 30 15:26:31 openwast01 systemd[1]: Started The plugin-driven server agent for reporting metrics into InfluxDB.
 7월 30 15:26:31 openwast01 telegraf[30938]: time="2021-07-30T15:26:31+09:00" level=error msg="failed to create cache directory. /etc/telegraf....go:120"
 7월 30 15:26:31 openwast01 telegraf[30938]: time="2021-07-30T15:26:31+09:00" level=error msg="failed to open. Ignored. open /etc/telegraf/.ca....go:120"
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! Starting Telegraf 1.19.1
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! Loaded inputs: cpu disk diskio kernel mem net processes swap system
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! Loaded aggregators:
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! Loaded processors:
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! Loaded outputs: influxdb_v2
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! Tags enabled: host=openwast01
 7월 30 15:26:31 openwast01 telegraf[30938]: 2021-07-30T06:26:31Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"openwast01", Flush Interval:10s
Hint: Some lines were ellipsized, use -l to show in full.
[root@openwast01 telegraf]#
Code Block 33 telegraf restart

failed to create cache directory

version	1.19.1-1
영향도	 낮음 
원인	gosnowflake 의 권한 이슈로 발생
내용	[root@openwast01 telegraf]# systemctl status telegraf.service
● telegraf.service - The plugin-driven server agent for reporting metrics into InfluxDB
   Loaded: loaded (/usr/lib/systemd/system/telegraf.service; enabled; vendor preset: disabled)
   Active: active (running) since 금 2021-07-30 15:10:26 KST; 1s ago
     Docs: https://github.com/influxdata/telegraf
 Main PID: 30083 (telegraf)
   CGroup: /system.slice/telegraf.service
           └─30083 /usr/bin/telegraf -config /etc/telegraf/telegraf.conf -config-directory /etc/telegraf/telegraf.d
 
 7월 30 15:10:26 openwast01 systemd[1]: Started The plugin-driven server agent for reporting metrics into InfluxDB.
 7월 30 15:10:26 openwast01 telegraf[30083]: time="2021-07-30T15:10:26+09:00" level=error msg="failed to create cache directory. /etc/telegraf/....go:120"
 7월 30 15:10:26 openwast01 telegraf[30083]: time="2021-07-30T15:10:26+09:00" level=error msg="failed to open. Ignored. open /etc/telegraf/.cac....go:120"
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! Starting Telegraf 1.19.1
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! Loaded inputs: cpu disk diskio kernel mem processes swap system
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! Loaded aggregators:
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! Loaded processors:
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! Loaded outputs: influxdb_v2
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! Tags enabled: host=openwast01
 7월 30 15:10:26 openwast01 telegraf[30083]: 2021-07-30T06:10:26Z I! [agent] Config: Interval:10s, Quiet:false, Hostname:"openwast01", Flush Interval:10s
Hint: Some lines were ellipsized, use -l to show in full.
[root@openwast01 telegraf]# timed out waiting for input: auto-logout

level=error msg="failed to create cache directory. /etc/telegraf/....go:120" 발생
참고	https://github.com/influxdata/telegraf/issues/9407

Dashboard : Grafana
개요
그라파나는 오픈소스 메트릭 데이터 시각화 도구로 메트릭 분석 플랫폼을 지향하고 있습니다. Torkel Ödegaard의 주도로 2014년 처음 릴리스되었으며, 처음에는 그라파이트Graphite, 인플럭스DBInfluxDB, 오픈TSDBOpenTSDB 등을 지원하는 오픈소스 대시보드 도구로 개발되었습니다. 메트릭 정보를 시각화하고 대시보드를 구성한다는 큰 틀은 여전히 변함이 없습니다만, AWS 클라우드와치AWS CloudWatch, 애저 모니터Azure Monitor와 같은 클라우드 데이터 소스를 비롯해 로키Loki나 엘라스틱서치ElasticSearch 등을 기반으로 로그 데이터를 지원하는 등 더 많은 데이터 소스를 지원하고 있습니다. 또한 엔터프라이즈 플랜에서는 스플렁크Splunk, 뉴 렐릭New Relic, 앱다이나믹AppDynamics, 오라클Oracle, 다이나트레이스Dynatrace, 서비스나우ServiceNow, 데이터독DataDog 등의 외부 서비스들과 통합도 지원하고 있습니다.
그라파나는 현재 그라파나 랩Grafana Labs에서 개발하고 있습니다. 그라파나 랩은 그라파나Grafana와 로키Loki, 탄카Tanka 등의 애플리케이션을 오픈소스를 개발하고 있는 회사로, 2019년 10월 시리즈 A $24M, 2020년 8월 시리즈B $50M의 투자를 유치했습니다. 2020년 현재 그라파나 랩은 32개 국가에서 리모트를 기반으로 운영되는 170명 규모의 회사로 성장했으며 그라파나 엔터프라이즈Grafana Enterprise와 그라파나 클라우드Grafana Cloud와 같은 상용 서비스도 개발하고 있습니다.
그라파나는 페이팔Paypal, 이베이ebay, 인텔Intel, 랙스페이스rackspace, 비메오Video, 테드TED, 디지털 오션Digital Ocean, 블룸버그Bloomberg 등 다양한 기업에서 활용되고 있습니다. 더 자세하고 다양한 도입 사례에 대해서는 그라파나 웹 사이트에서 확인할 수 있습니다.

출처 : 44BITS, 그라파나란? https://www.44bits.io/ko/keyword/grafana 
하위페이지
•	[Grafana] 설치/실행 안내
•	[Grafana] GUI 사용법
•	[Grafana] Data source 연동 - InfluxDB2
[Grafana] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
설치경로 : https://grafana.com/grafana/download
또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)
wget https://dl.grafana.com/oss/release/grafana-8.0.6-1.x86_64.rpm

프로그램 설치 및 최초 실행
설치
[root@openwebt01 downloads]# yum install grafana-8.0.6-1.x86_64.rpm 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
 
This system is not registered with an entitlement server. You can use subscription-manager to register.
 
Examining grafana-8.0.6-1.x86_64.rpm: grafana-8.0.6-1.x86_64
Marking grafana-8.0.6-1.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package grafana.x86_64 0:8.0.6-1 will be installed
--> Processing Dependency: fontconfig for package: grafana-8.0.6-1.x86_64
Local_Repo                                                                                                                                                                                                                                                                                          | 2.8 kB  00:00:00     
zabbix                                                                                                                                                                                                                                                                                              | 2.9 kB  00:00:00     
zabbix-non-supported                                                                                                                                                                                                                                                                                | 2.9 kB  00:00:00     
--> Processing Dependency: urw-fonts for package: grafana-8.0.6-1.x86_64
--> Running transaction check
---> Package fontconfig.x86_64 0:2.13.0-4.3.el7 will be installed
--> Processing Dependency: fontpackages-filesystem for package: fontconfig-2.13.0-4.3.el7.x86_64
--> Processing Dependency: dejavu-sans-fonts for package: fontconfig-2.13.0-4.3.el7.x86_64
---> Package urw-base35-fonts.noarch 0:20170801-10.el7 will be installed
--> Processing Dependency: urw-base35-fonts-common = 20170801-10.el7 for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-z003-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-standard-symbols-ps-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-p052-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-nimbus-sans-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-nimbus-roman-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-nimbus-mono-ps-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-gothic-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-d050000l-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-c059-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Processing Dependency: urw-base35-bookman-fonts for package: urw-base35-fonts-20170801-10.el7.noarch
--> Running transaction check
---> Package dejavu-sans-fonts.noarch 0:2.33-6.el7 will be installed
--> Processing Dependency: dejavu-fonts-common = 2.33-6.el7 for package: dejavu-sans-fonts-2.33-6.el7.noarch
---> Package fontpackages-filesystem.noarch 0:1.44-8.el7 will be installed
---> Package urw-base35-bookman-fonts.noarch 0:20170801-10.el7 will be installed
--> Processing Dependency: xorg-x11-server-utils for package: urw-base35-bookman-fonts-20170801-10.el7.noarch
--> Processing Dependency: xorg-x11-server-utils for package: urw-base35-bookman-fonts-20170801-10.el7.noarch
--> Processing Dependency: xorg-x11-font-utils for package: urw-base35-bookman-fonts-20170801-10.el7.noarch
--> Processing Dependency: xorg-x11-font-utils for package: urw-base35-bookman-fonts-20170801-10.el7.noarch
---> Package urw-base35-c059-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-d050000l-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-fonts-common.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-gothic-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-nimbus-mono-ps-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-nimbus-roman-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-nimbus-sans-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-p052-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-standard-symbols-ps-fonts.noarch 0:20170801-10.el7 will be installed
---> Package urw-base35-z003-fonts.noarch 0:20170801-10.el7 will be installed
--> Running transaction check
---> Package dejavu-fonts-common.noarch 0:2.33-6.el7 will be installed
---> Package xorg-x11-font-utils.x86_64 1:7.5-21.el7 will be installed
--> Processing Dependency: libfontenc.so.1()(64bit) for package: 1:xorg-x11-font-utils-7.5-21.el7.x86_64
---> Package xorg-x11-server-utils.x86_64 0:7.7-20.el7 will be installed
--> Processing Dependency: libXxf86vm.so.1()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXxf86misc.so.1()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXt.so.6()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXrender.so.1()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXrandr.so.2()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXmuu.so.1()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXmu.so.6()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXinerama.so.1()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXi.so.6()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXext.so.6()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libXcursor.so.1()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libX11.so.6()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Processing Dependency: libICE.so.6()(64bit) for package: xorg-x11-server-utils-7.7-20.el7.x86_64
--> Running transaction check
---> Package libICE.x86_64 0:1.0.9-9.el7 will be installed
---> Package libX11.x86_64 0:1.6.7-2.el7 will be installed
--> Processing Dependency: libX11-common >= 1.6.7-2.el7 for package: libX11-1.6.7-2.el7.x86_64
--> Processing Dependency: libxcb.so.1()(64bit) for package: libX11-1.6.7-2.el7.x86_64
---> Package libXcursor.x86_64 0:1.1.15-1.el7 will be installed
--> Processing Dependency: libXfixes.so.3()(64bit) for package: libXcursor-1.1.15-1.el7.x86_64
---> Package libXext.x86_64 0:1.3.3-3.el7 will be installed
---> Package libXi.x86_64 0:1.7.9-1.el7 will be installed
---> Package libXinerama.x86_64 0:1.1.3-2.1.el7 will be installed
---> Package libXmu.x86_64 0:1.1.2-2.el7 will be installed
---> Package libXrandr.x86_64 0:1.5.1-2.el7 will be installed
---> Package libXrender.x86_64 0:0.9.10-1.el7 will be installed
---> Package libXt.x86_64 0:1.1.5-3.el7 will be installed
--> Processing Dependency: libSM.so.6()(64bit) for package: libXt-1.1.5-3.el7.x86_64
---> Package libXxf86misc.x86_64 0:1.0.3-7.1.el7 will be installed
---> Package libXxf86vm.x86_64 0:1.1.4-1.el7 will be installed
---> Package libfontenc.x86_64 0:1.1.3-3.el7 will be installed
--> Running transaction check
---> Package libSM.x86_64 0:1.2.2-2.el7 will be installed
---> Package libX11-common.noarch 0:1.6.7-2.el7 will be installed
---> Package libXfixes.x86_64 0:5.0.3-1.el7 will be installed
---> Package libxcb.x86_64 0:1.13-1.el7 will be installed
--> Processing Dependency: libXau.so.6()(64bit) for package: libxcb-1.13-1.el7.x86_64
--> Running transaction check
---> Package libXau.x86_64 0:1.0.8-2.1.el7 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================================================================================================================================================================================
 Package                                                                                      Arch                                                           Version                                                                 Repository                                                                       Size
===========================================================================================================================================================================================================================================================================================================================
Installing:
 grafana                                                                                      x86_64                                                         8.0.6-1                                                                 /grafana-8.0.6-1.x86_64                                                         174 M
Installing for dependencies:
 dejavu-fonts-common                                                                          noarch                                                         2.33-6.el7                                                              Local_Repo                                                                       64 k
 dejavu-sans-fonts                                                                            noarch                                                         2.33-6.el7                                                              Local_Repo                                                                      1.4 M
 fontconfig                                                                                   x86_64                                                         2.13.0-4.3.el7                                                          Local_Repo                                                                      254 k
 fontpackages-filesystem                                                                      noarch                                                         1.44-8.el7                                                              Local_Repo                                                                      9.9 k
 libICE                                                                                       x86_64                                                         1.0.9-9.el7                                                             Local_Repo                                                                       66 k
 libSM                                                                                        x86_64                                                         1.2.2-2.el7                                                             Local_Repo                                                                       39 k
 libX11                                                                                       x86_64                                                         1.6.7-2.el7                                                             Local_Repo                                                                      607 k
 libX11-common                                                                                noarch                                                         1.6.7-2.el7                                                             Local_Repo                                                                      164 k
 libXau                                                                                       x86_64                                                         1.0.8-2.1.el7                                                           Local_Repo                                                                       29 k
 libXcursor                                                                                   x86_64                                                         1.1.15-1.el7                                                            Local_Repo                                                                       30 k
 libXext                                                                                      x86_64                                                         1.3.3-3.el7                                                             Local_Repo                                                                       39 k
 libXfixes                                                                                    x86_64                                                         5.0.3-1.el7                                                             Local_Repo                                                                       18 k
 libXi                                                                                        x86_64                                                         1.7.9-1.el7                                                             Local_Repo                                                                       40 k
 libXinerama                                                                                  x86_64                                                         1.1.3-2.1.el7                                                           Local_Repo                                                                       14 k
 libXmu                                                                                       x86_64                                                         1.1.2-2.el7                                                             Local_Repo                                                                       71 k
 libXrandr                                                                                    x86_64                                                         1.5.1-2.el7                                                             Local_Repo                                                                       27 k
 libXrender                                                                                   x86_64                                                         0.9.10-1.el7                                                            Local_Repo                                                                       26 k
 libXt                                                                                        x86_64                                                         1.1.5-3.el7                                                             Local_Repo                                                                      173 k
 libXxf86misc                                                                                 x86_64                                                         1.0.3-7.1.el7                                                           Local_Repo                                                                       19 k
 libXxf86vm                                                                                   x86_64                                                         1.1.4-1.el7                                                             Local_Repo                                                                       18 k
 libfontenc                                                                                   x86_64                                                         1.1.3-3.el7                                                             Local_Repo                                                                       31 k
 libxcb                                                                                       x86_64                                                         1.13-1.el7                                                              Local_Repo                                                                      214 k
 urw-base35-bookman-fonts                                                                     noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      852 k
 urw-base35-c059-fonts                                                                        noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      879 k
 urw-base35-d050000l-fonts                                                                    noarch                                                         20170801-10.el7                                                         Local_Repo                                                                       75 k
 urw-base35-fonts                                                                             noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      7.6 k
 urw-base35-fonts-common                                                                      noarch                                                         20170801-10.el7                                                         Local_Repo                                                                       19 k
 urw-base35-gothic-fonts                                                                      noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      650 k
 urw-base35-nimbus-mono-ps-fonts                                                              noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      796 k
 urw-base35-nimbus-roman-fonts                                                                noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      860 k
 urw-base35-nimbus-sans-fonts                                                                 noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      1.3 M
 urw-base35-p052-fonts                                                                        noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      978 k
 urw-base35-standard-symbols-ps-fonts                                                         noarch                                                         20170801-10.el7                                                         Local_Repo                                                                       40 k
 urw-base35-z003-fonts                                                                        noarch                                                         20170801-10.el7                                                         Local_Repo                                                                      275 k
 xorg-x11-font-utils                                                                          x86_64                                                         1:7.5-21.el7                                                            Local_Repo                                                                      104 k
 xorg-x11-server-utils                                                                        x86_64                                                         7.7-20.el7                                                              Local_Repo                                                                      178 k
 
Transaction Summary
===========================================================================================================================================================================================================================================================================================================================
Install  1 Package (+36 Dependent packages)
 
Total size: 184 M
Total download size: 10 M
Installed size: 196 M
Is this ok [y/d/N]: y
Downloading packages:
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                                                                                                                                      111 MB/s |  10 MB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : fontpackages-filesystem-1.44-8.el7.noarch                                                                                                                                                                                                                                                              1/37 
  Installing : urw-base35-fonts-common-20170801-10.el7.noarch                                                                                                                                                                                                                                                         2/37 
  Installing : libICE-1.0.9-9.el7.x86_64                                                                                                                                                                                                                                                                              3/37 
  Installing : libSM-1.2.2-2.el7.x86_64                                                                                                                                                                                                                                                                               4/37 
  Installing : dejavu-fonts-common-2.33-6.el7.noarch                                                                                                                                                                                                                                                                  5/37 
  Installing : dejavu-sans-fonts-2.33-6.el7.noarch                                                                                                                                                                                                                                                                    6/37 
  Installing : fontconfig-2.13.0-4.3.el7.x86_64                                                                                                                                                                                                                                                                       7/37 
  Installing : libfontenc-1.1.3-3.el7.x86_64                                                                                                                                                                                                                                                                          8/37 
  Installing : 1:xorg-x11-font-utils-7.5-21.el7.x86_64                                                                                                                                                                                                                                                                9/37 
  Installing : libXau-1.0.8-2.1.el7.x86_64                                                                                                                                                                                                                                                                           10/37 
  Installing : libxcb-1.13-1.el7.x86_64                                                                                                                                                                                                                                                                              11/37 
  Installing : libX11-common-1.6.7-2.el7.noarch                                                                                                                                                                                                                                                                      12/37 
  Installing : libX11-1.6.7-2.el7.x86_64                                                                                                                                                                                                                                                                             13/37 
  Installing : libXext-1.3.3-3.el7.x86_64                                                                                                                                                                                                                                                                            14/37 
  Installing : libXrender-0.9.10-1.el7.x86_64                                                                                                                                                                                                                                                                        15/37 
  Installing : libXt-1.1.5-3.el7.x86_64                                                                                                                                                                                                                                                                              16/37 
  Installing : libXmu-1.1.2-2.el7.x86_64                                                                                                                                                                                                                                                                             17/37 
  Installing : libXrandr-1.5.1-2.el7.x86_64                                                                                                                                                                                                                                                                          18/37 
  Installing : libXinerama-1.1.3-2.1.el7.x86_64                                                                                                                                                                                                                                                                      19/37 
  Installing : libXxf86misc-1.0.3-7.1.el7.x86_64                                                                                                                                                                                                                                                                     20/37 
  Installing : libXxf86vm-1.1.4-1.el7.x86_64                                                                                                                                                                                                                                                                         21/37 
  Installing : libXi-1.7.9-1.el7.x86_64                                                                                                                                                                                                                                                                              22/37 
  Installing : libXfixes-5.0.3-1.el7.x86_64                                                                                                                                                                                                                                                                          23/37 
  Installing : libXcursor-1.1.15-1.el7.x86_64                                                                                                                                                                                                                                                                        24/37 
  Installing : xorg-x11-server-utils-7.7-20.el7.x86_64                                                                                                                                                                                                                                                               25/37 
  Installing : urw-base35-z003-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                          26/37 
  Installing : urw-base35-p052-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                          27/37 
  Installing : urw-base35-nimbus-roman-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                  28/37 
  Installing : urw-base35-c059-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                          29/37 
  Installing : urw-base35-d050000l-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                      30/37 
  Installing : urw-base35-nimbus-mono-ps-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                31/37 
  Installing : urw-base35-bookman-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                       32/37 
  Installing : urw-base35-nimbus-sans-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                   33/37 
  Installing : urw-base35-standard-symbols-ps-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                           34/37 
  Installing : urw-base35-gothic-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                        35/37 
  Installing : urw-base35-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                               36/37 
  Installing : grafana-8.0.6-1.x86_64                                                                                                                                                                                                                                                                                37/37 
### NOT starting on installation, please execute the following statements to configure grafana to start automatically using systemd
 sudo /bin/systemctl daemon-reload
 sudo /bin/systemctl enable grafana-server.service
### You can start grafana-server by executing
 sudo /bin/systemctl start grafana-server.service
POSTTRANS: Running script
  Verifying  : libXext-1.3.3-3.el7.x86_64                                                                                                                                                                                                                                                                             1/37 
  Verifying  : 1:xorg-x11-font-utils-7.5-21.el7.x86_64                                                                                                                                                                                                                                                                2/37 
  Verifying  : fontconfig-2.13.0-4.3.el7.x86_64                                                                                                                                                                                                                                                                       3/37 
  Verifying  : libXinerama-1.1.3-2.1.el7.x86_64                                                                                                                                                                                                                                                                       4/37 
  Verifying  : libXrender-0.9.10-1.el7.x86_64                                                                                                                                                                                                                                                                         5/37 
  Verifying  : urw-base35-z003-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                           6/37 
  Verifying  : libXxf86misc-1.0.3-7.1.el7.x86_64                                                                                                                                                                                                                                                                      7/37 
  Verifying  : libXxf86vm-1.1.4-1.el7.x86_64                                                                                                                                                                                                                                                                          8/37 
  Verifying  : urw-base35-p052-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                           9/37 
  Verifying  : urw-base35-nimbus-roman-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                  10/37 
  Verifying  : libXi-1.7.9-1.el7.x86_64                                                                                                                                                                                                                                                                              11/37 
  Verifying  : libXt-1.1.5-3.el7.x86_64                                                                                                                                                                                                                                                                              12/37 
  Verifying  : libICE-1.0.9-9.el7.x86_64                                                                                                                                                                                                                                                                             13/37 
  Verifying  : fontpackages-filesystem-1.44-8.el7.noarch                                                                                                                                                                                                                                                             14/37 
  Verifying  : urw-base35-c059-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                          15/37 
  Verifying  : urw-base35-d050000l-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                      16/37 
  Verifying  : dejavu-fonts-common-2.33-6.el7.noarch                                                                                                                                                                                                                                                                 17/37 
  Verifying  : libX11-1.6.7-2.el7.x86_64                                                                                                                                                                                                                                                                             18/37 
  Verifying  : libX11-common-1.6.7-2.el7.noarch                                                                                                                                                                                                                                                                      19/37 
  Verifying  : libxcb-1.13-1.el7.x86_64                                                                                                                                                                                                                                                                              20/37 
  Verifying  : urw-base35-fonts-common-20170801-10.el7.noarch                                                                                                                                                                                                                                                        21/37 
  Verifying  : grafana-8.0.6-1.x86_64                                                                                                                                                                                                                                                                                22/37 
  Verifying  : urw-base35-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                               23/37 
  Verifying  : urw-base35-nimbus-mono-ps-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                24/37 
  Verifying  : dejavu-sans-fonts-2.33-6.el7.noarch                                                                                                                                                                                                                                                                   25/37 
  Verifying  : libXmu-1.1.2-2.el7.x86_64                                                                                                                                                                                                                                                                             26/37 
  Verifying  : libXrandr-1.5.1-2.el7.x86_64                                                                                                                                                                                                                                                                          27/37 
  Verifying  : urw-base35-bookman-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                       28/37 
  Verifying  : urw-base35-nimbus-sans-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                   29/37 
  Verifying  : libXau-1.0.8-2.1.el7.x86_64                                                                                                                                                                                                                                                                           30/37 
  Verifying  : libSM-1.2.2-2.el7.x86_64                                                                                                                                                                                                                                                                              31/37 
  Verifying  : libXcursor-1.1.15-1.el7.x86_64                                                                                                                                                                                                                                                                        32/37 
  Verifying  : urw-base35-standard-symbols-ps-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                           33/37 
  Verifying  : xorg-x11-server-utils-7.7-20.el7.x86_64                                                                                                                                                                                                                                                               34/37 
  Verifying  : libXfixes-5.0.3-1.el7.x86_64                                                                                                                                                                                                                                                                          35/37 
  Verifying  : libfontenc-1.1.3-3.el7.x86_64                                                                                                                                                                                                                                                                         36/37 
  Verifying  : urw-base35-gothic-fonts-20170801-10.el7.noarch                                                                                                                                                                                                                                                        37/37 
 
Installed:
  grafana.x86_64 0:8.0.6-1                                                                                                                                                                                                                                                                                                 
 
Dependency Installed:
  dejavu-fonts-common.noarch 0:2.33-6.el7                      dejavu-sans-fonts.noarch 0:2.33-6.el7                   fontconfig.x86_64 0:2.13.0-4.3.el7                                   fontpackages-filesystem.noarch 0:1.44-8.el7                     libICE.x86_64 0:1.0.9-9.el7                                  
  libSM.x86_64 0:1.2.2-2.el7                                   libX11.x86_64 0:1.6.7-2.el7                             libX11-common.noarch 0:1.6.7-2.el7                                   libXau.x86_64 0:1.0.8-2.1.el7                                   libXcursor.x86_64 0:1.1.15-1.el7                             
  libXext.x86_64 0:1.3.3-3.el7                                 libXfixes.x86_64 0:5.0.3-1.el7                          libXi.x86_64 0:1.7.9-1.el7                                           libXinerama.x86_64 0:1.1.3-2.1.el7                              libXmu.x86_64 0:1.1.2-2.el7                                  
  libXrandr.x86_64 0:1.5.1-2.el7                               libXrender.x86_64 0:0.9.10-1.el7                        libXt.x86_64 0:1.1.5-3.el7                                           libXxf86misc.x86_64 0:1.0.3-7.1.el7                             libXxf86vm.x86_64 0:1.1.4-1.el7                              
  libfontenc.x86_64 0:1.1.3-3.el7                              libxcb.x86_64 0:1.13-1.el7                              urw-base35-bookman-fonts.noarch 0:20170801-10.el7                    urw-base35-c059-fonts.noarch 0:20170801-10.el7                  urw-base35-d050000l-fonts.noarch 0:20170801-10.el7           
  urw-base35-fonts.noarch 0:20170801-10.el7                    urw-base35-fonts-common.noarch 0:20170801-10.el7        urw-base35-gothic-fonts.noarch 0:20170801-10.el7                     urw-base35-nimbus-mono-ps-fonts.noarch 0:20170801-10.el7        urw-base35-nimbus-roman-fonts.noarch 0:20170801-10.el7       
  urw-base35-nimbus-sans-fonts.noarch 0:20170801-10.el7        urw-base35-p052-fonts.noarch 0:20170801-10.el7          urw-base35-standard-symbols-ps-fonts.noarch 0:20170801-10.el7        urw-base35-z003-fonts.noarch 0:20170801-10.el7                  xorg-x11-font-utils.x86_64 1:7.5-21.el7                      
  xorg-x11-server-utils.x86_64 0:7.7-20.el7                   
 
Complete!
[root@openwebt01 downloads]# 
Code Block 34 grafana install

실행
[root@openwebt01 downloads]# systemctl start grafana-server
[root@openwebt01 downloads]# systemctl status grafana-server
● grafana-server.service - Grafana instance
   Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; disabled; vendor preset: disabled)
   Active: active (running) since 월 2021-08-02 09:58:42 KST; 4s ago
     Docs: http://docs.grafana.org
 Main PID: 10783 (grafana-server)
   CGroup: /system.slice/grafana-server.service
           └─10783 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/var/run/grafana/grafana-server.pid --packaging=rpm cfg:default.paths.logs=/var/log/grafana cfg:default.paths.data=/var/lib/grafana cfg:default.paths.plugins=/var/lib/grafana/plugins cfg:default.paths.provisioning=/etc/grafa...
 
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="migrations completed" logger=migrator performed=330 skipped=0 duration=507.041783ms
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="Created default admin" logger=sqlstore user=admin
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="Created default organization" logger=sqlstore
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="Starting plugin search" logger=plugins
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="Registering plugin" logger=plugins id=input
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="Registering plugin" logger=plugins id=grafana-plugin-admin-app
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="External plugins directory created" logger=plugins directory=/var/lib/grafana/plugins
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="Live Push Gateway initialization" logger=live.push_http
 8월 02 09:58:42 openwebt01 systemd[1]: Started Grafana instance.
 8월 02 09:58:42 openwebt01 grafana-server[10783]: t=2021-08-02T09:58:42+0900 lvl=info msg="HTTP Server Listen" logger=http.server address=0.0.0.0:3000 protocol=http subUrl= socket=
[root@openwebt01 downloads]# 
Code Block 35 grafana start

제목	화면	비고
최초화면	 	http://<SERVER-IP>:3000/login 접속 및 최초정보 입력
최초 계정 : admin
초기 패스워드 : admin
초기 패스워드 설정	 	초기 계정의 패스워드를 변경

프로그램 종료

[root@openwebt01 downloads]# systemctl stop grafana-server
[root@openwebt01 downloads]# systemctl status grafana-server
● grafana-server.service - Grafana instance
   Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: http://docs.grafana.org
 
 8월 02 10:10:15 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:15+0900 lvl=warn msg="Request Origin is not authorized" logger=live origin=http://172.30.161.221:3000 appUrl=http://localhost:3000/ allowedOrigins=
 8월 02 10:10:15 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:15+0900 lvl=info msg="Request Completed" logger=context userId=1 orgId=1 uname=admin method=GET path=/api/live/ws status=403 remote_addr=172.28.117.15 time_ms=0 size=10 referer=
 8월 02 10:10:21 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:21+0900 lvl=warn msg="Request Origin is not authorized" logger=live origin=http://172.30.161.221:3000 appUrl=http://localhost:3000/ allowedOrigins=
 8월 02 10:10:21 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:21+0900 lvl=info msg="Request Completed" logger=context userId=1 orgId=1 uname=admin method=GET path=/api/live/ws status=403 remote_addr=172.28.117.15 time_ms=0 size=10 referer=
 8월 02 10:10:35 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:35+0900 lvl=warn msg="Request Origin is not authorized" logger=live origin=http://172.30.161.221:3000 appUrl=http://localhost:3000/ allowedOrigins=
 8월 02 10:10:35 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:35+0900 lvl=info msg="Request Completed" logger=context userId=1 orgId=1 uname=admin method=GET path=/api/live/ws status=403 remote_addr=172.28.117.15 time_ms=0 size=10 referer=
 8월 02 10:10:50 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:50+0900 lvl=warn msg="Request Origin is not authorized" logger=live origin=http://172.30.161.221:3000 appUrl=http://localhost:3000/ allowedOrigins=
 8월 02 10:10:50 openwebt01 grafana-server[10783]: t=2021-08-02T10:10:50+0900 lvl=info msg="Request Completed" logger=context userId=1 orgId=1 uname=admin method=GET path=/api/live/ws status=403 remote_addr=172.28.117.15 time_ms=0 size=10 referer=
 8월 02 10:15:41 openwebt01 systemd[1]: Stopping Grafana instance...
 8월 02 10:15:41 openwebt01 systemd[1]: Stopped Grafana instance.
[root@openwebt01 downloads]# 
Code Block 36 grafana stop


삭제(yum remove)

grafana server 종료 후 수행해야 합니다.

[root@openwebt01 downloads]# yum list | grep grafana
grafana.x86_64                          8.0.6-1                    @/grafana-8.0.6-1.x86_64
[root@openwebt01 downloads]# yum remove grafana
Loaded plugins: product-id, search-disabled-repos, subscription-manager
 
This system is not registered with an entitlement server. You can use subscription-manager to register.
 
Resolving Dependencies
--> Running transaction check
---> Package grafana.x86_64 0:8.0.6-1 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================================================================================================================================================================================
 Package                                                                  Arch                                                                    Version                                                                  Repository                                                                                 Size
===========================================================================================================================================================================================================================================================================================================================
Removing:
 grafana                                                                  x86_64                                                                  8.0.6-1                                                                  @/grafana-8.0.6-1.x86_64                                                                  174 M
 
Transaction Summary
===========================================================================================================================================================================================================================================================================================================================
Remove  1 Package
 
Installed size: 174 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Erasing    : grafana-8.0.6-1.x86_64                                                                                                                                                                                                                                                                                  1/1 
  Verifying  : grafana-8.0.6-1.x86_64                                                                                                                                                                                                                                                                                  1/1 
 
Removed:
  grafana.x86_64 0:8.0.6-1                                                                                                                                                                                                                                                                                                 
 
Complete!
[root@openwebt01 downloads]# 
Code Block 37 grafana remove

[Grafana] GUI 사용법
로그인
1.	url : http://<SERVER-IP>:3000/login 접속
2.	생성된 Email or username 과 패스워드 입력
 

로그아웃
1.	프로필(http://<SERVER-IP>:3000/profile) 또는 메뉴 왼쪽 하단의 프로필 아이콘 mouse over
2.	Sign Out 선택
 


환경설정
1.	프로필(http://<SERVER-IP>:3000/profile) 또는 메뉴 왼쪽 하단의 프로필 클릭
2.	Preferences 의 Edit profice, Preferences, Organizations 확인 및 수정
패스워드 변경
1.	프로필(http://<SERVER-IP>:3000/profile) 또는 메뉴 왼쪽 하단의 프로필 클릭
2.	Preferences 의 Edit profice, Preferences, Organizations 확인 및 수정
3.	현재 패스워드 및 변경할 패스워드 입력
 

Search
 TBD 
Create New dashboard
 TBD 
Dashboard
 TBD 
Explore
 TBD 
Alerting
 TBD 
Configuration
 TBD 
Server Admin
 TBD 
[Grafana] Data source 연동 - InfluxDB2
개요
OSS TSDB 인 InfluxDB2 를 통한 Data source 연동
사전준비
1.	InfluxDB 가 설치되어 있어야 함
2.	[InfluxDB2] 설치/실행 안내 참고
설정 생성
1.	Configuration - Data source 접근
2.	Time series database 의 InfluxDB 선택
 

3.	Name : 임의의 데이터베이스 명칭
4.	Query Language : Flux 선택
5.	HTTP 옵션에 URL : http://<InfluxDB2-IP>:8086, Access : Server(default) 선택
6.	Auth : 환경에 맞는 설정 진행
7.	InfluxDB Details 정보 입력
a.	Organization : InfluxxDB 의 조직명
b.	Token : 최소 Real 가능한 Token 정보
c.	Default bucket 검색 기본 bucket, 비워도 상관없음

 
8.	등록 후 Explore 메뉴에서 Query 통해서 설정 확인
데이터 처리 어플리케이션
•	ELK Stack
o	[Elasticsearch] 설치/실행 안내
o	[Kibana] 설치/실행 안내
o	[Kibana] 화면 기능
o	[ELK Stack] Trubleshooting
o	[ELK] 기타
	[작업중][Elasticsearch] 추가설정
•	Opensearch
o	[opensearch] 설치/실행 안내
o	[logstash] 환경설정 방법
o	[OpenSearch] 대시보드 사용방법
o	[Opensearch] Trubleshooting
o	_temp [opensearch] 설치/실행 안내
•	Beats
o	[Filebeat] 설치/실행 안내
o	[Filebeat] 환경설정 방법
ELK Stack
 
개요
ELK
E = Elasticsearch
Elasticsearch는 Apache Lucene에 구축되어 배포된 검색 및 분석 엔진입니다. 다양한 언어를 지원하고 고성능에 스키마가 없는 JSON 문서로 Elasticsearch는 다양한 로그 분석과 검색 사용 사례에 최고의 선택이 되었습니다.
2021년 1월 21일, Elastic NV는 소프트웨어 라이선스 전략을 변경하는 바, 퍼미시브 라이선스인 Apache License Version 2.0(ALv2) 라이선스 하에서 Elasticsearch 및 Kibana의 새로운 버전을 더 이상 릴리스하지 않는다고 발표했습니다. 그 대신 새로운 버전의 소프트웨어는 Elastic License 또는 SSPL 아래에서 소스 코드를 사용할 수 있는 Elastic 라이선스 하에서 제공됩니다. 해당 라이선스는 오픈 소스가 아니며 사용자에게 동일한 자유를 제공하지 않습니다. 오픈 소스 커뮤니티와 고객이 계속해서 안전하고 고품질에 완전한 오픈 소스 검색과 분석 제품군을 사용할 수 있도록 AWS는 커뮤니티 주도적이며 오픈 소스 Elasticsearch 및 Kibana의 ALv2 라이선스 갈래인 OpenSearch 프로젝트를 도입했습니다. OpenSearch 제품군은 검색 엔진인 OpenSearch와 시각화 및 사용자 인터페이스인 OpenSearch 대시보드로 구성됩니다.
L = Logstash
Logstash는 다양한 소스로부터 데이터를 수집하고 전환하여 원하는 대상에 전송할 수 있도록 하는 오픈 소스 데이터 수집 도구입니다. 사전 구축된 필터와 200개가 넘은 플러그인에 대한 지원으로 Logstash는 사용자가 데이터 원본이나 유형에 관계없이 데이터를 쉽게 수집할 수 있도록 도와줍니다.
K = Kibana
Kibana는 로그 및 이벤트 검토에 사용하는 데이터 시각화 및 탐색 도구입니다. Kibana는 사용하기 쉽고 대화형 차트와 사전 구축된 집계 및 필터, 지리 공간적 지원을 제공하고 이를 사용해 Elasticsearch에 저장된 데이터를 시각화할 때 원하는 선택을 할 수 있습니다. 
ELK 스택은 로그 분석 공간에서 필요를 채워줍니다. 여러분의 IT 인프라가 점점 더 퍼블릭 클라우드로 이동할수록, 해당 인프라와 서버 로그, 애플리케이션 로그, 클릭스트림 프로세스를 모니터링하기 위해 로그 관리와 분석 솔루션이 필요합니다. ELK 스택은 개발자와 DevOps 엔지니어가 오류 진단, 애플리케이션 성능, 인프라 모니터링으로부터 값진 인사이트를 얻을 수 있도록 적은 비용으로 단순하면서도 강력한 로그 분석 솔루션을 제공합니다.
ELK Stack
기존의 ELK 에 Beats 를 포함하여 ELK Stack 로 호칭합니다.
기본 설정 정보(default 설정)

서비스	환경설정 파일	서비스 로그파일	비고
ElasticSearch	/etc/elasticsearch/elasticsearch.yml	/var/log/elasticsearch/elasticsearch.log	
Logstash	/etc/logstash/logstash.yml	/var/log/logstash/logstash.log	
Kibana	/etc/kibana/kibana.yml	/var/log/kibana/kibana.log	
Filebeat	/etc/filebeat/filebeat.yml	/var/log/filebeat/filebeat.log	filebeat 는 기본적으로 log 생성하지 않음
다운로드

서비스	안내 페이지	서비스 버전	다운로드 path
ElasticSearch	https://www.elastic.co/downloads/elasticsearch
	7.14.1	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.15.0-x86_64.rpm

Logstash	https://www.elastic.co/kr/downloads/logstash
7.14.1	https://artifacts.elastic.co/downloads/logstash/logstash-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/logstash/logstash-7.15.0-x86_64.rpm

Kibana	https://www.elastic.co/downloads/kibana
7.14.1	https://artifacts.elastic.co/downloads/kibana/kibana-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/kibana/kibana-7.15.0-x86_64.rpm

Filebeat	https://www.elastic.co/kr/downloads/beats/filebeat
7.14.1(64 bit)	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.14.1-x86_64.rpm

		7.15.0(64 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-x86_64.rpm

		7.15.0(32 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-i686.rpm

하위페이지
•	[Elasticsearch] 설치/실행 안내
•	[Kibana] 설치/실행 안내
•	[Kibana] 화면 기능
•	[ELK Stack] Trubleshooting
•	[ELK] 기타
o	[작업중][Elasticsearch] 추가설정
[Elasticsearch] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.6 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드

서비스	안내 페이지	서비스 버전	다운로드 path
ElasticSearch	https://www.elastic.co/downloads/elasticsearch
	7.14.1	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.15.0-x86_64.rpm

Logstash	https://www.elastic.co/kr/downloads/logstash
7.14.1	https://artifacts.elastic.co/downloads/logstash/logstash-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/logstash/logstash-7.15.0-x86_64.rpm

Kibana	https://www.elastic.co/downloads/kibana
7.14.1	https://artifacts.elastic.co/downloads/kibana/kibana-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/kibana/kibana-7.15.0-x86_64.rpm

Filebeat	https://www.elastic.co/kr/downloads/beats/filebeat
7.14.1(64 bit)	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.14.1-x86_64.rpm

		7.15.0(64 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-x86_64.rpm

		7.15.0(32 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-i686.rpm

프로그램 설치 및 최초 실행
설치
[root@zabbixt01 7.15.0]# yum install elasticsearch-7.15.0-x86_64.rpm
HIWARE: WARNING. Please confirm your command.
Allow command Input?(y/n) 
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Examining elasticsearch-7.15.0-x86_64.rpm: elasticsearch-7.15.0-1.x86_64
Marking elasticsearch-7.15.0-x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package elasticsearch.x86_64 0:7.15.0-1 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
========================================================================================================================================================
 Package                            Arch                        Version                         Repository                                         Size
========================================================================================================================================================
Installing:
 elasticsearch                      x86_64                      7.15.0-1                        /elasticsearch-7.15.0-x86_64                      543 M
 
Transaction Summary
========================================================================================================================================================
Install  1 Package
 
Total size: 543 M
Installed size: 543 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Creating elasticsearch group... OK
Creating elasticsearch user... OK
  Installing : elasticsearch-7.15.0-1.x86_64                                                                                                        1/1 
### NOT starting on installation, please execute the following statements to configure elasticsearch service to start automatically using systemd
 sudo systemctl daemon-reload
 sudo systemctl enable elasticsearch.service
### You can start elasticsearch service by executing
 sudo systemctl start elasticsearch.service
Created elasticsearch keystore in /etc/elasticsearch/elasticsearch.keystore
  Verifying  : elasticsearch-7.15.0-1.x86_64                                                                                                        1/1 
 
Installed:
  elasticsearch.x86_64 0:7.15.0-1                                                                                                                       
 
Complete!
[root@zabbixt01 7.15.0]# 
Code Block 38 elasticsearch install

설정
/etc/elasticsearch/elasticsearch.yml 내 아래 정보 입력
# ======================== Elasticsearch Configuration =========================
#
# NOTE: Elasticsearch comes with reasonable defaults for most settings.
#       Before you set out to tweak and tune the configuration, make sure you
#       understand what are you trying to accomplish and the consequences.
#
# The primary way of configuring a node is via this file. This template lists
# the most important settings you may want to configure for a production cluster.
#
# Please consult the documentation for further information on configuration options:
# https://www.elastic.co/guide/en/elasticsearch/reference/index.html
#
# ---------------------------------- Cluster -----------------------------------
#
# Use a descriptive name for your cluster:
#
#cluster.name: my-application
#
# ------------------------------------ Node ------------------------------------
#
# Use a descriptive name for the node:
#
#node.name: node-1
#
# Add custom attributes to the node:
#
#node.attr.rack: r1
#
# ----------------------------------- Paths ------------------------------------
#
# Path to directory where to store the data (separate multiple locations by comma):
#
path.data: /var/lib/elasticsearch
#
# Path to log files:
#
path.logs: /var/log/elasticsearch
#
# ----------------------------------- Memory -----------------------------------
#
# Lock the memory on startup:
#
#bootstrap.memory_lock: true
#
# Make sure that the heap size is set to about half the memory available
# on the system and that the owner of the process is allowed to use this
# limit.
#
# Elasticsearch performs poorly when the system is swapping the memory.
#
# ---------------------------------- Network -----------------------------------
#
# By default Elasticsearch is only accessible on localhost. Set a different
# address here to expose this node on the network:
#
#network.host: 192.168.0.1
network.host: 0.0.0.0
#
# By default Elasticsearch listens for HTTP traffic on the first free port it
# finds starting at 9200. Set a specific HTTP port here:
#
#http.port: 9200
#
# For more information, consult the network module documentation.
#
# --------------------------------- Discovery ----------------------------------
#
# Pass an initial list of hosts to perform discovery when this node is started:
# The default list of hosts is ["127.0.0.1", "[::1]"]
#
#discovery.seed_hosts: ["host1", "host2"]
#
# Bootstrap the cluster using an initial set of master-eligible nodes:
#
cluster.initial_master_nodes: ["node-1", "node-2"]
#
# For more information, consult the discovery and cluster formation module documentation.
#
# ---------------------------------- Various -----------------------------------
#
# Require explicit names when deleting indices:
#
#action.destructive_requires_name: true
ingest.geoip.downloader.enabled: false
Code Block 39 elasticsearch config

실행
[root@zabbixt01 7.15.0]# systemctl start elasticsearch.service
[root@zabbixt01 7.15.0]# systemctl status elasticsearch.service
● elasticsearch.service - Elasticsearch
   Loaded: loaded (/usr/lib/systemd/system/elasticsearch.service; disabled; vendor preset: disabled)
   Active: active (running) since 목 2021-09-23 15:48:18 KST; 2s ago
     Docs: https://www.elastic.co
 Main PID: 23425 (java)
   CGroup: /system.slice/elasticsearch.service
           ├─23425 /usr/share/elasticsearch/jdk/bin/java -Xshare:auto -Des.networkaddress.cache.ttl=60 -Des.networkaddress.cache.negative.ttl=10 -XX:...
           └─23642 /usr/share/elasticsearch/modules/x-pack-ml/platform/linux-x86_64/bin/controller
 
 9월 23 15:48:00 zabbixt01 systemd[1]: Starting Elasticsearch...
 9월 23 15:48:18 zabbixt01 systemd[1]: Started Elasticsearch.
[root@zabbixt01 7.15.0]#
Code Block 40 elasticsearch start

프로그램 종료

[root@zabbixt01 elasticsearch]# systemctl stop elasticsearch.service
[root@zabbixt01 elasticsearch]# systemctl status elasticsearch.service
● elasticsearch.service - Elasticsearch
   Loaded: loaded (/usr/lib/systemd/system/elasticsearch.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://www.elastic.co
 
 9월 08 13:20:58 zabbixt01 systemd[1]: Unit elasticsearch.service entered failed state.
 9월 08 13:20:58 zabbixt01 systemd[1]: elasticsearch.service failed.
 9월 08 13:22:29 zabbixt01 systemd[1]: Starting Elasticsearch...
 9월 08 13:22:48 zabbixt01 systemd[1]: Started Elasticsearch.
 9월 08 13:23:18 zabbixt01 systemd[1]: Stopping Elasticsearch...
 9월 08 13:23:18 zabbixt01 systemd[1]: Stopped Elasticsearch.
 9월 08 13:23:42 zabbixt01 systemd[1]: Starting Elasticsearch...
 9월 08 13:23:58 zabbixt01 systemd[1]: Started Elasticsearch.
 9월 23 11:31:04 zabbixt01 systemd[1]: Stopping Elasticsearch...
 9월 23 11:31:04 zabbixt01 systemd[1]: Stopped Elasticsearch.
[root@zabbixt01 elasticsearch]# 
Code Block 41 elasticsearch stop

삭제(yum remove)

서비스 종료 후 수행해야 합니다.

[root@zabbixt01 7.15.0]# yum list | grep elasticsearch
 
elasticsearch.x86_64                    7.15.0-1                   installed    
pcp-pmda-elasticsearch.x86_64           4.1.0-4.el7                local-repo   
[root@zabbixt01 7.15.0]# yum remove elasticsearch
HIWARE: WARNING. Please confirm your command.
Allow command Input?(y/n) 
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Resolving Dependencies
--> Running transaction check
---> Package elasticsearch.x86_64 0:7.15.0-1 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
========================================================================================================================================================
 Package                                 Arch                             Version                             Repository                           Size
========================================================================================================================================================
Removing:
 elasticsearch                           x86_64                           7.15.0-1                            installed                           543 M
 
Transaction Summary
========================================================================================================================================================
Remove  1 Package
 
Installed size: 543 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Stopping elasticsearch service... OK
  Erasing    : elasticsearch-7.15.0-1.x86_64                                                                                                        1/1 
  Verifying  : elasticsearch-7.15.0-1.x86_64                                                                                                        1/1 
 
Removed:
  elasticsearch.x86_64 0:7.15.0-1                                                                                                                       
 
Complete!
[root@zabbixt01 7.15.0]# 
Code Block 42 elasticsearch remove

[Kibana] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.6 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드

서비스	안내 페이지	서비스 버전	다운로드 path
ElasticSearch	https://www.elastic.co/downloads/elasticsearch
	7.14.1	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.15.0-x86_64.rpm

Logstash	https://www.elastic.co/kr/downloads/logstash
7.14.1	https://artifacts.elastic.co/downloads/logstash/logstash-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/logstash/logstash-7.15.0-x86_64.rpm

Kibana	https://www.elastic.co/downloads/kibana
7.14.1	https://artifacts.elastic.co/downloads/kibana/kibana-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/kibana/kibana-7.15.0-x86_64.rpm

Filebeat	https://www.elastic.co/kr/downloads/beats/filebeat
7.14.1(64 bit)	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.14.1-x86_64.rpm

		7.15.0(64 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-x86_64.rpm

		7.15.0(32 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-i686.rpm

프로그램 설치 및 최초 실행
설치
[root@zabbixt01 7.15.0]# yum install kibana-7.15.0-x86_64.rpm
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Examining kibana-7.15.0-x86_64.rpm: kibana-7.15.0-1.x86_64
Marking kibana-7.15.0-x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package kibana.x86_64 0:7.15.0-1 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
========================================================================================================================================================
 Package                         Arch                            Version                           Repository                                      Size
========================================================================================================================================================
Installing:
 kibana                          x86_64                          7.15.0-1                          /kibana-7.15.0-x86_64                          749 M
 
Transaction Summary
========================================================================================================================================================
Install  1 Package
 
Total size: 749 M
Installed size: 749 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : kibana-7.15.0-1.x86_64                                                                                                               1/1 
Creating kibana group... OK
Creating kibana user... OK
  Verifying  : kibana-7.15.0-1.x86_64                                                                                                               1/1 
 
Installed:
  kibana.x86_64 0:7.15.0-1                                                                                                                              
 
Complete!
[root@zabbixt01 7.15.0]# 
Code Block 43 kibana install

설정
/etc/kibana/kibana.yml 내 아래 정보 입력
# Kibana is served by a back end server. This setting specifies the port to use.
#server.port: 5601
server.port: 5601       ##사용할 service port
# Specifies the address to which the Kibana server will bind. IP addresses and host names are both valid values.
# The default is 'localhost', which usually means remote machines will not be able to connect.
# To allow connections from remote users, set this parameter to a non-loopback address.
#server.host: "localhost"
server.host: "0.0.0.0"   ##외부접속을 허용하기 위해 반드시 0.0.0.0 으로 변경 필요
# Enables you to specify a path to mount Kibana at if you are running behind a proxy.
# Use the `server.rewriteBasePath` setting to tell Kibana if it should remove the basePath
# from requests it receives, and to prevent a deprecation warning at startup.
# This setting cannot end in a slash.
#server.basePath: ""
 
# Specifies whether Kibana should rewrite requests that are prefixed with
# `server.basePath` or require that they are rewritten by your reverse proxy.
# This setting was effectively always `false` before Kibana 6.3 and will
# default to `true` starting in Kibana 7.0.
#server.rewriteBasePath: false
 
# Specifies the public URL at which Kibana is available for end users. If
# `server.basePath` is configured this URL should end with the same basePath.
#server.publicBaseUrl: ""
server.publicBaseUrl: "http://172.32.161.35:5601"
# The maximum payload size in bytes for incoming server requests.
#server.maxPayload: 1048576
 
# The Kibana server's name.  This is used for display purposes.
#server.name: "your-hostname"
 
# The URLs of the Elasticsearch instances to use for all your queries.
#elasticsearch.hosts: ["http://localhost:9200"]
elasticsearch.hosts: ["http://localhost:9200"]  ##elasticsearch host 위치. 해당 값이 없으면 kibana 실행되지 않습니다.
Code Block 44 kibana config

실행
[root@zabbixt01 kibana]# systemctl start kibana.service
[root@zabbixt01 kibana]# systemctl status kibana.service
● kibana.service - Kibana
   Loaded: loaded (/etc/systemd/system/kibana.service; disabled; vendor preset: disabled)
   Active: active (running) since 목 2021-09-23 15:57:10 KST; 4s ago
     Docs: https://www.elastic.co
 Main PID: 24479 (node)
   CGroup: /system.slice/kibana.service
           ├─24479 /usr/share/kibana/bin/../node/bin/node /usr/share/kibana/bin/../src/cli/dist --logging.dest="/var/log/kibana/kibana.log" --pid.fil...
           └─24492 /usr/share/kibana/node/bin/node --preserve-symlinks-main --preserve-symlinks /usr/share/kibana/src/cli/dist --logging.dest="/var/l...
 
 9월 23 15:57:10 zabbixt01 systemd[1]: Started Kibana.
[root@zabbixt01 kibana]# 
Code Block 45 kibana start

설치된 서버의 5601 포트로 접속
 
프로그램 종료

[root@zabbixt01 filebeat]# systemctl stop kibana.service
[root@zabbixt01 filebeat]# systemctl status kibana.service
● kibana.service - Kibana
   Loaded: loaded (/etc/systemd/system/kibana.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://www.elastic.co
 
 9월 08 13:26:41 zabbixt01 systemd[1]: Started Kibana.
 9월 17 09:48:37 zabbixt01 systemd[1]: Stopping Kibana...
 9월 17 09:48:37 zabbixt01 systemd[1]: Stopped Kibana.
 9월 17 09:48:45 zabbixt01 systemd[1]: Started Kibana.
 9월 17 09:51:10 zabbixt01 systemd[1]: Stopping Kibana...
 9월 17 09:51:10 zabbixt01 systemd[1]: Stopped Kibana.
 9월 17 09:51:18 zabbixt01 systemd[1]: Started Kibana.
 9월 23 10:30:48 zabbixt01 systemd[1]: Stopping Kibana...
 9월 23 10:30:50 zabbixt01 systemd[1]: Stopped Kibana.
[root@zabbixt01 filebeat]# 
Code Block 46 kibana stop

삭제(yum remove)

서비스 종료 후 수행해야 합니다.

[root@zabbixt01 7.15.0]# yum list | grep kibana
 
kibana.x86_64                           7.15.0-1                   installed    
[root@zabbixt01 7.15.0]# yum remove kibana
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Resolving Dependencies
--> Running transaction check
---> Package kibana.x86_64 0:7.15.0-1 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
========================================================================================================================================================
 Package                            Arch                               Version                              Repository                             Size
========================================================================================================================================================
Removing:
 kibana                             x86_64                             7.15.0-1                             installed                             749 M
 
Transaction Summary
========================================================================================================================================================
Remove  1 Package
 
Installed size: 749 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Stopping kibana service...Stopping kibana (via systemctl):  [  OK  ]
 OK
  Erasing    : kibana-7.15.0-1.x86_64                                                                                                               1/1 
Deleting log directory... OK
  Verifying  : kibana-7.15.0-1.x86_64                                                                                                               1/1 
 
Removed:
  kibana.x86_64 0:7.15.0-1                                                                                                                              
 
Complete!
[root@zabbixt01 7.15.0]#
Code Block 47 kibana remove

[Kibana] 화면 기능
로그 조회 방법
1.	Kibana web site 접근
 

2.	Observalility 메뉴 - Logs 메뉴 접근
 

3.	Logs 의 Stream 선택
 

4.	조회 기간 설정
 

화면 설명
Observalility
•	Overview
•	
•	Logs
•	
o	Stream - 로그 조회 및 분석을 위한 화면
o	 
•	검색 조건 조회
 

 
텍스트 데이터 검색 시 "message=검색할 텍스트명" 입력 후 검색 수행 필요
•	사용자 화
 
보여지는 화면을 사용자화 할 수 있음
•	Highlights
 
하이라이트에 표시한 텍스트를 강조하여 표시해 줌
•	조회 기간 입력
 

•	달력부분 클릭하여 정해진 기간 또는 원하는 기간을 입력하여 조회할 수 있음
[ELK Stack] Trubleshooting
Service	Issue	Issue message	조치방법	비고
Kibana	 	server.publicBaseUrl is missing and should be configured when running in a production environment.	/etc/kibana/kibana.yml 에 server.publicBaseUrl 에 해당 서버의 최초 접근 baseUrl 설정 필요
설정 시 주소 값 마지막에 / 를 제외하여 설정
예) server.publicBaseUrl: "172.32.161.35:5601"	
Kibana	 	Don’t lose one bit. Enable our free security features.	https://www.elastic.co/guide/en/elasticsearch/reference/7.15/configuring-stack-security.html?blade=kibanasecuritymessage 내 조치 방법 따름
무료 라이선스 상에서는 secure 옵션 설정 불가능
Elasticsearch	[2021-09-24T11:45:47,254][ERROR][o.e.i.g.GeoIpDownloader ] [zabbixt01] exception during geoip databases update
java.net.SocketTimeoutException: Connect timed out
.......	exception during geoip databases update	/etc/kibana/kibana.yml 에 ingest.geoip.downloader.enabled 옵션 변경
예) ingest.geoip.downloader.enabled: false	해당 옵션 false 로 해도 exception 발생한다는 리포트가 7.13 ~ 7.14 에서 제기된 바 있음
[ELK] 기타
보안

Generate the certificate authority
인증서 생성

/usr/share/elasticsearch/bin

[root@zabbixt01 bin]# pwd
/usr/share/elasticsearch/bin
[root@zabbixt01 bin]# ./elasticsearch-certutil ca
This tool assists you in the generation of X.509 certificates and certificate
signing requests for use with SSL/TLS in the Elastic stack.
 
The 'ca' mode generates a new 'certificate authority'
This will create a new X.509 certificate and private key that can be used
to sign certificate when running in 'cert' mode.
 
Use the 'ca-dn' option if you wish to configure the 'distinguished name'
of the certificate authority
 
By default the 'ca' mode produces a single PKCS#12 output file which holds:
    * The CA certificate
    * The CA's private key
 
If you elect to generate PEM format certificates (the -pem option), then the output will
be a zip file containing individual files for the CA certificate and private key
 
Please enter the desired output file [elastic-stack-ca.p12]: elastic-stack-ca.p12
Enter password for elastic-stack-ca.p12 : 
[root@zabbixt01 bin]# 

[root@zabbixt01 bin]# ./elasticsearch-certutil cert --ca elastic-stack-ca.p12
This tool assists you in the generation of X.509 certificates and certificate
signing requests for use with SSL/TLS in the Elastic stack.
 
The 'cert' mode generates X.509 certificate and private keys.
    * By default, this generates a single certificate and key for use
       on a single instance.
    * The '-multiple' option will prompt you to enter details for multiple
       instances and will generate a certificate and key for each one
    * The '-in' option allows for the certificate generation to be automated by describing
       the details of each instance in a YAML file
 
    * An instance is any piece of the Elastic Stack that requires an SSL certificate.
      Depending on your configuration, Elasticsearch, Logstash, Kibana, and Beats
      may all require a certificate and private key.
    * The minimum required value for each instance is a name. This can simply be the
      hostname, which will be used as the Common Name of the certificate. A full
      distinguished name may also be used.
    * A filename value may be required for each instance. This is necessary when the
      name would result in an invalid file or directory name. The name provided here
      is used as the directory name (within the zip) and the prefix for the key and
      certificate files. The filename is required if you are prompted and the name
      is not displayed in the prompt.
    * IP addresses and DNS names are optional. Multiple values can be specified as a
      comma separated string. If no IP addresses or DNS names are provided, you may
      disable hostname verification in your SSL configuration.
 
    * All certificates generated by this tool will be signed by a certificate authority (CA)
      unless the --self-signed command line option is specified.
      The tool can automatically generate a new CA for you, or you can provide your own with
      the --ca or --ca-cert command line options.
 
By default the 'cert' mode produces a single PKCS#12 output file which holds:
    * The instance certificate
    * The private key for the instance certificate
    * The CA certificate
 
If you specify any of the following options:
    * -pem (PEM formatted output)
    * -keep-ca-key (retain generated CA key)
    * -multiple (generate multiple certificates)
    * -in (generate certificates from an input file)
then the output will be be a zip file containing individual certificate/key files
 
Enter password for CA (elastic-stack-ca.p12) : 
Please enter the desired output file [elastic-certificates.p12]: elastic-certificates.p12
Enter password for elastic-certificates.p12 : 
 
Certificates written to /usr/share/elasticsearch/elastic-certificates.p12
 
This file should be properly secured as it contains the private key for 
your instance.
 
This file is a self contained file and can be copied and used 'as is'
For each Elastic product that you wish to configure, you should copy
this '.p12' file to the relevant configuration directory
and then follow the SSL configuration instructions in the product guide.
 
For client applications, you may only need to copy the CA certificate and
configure the client to trust this certificate.
[root@zabbixt01 bin]# 

[root@zabbixt01 elasticsearch]# pwd
/usr/share/elasticsearch
[root@zabbixt01 elasticsearch]# cp -rf *.p12 /etc/elasticsearch/

Encrypt internode communications with TLS
TLS 로 노드간 통신 암호화
cluster.name: elasticsearch-1
node.name: node-1
 
 
xpack.security.enabled: false
xpack.security.transport.ssl.enabled: false 
xpack.security.transport.ssl.verification_mode: certificate
xpack.security.transport.ssl.client_authentication: required
xpack.security.transport.ssl.keystore.path: elastic-certificates.p12
xpack.security.transport.ssl.truststore.path: elastic-certificates.p12



[root@zabbixt01 bin]# pwd
/usr/share/elasticsearch/bin
[root@zabbixt01 bin]# ./elasticsearch-keystore add xpack.security.transport.ssl.keystore.secure_password
Enter value for xpack.security.transport.ssl.keystore.secure_password: 
[root@zabbixt01 bin]# ./elasticsearch-keystore add xpack.security.transport.ssl.truststore.secure_password
Enter value for xpack.security.transport.ssl.truststore.secure_password: 
[root@zabbixt01 bin]# 

권한 변경
[root@zabbixt01 cert]# chown -R elasticsearch:elasticsearch elastic-certificates.p12
[root@zabbixt01 cert]# chown -R elasticsearch:elasticsearch elastic-stack-ca.p12
계정/패스워드 생성
[root@zabbixt01 bin]# ./elasticsearch-setup-passwords interactive
Initiating the setup of passwords for reserved users elastic,apm_system,kibana,kibana_system,logstash_system,beats_system,remote_monitoring_user.
You will be prompted to enter passwords as the process progresses.
Please confirm that you would like to continue [y/N]y
 
 
Enter password for [elastic]: 
Reenter password for [elastic]: 
Enter password for [apm_system]: 
Reenter password for [apm_system]: 
Enter password for [kibana_system]: 
Reenter password for [kibana_system]: 
Enter password for [logstash_system]: 
Reenter password for [logstash_system]: 
Enter password for [beats_system]: 
Reenter password for [beats_system]: 
Enter password for [remote_monitoring_user]: 
Reenter password for [remote_monitoring_user]: 
Changed password for user [apm_system]
Changed password for user [kibana_system]
Changed password for user [kibana]
Changed password for user [logstash_system]
Changed password for user [beats_system]
Changed password for user [remote_monitoring_user]
Changed password for user [elastic]
[root@zabbixt01 bin]# 

elasticsearch.username: "kibana_system"
elasticsearch.password: "skdltm100%"
Code Block 48 kibana.yml

[root@zabbixt01 bin]# pwd
/usr/share/kibana/bin
[root@zabbixt01 bin]# ./kibana-keystore add elasticsearch.password
Enter value for elasticsearch.password: **********


계정/패스워드 생성
Elasticsearch에 대한 최소 보안 설정편집하다
Elasticsearch 보안 기능을 활성화한 다음 기본 제공 사용자의 비밀번호를 생성합니다. 나중에 더 많은 사용자를 추가할 수 있지만 기본 제공 사용자를 사용하면 클러스터에 대한 보안을 활성화하는 프로세스가 간소화됩니다.
최소 보안 시나리오는 프로덕션 모드 클러스터에 충분하지 않습니다 . 클러스터에 여러 노드가 있는 경우 최소 보안을 활성화한 다음 노드 간에 TLS(전송 계층 보안) 를 구성 해야 합니다 .
전제 조건편집하다
Elasticsearch와 Kibana를 설치하고 구성합니다. Elastic Stack 시작하기 를 참조하십시오 .
원하는 특정 보안 기능이 포함된 라이센스를 사용하고 있는지 확인하십시오.
기본 라이선스에는 Elastic Stack에 대한 최소한의 보안 설정이 포함되어 있으므로 배포판을 다운로드하고 작업을 시작하기만 하면 됩니다. 무료 평가판 라이선스를 활성화하여 Elastic Stack의 모든 기능에 액세스할 수도 있습니다. 구독 및 라이선스 관리를 참조하십시오 .
Elasticsearch 보안 기능 활성화편집하다
기본 라이선스를 사용하면 Elasticsearch 보안 기능이 기본적으로 비활성화됩니다. Elasticsearch 보안 기능을 활성화하면 기본 인증이 활성화되어 사용자 이름 및 비밀번호 인증으로 로컬 클러스터를 실행할 수 있습니다.
에 모든 클러스터에서 노드, 키바와 Elasticsearch가 실행중인 경우를 모두 중지합니다.
에 모든 클러스터에 노드를 추가 xpack.security.enabled받는 설정을 $ES_PATH_CONF/elasticsearch.yml파일과 값을 설정합니다 true:
xpack.security.enabled: true
$ES_PATH_CONF변수는 Elasticsearch 구성 파일의 경로입니다. 아카이브 배포( zip또는 tar.gz)를 사용하여 Elasticsearch를 설치한 경우 변수의 기본값은 $ES_HOME/config. 패키지 배포(Debian 또는 RPM)를 사용한 경우 변수의 기본값은 /etc/elasticsearch.
클러스터에 단일 노드가 있는 경우 파일에 discovery.type설정을 추가 $ES_PATH_CONF/elasticsearch.yml하고 값을 로 설정합니다 single-node. 이 설정은 노드가 네트워크에서 실행 중인 다른 클러스터에 실수로 연결되지 않도록 합니다.
discovery.type: single-node
기본 제공 사용자의 암호 만들기편집하다
클러스터와 통신하려면 기본 제공 사용자의 사용자 이름을 구성해야 합니다. 익명 액세스를 활성화하지 않는 한 사용자 이름과 암호가 포함되지 않은 모든 요청은 거부됩니다.
최소 또는 기본 보안을 활성화할 때 elastic및 kibana_system사용자에 대한 암호만 설정 하면 됩니다.
에 모든 클러스터에서 노드 Elasticsearch를 시작합니다. 예를 들어 Elasticsearch를 .tar.gz패키지 와 함께 설치 한 경우 ES_HOME 디렉터리 에서 다음 명령을 실행합니다 .
./bin/elasticsearch
다른 터미널 창에서 elasticsearch-setup-passwords유틸리티 를 실행하여 기본 제공 사용자의 암호를 설정 합니다.
elasticsearch-setup-passwords클러스터의 모든 노드에 대해 유틸리티를 실행할 수 있습니다 . 그러나 이 유틸리티 는 전체 클러스터에 대해 한 번만 실행해야 합니다.
auto매개변수를 사용하면 나중에 필요한 경우 변경할 수 있는 무작위로 생성된 비밀번호가 콘솔에 출력됩니다.
./bin/elasticsearch-setup-passwords auto
고유한 암호를 사용하려면 interactive매개변수 대신 매개변수를 사용 하여 명령을 실행하십시오 auto. 이 모드를 사용하면 모든 기본 제공 사용자에 대한 암호 구성을 단계별로 안내합니다.
./bin/elasticsearch-setup-passwords interactive
생성된 비밀번호를 저장합니다. Kibana에 기본 제공 사용자를 추가하려면 필요합니다.
elastic사용자 의 암호를 설정한 후에 는 elasticsearch-setup-passwords명령을 두 번째로 실행할 수 없습니다 .
다음 : 비밀번호를 사용하여 Elasticsearch에 연결하도록 Kibana 구성
비밀번호를 사용하여 Elasticsearch에 연결하도록 Kibana 구성편집하다
Elasticsearch 보안 기능이 활성화되면 사용자는 유효한 사용자 이름과 암호를 사용하여 Kibana에 로그인해야 합니다.
기본 제공 kibana_system사용자와 이전에 생성한 암호 를 사용하도록 Kibana를 구성합니다 . Kibana는 kibana_system사용자를 사용해야 하는 몇 가지 백그라운드 작업을 수행합니다 .
이 계정은 개별 사용자를 위한 것이 아니며 브라우저에서 Kibana에 로그인할 수 있는 권한이 없습니다. 대신 elastic수퍼유저 로 Kibana에 로그인합니다.
파일에 elasticsearch.username설정을 추가하고 KIB_PATH_CONF/kibana.yml값을 kibana_system사용자로 설정합니다 .
elasticsearch.username: "kibana_system"
KIB_PATH_CONF변수는 키바 구성 파일의 경로입니다. 아카이브 배포( zip또는 tar.gz)를 사용하여 Kibana를 설치한 경우 변수의 기본값은 KIB_HOME/config. 패키지 배포(Debian 또는 RPM)를 사용한 경우 변수의 기본값은 /etc/kibana.
Kibana를 설치한 디렉토리에서 다음 명령을 실행하여 Kibana 키 저장소를 생성하고 보안 설정을 추가하십시오.
Kibana 키 저장소 생성:
./bin/kibana-keystore create
kibana_systemKibana 키 저장소에 사용자 의 비밀번호를 추가하십시오 .
./bin/kibana-keystore add elasticsearch.password
메시지가 표시되면 kibana_system사용자 의 암호를 입력합니다 .
Kibana를 다시 시작하십시오. 예를 들어 .tar.gz패키지 와 함께 Kibana를 설치 한 경우 Kibana 디렉터리에서 다음 명령을 실행합니다.
./bin/kibana
elastic사용자 로 Kibana에 로그인 합니다. 이 수퍼유저 계정을 사용하여 공간 을 관리하고, 새 사용자를 만들고, 역할을 할당합니다 . 로컬에서 Kibana를 실행하는 경우 http://localhost:5601로그인 페이지를 보려면 로 이동 하십시오.
무엇 향후 계획?편집하다
축하합니다! 무단 액세스를 방지하기 위해 로컬 클러스터에 대한 암호 보호를 활성화했습니다. elastic 사용자 로 안전하게 Kibana에 로그인하고 추가 사용자 및 역할을 생성 할 수 있습니다 . 단일 노드 클러스터를 실행하는 경우 여기에서 중지할 수 있습니다.
클러스터에 여러 노드가 있는 경우 노드 간에 TLS(전송 계층 보안)를 구성해야 합니다. TLS를 활성화하지 않으면 프로덕션 모드 클러스터가 시작되지 않습니다.
클러스터의 노드 간의 모든 내부 통신을 보호하기 위해 Elastic Stack 에 대한 기본 보안을 설정 합니다.
Opensearch
개요
elastic 과 AWS(Amazoe web service) 간의 분쟁으로 태어난 오픈소스 데이터 처리 솔루션
일시	AWS	elastic
2018.2		elastic 에서 상용 확장팩인 X-pack 을 Elastic 라이선스로 적용하여 공개
(기존 elastic 기능은 Apache 2.0)
X-pack : security, Alert, 모니터링 등의 추가 기능
2019.3	elastic 의 라이선스가 상용소스코드가 섞여 문제가 된다고 판단, X-Pack 의 기능 일부를 포함한 Open Distro for Elasticsearch 를 공개	
2021.1		7.11 버전부터 Elasticsearch 와 Kibana 의 라이선스를 Apache2.0 에서 SSPL 로 변경
(AWS 의 기여 없는 소스코드 사용을 비난)
2021.1	Apache2.0 라이선스의 7.10 버전을 fork 하여 공개 후 직접 운영하겠다고 발표	
2021.8	fork 버전인 OpenSearch 1.0 발표	
기본 설정 정보(default 설정)

서비스	환경설정 파일	서비스 로그파일	비고
			
			
			
			

서비스	안내 페이지	서비스 버전	다운로드 path
opensearch	https://opensearch.org/downloads.html
1.0.0  CURRENT 	https://artifacts.opensearch.org/releases/bundle/opensearch/1.1.0/opensearch-1.0.0-linux-x64.tar.gz

		1.1.0  TESTED 	https://artifacts.opensearch.org/releases/bundle/opensearch/1.1.0/opensearch-1.1.0-linux-x64.tar.gz

opensearch dashboard	https://opensearch.org/downloads.html
1.0.0  CURRENT 	https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/1.0.0/opensearch-dashboards-1.0.0-linux-x64.tar.gz

		1.1.0  TESTED 	https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/1.1.0/opensearch-dashboards-1.1.0-linux-x64.tar.gz

Ingest Tools	https://opensearch.org/downloads.html
7.13.2 CURRENT 	https://artifacts.opensearch.org/logstash/logstash-oss-with-opensearch-output-plugin-7.13.2-linux-x64.tar.gz

Filebeat OSS 7.12.1	https://www.elastic.co/downloads/past-releases/filebeat-oss-7-12-1
7.12.1 STABLE 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-windows-x86.zip
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-windows-x86_64.zip
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-linux-x86.tar.gz
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-linux-x86_64.tar.gz




OpenSearch 를 시작/중지/상태 확인하기 위한 shell script

#!/bin/bash
 
ARGV=$2
INSTNAME=$1
USER="pg"
OPENSEARCH_HOME_DIR=/data/opensearch
 
function user_check(){
  UNAME=`id -u -n`
  if [ e$UNAME != "e$USER" ]; then
      echo -e " [\e[1;31m Use by only user account\e[0m [ \e[33m$USER\e[0m ] Start Fail - \e[1;33m$INSTNAME\e[0m ]"
      echo " "
      exit;
  fi
}
 
case $ARGV in
start)
  user_check
    case $INSTNAME in
      opensearch)
            run_inst=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')
            if [ -z "$run_inst" ]; then
                $OPENSEARCH_HOME_DIR/opensearch-1.0.0/bin/opensearch -d
                echo -e " \e[1;34m Starting \e[0m [ \e[1;33m$INSTNAME\e[0m ....] "
                  while (true) 
                  do
                      PID=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')
                      if [ ! -z "$PID" ]; then
                          echo -e $INSTNAME" pid :" $PID " started."
                          echo " "
                          exit
                      else
                          sleep 1.5
                      fi
                   done
            else
                echo -e " \e[1;33m Already Running\e[0m [ \e[1;33m$INSTNAME\e[0m (pid:$run_inst)] !!! "
                ERROR=$?
                echo " "        
            fi
      ;;
      opensearch_dashboard)
            run_inst=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
            if [ -z "$run_inst" ]; then
                nohup  $OPENSEARCH_HOME_DIR/opensearch-dashboards-1.0.0/bin/opensearch-dashboards serve -l /data/opensearch/opensearch-dashboards-1.0.0/logs/opensearch-dashboard.log  > /dev/null 2>&1 &
                echo -e " \e[1;34m Starting \e[0m [ \e[1;33m$INSTNAME\e[0m ....] "
                  while (true) 
                  do
                      PID=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
                      if [ ! -z "$PID" ]; then
                          echo -e $INSTNAME" pid :" $PID " started."
                          echo " "
                          exit
                      else
                          sleep 1.5
                      fi
                   done
            else
                echo -e " \e[1;33m Already Running\e[0m [ \e[1;33m$INSTNAME\e[0m (pid:$run_inst)] !!! "
                ERROR=$?
                echo " "        
            fi
      ;;
      logstash)
            run_inst=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
            if [ -z "$run_inst" ]; then
                nohup  $OPENSEARCH_HOME_DIR/logstash-7.13.2/bin/logstash --config.reload.automatic --pipeline.unsafe_shutdown > /dev/null 2>&1 &
                echo -e " \e[1;34m Starting \e[0m [ \e[1;33m$INSTNAME\e[0m ....] "
                  while (true) 
                  do
                      PID=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
                      if [ ! -z "$PID" ]; then
                          echo -e $INSTNAME" pid :" $PID " started."
                          echo " "
                          exit
                      else
                          sleep 1.5
                      fi
                   done
            else
                echo -e " \e[1;33m Already Running\e[0m [ \e[1;33m$INSTNAME\e[0m (pid:$run_inst)] !!! "
                ERROR=$?
                echo " "        
            fi
      ;;
      filebeat)
        echo $INSTNAME
      ;;
      *)
        echo -e "instance list : [ \e[1;31m opensearch \e[0m | \e[1;31m opensearch_dashboard \e[0m | \e[1;31m logstash \e[0m | \e[1;31m fllebeat \e[0m ]"
      ;;
      esac
;;
stop)
  user_check
    case $INSTNAME in
      opensearch)
      runinst=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')
      echo "runinst : $runinst"
      kill $runinst
      echo -e " \e[1;31m Stopping \e[0m[ \e[1;33m$INSTNAME\e[0m ] "
      echo -e " \e[1;31m Instance\e[0m [ \e[1;35m$INSTNAME\e[0m ] \e[1;31mShutdown OK ! \e[0m"
      ;;
      opensearch_dashboard)
        echo $INSTNAME
      runinst=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
      echo "runinst : $runinst"
      kill $runinst
      echo -e " \e[1;31m Stopping \e[0m[ \e[1;33m$INSTNAME\e[0m ] "
      echo -e " \e[1;31m Instance\e[0m [ \e[1;35m$INSTNAME\e[0m ] \e[1;31mShutdown OK ! \e[0m"
      ;;
      logstash)
      runinst=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
      echo "runinst : $runinst"
      kill $runinst
      echo -e " \e[1;31m Stopping \e[0m[ \e[1;33m$INSTNAME\e[0m ] "
      echo -e " \e[1;31m Instance\e[0m [ \e[1;35m$INSTNAME\e[0m ] \e[1;31mShutdown OK ! \e[0m"
      ;;
      filebeat)
        echo $INSTNAME
      ;;
      *)
        echo -e "instance list : [ \e[1;31m opensearch \e[0m | \e[1;31m opensearch_dashboard \e[0m | \e[1;31m logstash \e[0m | \e[1;31m fllebeat \e[0m ]"
      ;;
      esac
;;
status)
    case $INSTNAME in
      opensearch)
        runinst=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')
        if [ -z "$runinst" ]; then
           echo -e $INSTNAME " stop."
        else
           echo -e $INSTNAME" pid :" $runinst " started."
        fi
      ;;
      opensearch_dashboard)
      runinst=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
        if [ -z "$runinst" ]; then
           echo -e $INSTNAME " stop."
        else
           echo -e $INSTNAME" pid :" $runinst " started."
        fi
      ;;
      logstash)
      runinst=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
        if [ -z "$runinst" ]; then
           echo -e $INSTNAME " stop."
        else
           echo -e $INSTNAME" pid :" $runinst " started."
        fi
      ;;
      filebeat)
        echo $INSTNAME
      ;;
      *)
        echo -e "instance list : [ \e[1;31m opensearch \e[0m | \e[1;31m opensearch_dashboard \e[0m | \e[1;31m logstash \e[0m | \e[1;31m fllebeat \e[0m ]"
      ;;
      esac
;;
*)
        echo " " 
        echo -e "Status : Invalid parameter [ \e[1;31m$ARGV\e[0m ]"
        echo "parameter start|stop"
 
;;
 
esac
 
exit $ERROR
Code Block 49 launcher.sh

하위페이지
•	[opensearch] 설치/실행 안내
•	[logstash] 환경설정 방법
•	[OpenSearch] 대시보드 사용방법
•	[Opensearch] Trubleshooting
•	_temp [opensearch] 설치/실행 안내
[opensearch] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.6 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 서비스(pg) 계정에서 수행하였습니다.

다운로드

서비스	안내 페이지	서비스 버전	다운로드 path
opensearch	https://opensearch.org/downloads.html
1.0.0  CURRENT 	https://artifacts.opensearch.org/releases/bundle/opensearch/1.1.0/opensearch-1.0.0-linux-x64.tar.gz

		1.1.0  TESTED 	https://artifacts.opensearch.org/releases/bundle/opensearch/1.1.0/opensearch-1.1.0-linux-x64.tar.gz

opensearch dashboard	https://opensearch.org/downloads.html
1.0.0  CURRENT 	https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/1.0.0/opensearch-dashboards-1.0.0-linux-x64.tar.gz

		1.1.0  TESTED 	https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/1.1.0/opensearch-dashboards-1.1.0-linux-x64.tar.gz

Ingest Tools	https://opensearch.org/downloads.html
7.13.2 CURRENT 	https://artifacts.opensearch.org/logstash/logstash-oss-with-opensearch-output-plugin-7.13.2-linux-x64.tar.gz

Filebeat OSS 7.12.1	https://www.elastic.co/downloads/past-releases/filebeat-oss-7-12-1
7.12.1 STABLE 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-windows-x86.zip
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-windows-x86_64.zip
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-linux-x86.tar.gz
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-linux-x86_64.tar.gz

프로그램 설치 및 최초 실행(tarball 기준)
opensearch
1.	다운로드 파일 압축 해제
tar -xvf opensearch-1.0.0-linux-x64.tar.gz
2.	환경설정(기본 포함 파일 사용)
# ======================== OpenSearch Configuration =========================
#
# NOTE: OpenSearch comes with reasonable defaults for most settings.
#       Before you set out to tweak and tune the configuration, make sure you
#       understand what are you trying to accomplish and the consequences.
#
# The primary way of configuring a node is via this file. This template lists
# the most important settings you may want to configure for a production cluster.
#
# Please consult the documentation for further information on configuration options:
# https://www.opensearch.org
#
# ---------------------------------- Cluster -----------------------------------
#
# Use a descriptive name for your cluster:
#
#cluster.name: my-application
#
# ------------------------------------ Node ------------------------------------
#
# Use a descriptive name for the node:
#
#node.name: node-1
#
# Add custom attributes to the node:
#
#node.attr.rack: r1
#
# ----------------------------------- Paths ------------------------------------
#
# Path to directory where to store the data (separate multiple locations by comma):
#
#path.data: /path/to/data
#
# Path to log files:
#
#path.logs: /path/to/logs
#
# ----------------------------------- Memory -----------------------------------
#
# Lock the memory on startup:
#
#bootstrap.memory_lock: true
#
# Make sure that the heap size is set to about half the memory available
# on the system and that the owner of the process is allowed to use this
# limit.
#
# OpenSearch performs poorly when the system is swapping the memory.
#
# ---------------------------------- Network -----------------------------------
#
# Set the bind address to a specific IP (IPv4 or IPv6):
#
#network.host: 192.168.0.1
#
# Set a custom port for HTTP:
#
#http.port: 9200
#
# For more information, consult the network module documentation.
#
# --------------------------------- Discovery ----------------------------------
#
# Pass an initial list of hosts to perform discovery when this node is started:
# The default list of hosts is ["127.0.0.1", "[::1]"]
#
#discovery.seed_hosts: ["host1", "host2"]
#
# Bootstrap the cluster using an initial set of master-eligible nodes:
#
#cluster.initial_master_nodes: ["node-1", "node-2"]
#
# For more information, consult the discovery and cluster formation module documentation.
#
# ---------------------------------- Gateway -----------------------------------
#
# Block initial recovery after a full cluster restart until N nodes are started:
#
#gateway.recover_after_nodes: 3
#
# For more information, consult the gateway module documentation.
#
# ---------------------------------- Various -----------------------------------
#
# Require explicit names when deleting indices:
#
#action.destructive_requires_name: true
 
######## Start OpenSearch Security Demo Configuration ########
# WARNING: revise all the lines below before you go into production
plugins.security.ssl.transport.pemcert_filepath: esnode.pem
plugins.security.ssl.transport.pemkey_filepath: esnode-key.pem
plugins.security.ssl.transport.pemtrustedcas_filepath: root-ca.pem
plugins.security.ssl.transport.enforce_hostname_verification: false
plugins.security.ssl.http.enabled: true
plugins.security.ssl.http.pemcert_filepath: esnode.pem
plugins.security.ssl.http.pemkey_filepath: esnode-key.pem
plugins.security.ssl.http.pemtrustedcas_filepath: root-ca.pem
plugins.security.allow_unsafe_democertificates: true
plugins.security.allow_default_init_securityindex: true
plugins.security.authcz.admin_dn:
  - CN=kirk,OU=client,O=client,L=test, C=de
 
plugins.security.audit.type: internal_opensearch
plugins.security.enable_snapshot_restore_privilege: true
plugins.security.check_snapshot_restore_write_privileges: true
plugins.security.restapi.roles_enabled: ["all_access", "security_rest_api_access"]
plugins.security.system_indices.enabled: true
plugins.security.system_indices.indices: [".opendistro-alerting-config", ".opendistro-alerting-alert*", ".opendistro-anomaly-results*", ".opendistro-anomaly-detector*", ".opendistro-anomaly-checkpoints", ".opendistro-anomaly-detection-state", ".opendistro-reports-*", ".opendistro-notifications-*", ".opendistro-notebooks", ".opendistro-asynchronous-search-response*"]
node.max_local_storage_nodes: 3
######## End OpenSearch Security Demo Configuration ########
Code Block 50 config/opensearch.yml
3.	실행
bin/opensearch -d
4.	opensearch start option
Option 	Description 
-E <KeyValuePair>	Configure a setting 
-V, --version 	Prints OpenSearch version information and exits 
-d, --daemonize	Starts OpenSearch in the background 
-h, --help 	Show help 
-p, --pidfile <Path> 	Creates a pid file in the specified path on start 
-q, --quiet 	Turns off standard output/error streams logging in console
-s, --silent 	Show minimal output 
-v, --verbose 	Show verbose output
opensearch-dashboard
1.	다운로드 파일 압축해제
2.	환경설정 server.host: "0.0.0.0" 추가
# Copyright 2021 Amazon.com, Inc. or its affiliates. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License").
# You may not use this file except in compliance with the License.
# A copy of the License is located at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# or in the "license" file accompanying this file. This file is distributed
# on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either
# express or implied. See the License for the specific language governing
# permissions and limitations under the License.
 
# Description:
# Default configuration for OpenSearch Dashboards
 
opensearch.hosts: ["https://localhost:9200"]
opensearch.ssl.verificationMode: none
opensearch.username: "kibanaserver"
opensearch.password: "kibanaserver"
opensearch.requestHeadersWhitelist: [ authorization,securitytenant ]
 
opensearch_security.multitenancy.enabled: true
opensearch_security.multitenancy.tenants.preferred: ["Private", "Global"]
opensearch_security.readonly_mode.roles: ["kibana_read_only"]
# Use this setting if you are running kibana without https
opensearch_security.cookie.secure: false
 
server.host: "0.0.0.0"
Code Block 51 config/opensearch_dashboards.yml
3.	실행
bin/opensearch-dashboards serve -l /data/opensearch/opensearch-dashboards-1.0.0/logs/opensearch-dashboard.log
4.	opensearch-dashboard start option
Option	Description 
-e, --opensearch <uri1,uri2>	OpenSearch instances
-c, --config <path>	Path to the config file, use multiple --config args to include multiple config files (default: ["/data/opensearch/opensearch-dashboards-1.0.0/config/opensearch_dashboards.yml"])
-p, --port <port>	The port to bind to
-q, --quiet	Prevent all logging except errors
-Q, --silent	Prevent all logging
 --verbose	Turns on verbose logging
-H, --host <host>	The host to bind to
-l, --log-file <path>	The file to log to
--plugin-dir <path>	A path to scan for plugins, this can be specified multiple times to specify multiple directories (default: ["/data/opensearch/opensearch-dashboards-1.0.0/plugins"])
--plugin-path <path>	A path to a plugin which should be included by the server, this can be specified multiple times to specify multiple paths (default: [])
--plugins <path>	an alias for --plugin-dir
--optimize 	Deprecated, running the optimizer is no longer required
-h, --help	output usage information
logstash
1.	다운로드 파일 압축 해제
tar -xvf logstash-oss-with-opensearch-output-plugin-7.13.2-linux-x64.tar.gz
2.	환경설정
[logstash] 환경설정 방법 참고
3.	실행
bin/logstash -f config/beat-pipelines.conf --config.reload.automatic --pipeline.unsafe_shutdown
4.	logstash start option
Option 	Description 
-n, --node.name NAME 	Specify the name of this logstash instance, if no value is given it will default to the current hostname.
(default: "zabbixt01")
-f, --path.config CONFIG_PATH	Load the logstash config from a specific file or directory. If a directory is given, all files in that directory will be concatenated in lexicographical order and then parsed as a single config file. You can also specify wildcards (globs) and any matched files will be loaded in the order described above.
-e, --config.string CONFIG_STRING	Use the given string as the configuration data. Same syntax as the config file. If no input is specified, then the following is used as the default input: "input { stdin { type => stdin } }" and if no output is specified, then the following is used as the default output:
"output { stdout { codec => rubydebug } }"
If you wish to use both defaults, please use the empty string for the '-e' flag.
(default: nil)
--field-reference-parser MODE	(DEPRECATED) This option is no longer configurable.

Use the given MODE when parsing field references.

The field reference parser is used to expand field references in your pipeline configs,
and has become more strict to better handle ambiguous- and illegal-syntax inputs.

The only available MODE is:
- `STRICT`: parse in a strict manner; when given ambiguous- or illegal-syntax input,
raises a runtime exception that should be handled by the calling plugin.
(default: "STRICT")
--modules MODULES	Load Logstash modules.
Modules can be defined using multiple instances
'--modules module1 --modules module2',
or comma-separated syntax
'--modules=module1,module2'
Cannot be used in conjunction with '-e' or '-f' Use of '--modules' will override modules declared in the 'logstash.yml' file.
-M, --modules.variable MODULES_VARIABLE	Load variables for module template. Multiple instances of '-M' or '--modules.variable' are supported.
Ignored if '--modules' flag is not used.
Should be in the format of '-M "MODULE_NAME.var.PLUGIN_TYPE.PLUGIN_NAME.VARIABLE_NAME=VALUE"' as in
'-M "example.var.filter.mutate.fieldname=fieldvalue"'
--setup	Load index template into Elasticsearch, and saved searches,
index-pattern, visualizations, and dashboards into Kibana when running modules.
(default: false)
--cloud.id CLOUD_ID	Sets the elasticsearch and kibana host settings for module connections in Elastic Cloud.
Your Elastic Cloud User interface or the Cloud support team should provide this.
Add an optional label prefix '<label>:' to help you identify multiple cloud.ids.
e.g. 'staging:dXMtZWFzdC0xLmF3cy5mb3VuZC5pbyRub3RhcmVhbCRpZGVudGlmaWVy'
--cloud.auth CLOUD_AUTH	Sets the elasticsearch and kibana username and password
for module connections in Elastic Cloud e.g. 'username:<password>'
--pipeline.id ID	Sets the ID of the pipeline.
(default: "main")
-w, --pipeline.workers COUNT	Sets the number of pipeline workers to run.
(default: 2)
--pipeline.ordered ORDERED	Preserve events order. Possible values are `auto` (default), `true` and `false`.
This setting
will only work when also using a single worker for the pipeline.
Note that when enabled, it may impact the performance of the filters and ouput processing.
The `auto` option will automatically enable ordering if the `pipeline.workers` setting is set to `1`.
Use `true` to enable ordering on the pipeline and prevent logstash from starting if there are multiple workers.
Use `false` to disable any extra processing necessary for preserving ordering.
(default: "auto")
--java-execution	Use Java execution engine.
(default: true)
--plugin-classloaders	(Beta) Load Java plugins in independent classloaders to isolate their dependencies.
(default: false)
-b, --pipeline.batch.size SIZE	Size of batches the pipeline is to work in.
(default: 125)
-u, --pipeline.batch.delay DELAY_IN_MS	When creating pipeline batches, how long to wait while polling for the next event.
(default: 50)
--pipeline.unsafe_shutdown	Force logstash to exit during shutdown even if there are still inflight events in memory.
By default, logstash will refuse to quit until all received events have been pushed to the outputs.
(default: false)
--pipeline.ecs_compatibility STRING	Sets the pipeline's default value for `ecs_compatibility`, a setting that is available to plugins that implement an ECS Compatibility mode for use with the Elastic Common Schema.
Possible values are:
- disabled (default)
- v1
- v2
This option allows the early opt-in (or preemptive opt-out) of ECS Compatibility modes in plugins, which is scheduled to be on-by-default in a future major release of Logstash.
Values other than `disabled` are currently considered BETA, and may produce unintended consequences when upgrading Logstash.
(default: "disabled")
--path.data PATH	This should point to a writable directory. Logstash will use this directory whenever it needs to store data. Plugins will also have access to this path.
(default: "/data/opensearch/logstash-7.13.2/data")
-p, --path.plugins PATH	A path of where to find plugins. This flag can be given multiple times to include multiple paths. Plugins are expected to be in a specific directory hierarchy:
'PATH/logstash/TYPE/NAME.rb' where TYPE is 'inputs' 'filters', 'outputs' or 'codecs' and NAME is the name of the plugin.
(default: [])
-l, --path.logs PATH	Write logstash internal logs to the given file. Without this flag, logstash will emit logs to standard output.
(default: "/data/opensearch/logstash-7.13.2/logs")
--log.level LEVEL	Set the log level for logstash. Possible values are:
- fatal
- error
- warn
- info
- debug
- trace
(default: "info")
--config.debug	Print the compiled config ruby code out as a debug log (you must also have --log.level=debug enabled).
WARNING: This will include any 'password' options passed to plugin configs as plaintext, and may result in plaintext passwords appearing in your logs!
(default: false)
-i, --interactive SHELL	Drop to shell instead of running as normal.
Valid shells are "irb" and "pry"
-V, --version	Emit the version of logstash and its friends, then exit.
-t, --config.test_and_exit	Check configuration for valid syntax and then exit.
(default: false)
-r, --config.reload.automatic	Monitor configuration changes and reload whenever it is changed.
NOTE: use SIGHUP to manually reload the config
(default: false)
--config.reload.interval RELOAD_INTERVAL	How frequently to poll the configuration location for changes, in seconds.
(default: #<Java::OrgLogstashUtil::TimeValue:0x69b96cd>)
--http.enabled ENABLED	Can be used to disable the Web API, which is enabled by default.
(default: true)
--http.host HTTP_HOST	Web API binding host (default: "127.0.0.1")
--http.port HTTP_PORT	Web API http port (default: 9600..9700)
--log.format FORMAT	Specify if Logstash should write its own logs in JSON form (one event per line) or in plain text (using Ruby's Object#inspect)
(default: "plain")
--path.settings SETTINGS_DIR	Directory containing logstash.yml file. This can also be set through the LS_SETTINGS_DIR environment variable.
(default: "/data/opensearch/logstash-7.13.2/config")
--verbose	Set the log level to info.
DEPRECATED: use --log.level=info instead.
--debug	Set the log level to debug.
DEPRECATED: use --log.level=debug instead.
--quiet	Set the log level to info.
DEPRECATED: use --log.level=info instead.
-h, --help	print help
Filebeat
[Filebeat] 설치/실행 안내 참고
[logstash] 환경설정 방법
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.6 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 서비스(pg) 계정에서 수행하였습니다.

pipeline 설정 방법
pipelines.yml 설정
 - pipeline.id: log
   path.config: "/data/opensearch/logstash-7.13.2/config/nicepay-pipelines.conf"
Code Block 52 pipelines.yml

nicepay-pipelines.conf 설정
# Beats -> Logstash -> Opensearch pipeline.
 
input {
  beats {
    port => 5044
    ssl => false
    host => "0.0.0.0"
    include_codec_tag => false
  }
}
 
filter {
  if "ims" in [tags] {
    grok {
      match => {"message" => ["^\[%{TIMESTAMP_ISO8601:logtime}]%{SPACE}%{LOGLEVEL:loglevel}%{SPACE}%{GREEDYDATA:logmsg}"
                              ,"%{GREEDYDATA:logmsg}"]}
      remove_field => ["SPACE"]
    }
    date {
      match => ["logtime","YYYY-MM-dd H:m:s"]
      target => "@timestamp"
      timezone => "Asia/Seoul"
    }
  }
}
 
output {
  if "ims" in [tags] {
    opensearch {
      hosts => ["https://localhost:9200"]
      user => "logstash"
      password => "logstash"
      index => "logstash-ims-%{[host][name]}-%{+YYYY.MM.dd}"
      ssl_certificate_verification => false
    }
  }
  else if "mms" in [tags] {
    opensearch {
      hosts => ["https://localhost:9200"]
      user => "logstash"
      password => "logstash"
      index => "logstash-mms-%{[host][name]}-%{+YYYY.MM.dd}"
      ssl_certificate_verification => false
    }
  }
  else {
    opensearch {
      hosts => ["https://localhost:9200"]
      user => "logstash"
      password => "logstash"
      index => "logstash-etc-%{[host][name]}-%{+YYYY.MM.dd}"
      ssl_certificate_verification => false
    }
  }
}
Code Block 53 nicepay-pipeline.conf

beat-pipelines.conf(예제용)
# Beats -> Logstash -> Elasticsearch pipeline.
 
input {
  beats {
    port => 5044
    ssl => false
    host => "0.0.0.0"
  }
}
 
filter {
  if "ims" in [log][file][path] {
    grok {
      match => {"message" => ["^\[%{TIMESTAMP_ISO8601:logtime}]%{SPACE}%{LOGLEVEL:loglevel}%{SPACE}%{GREEDYDATA:logmsg}"]}
      remove_field => ["SPACE"]
    }
    #mutate {
    #  rename => {"@timestamp" => "read_timestamp" }
    #  add_field => {"read_timestamp" => "%{@timestamp}"}
    #}
    date {
      match => ["logtime","YYYY-MM-dd H:m:s"]
      target => "@timestamp"
      timezone => "Asia/Seoul"
    }
  }
}
output {
  if "ims" in [log][file][path] {
    opensearch {
      hosts => ["https://localhost:9200"]
      user => "logstash"
      password => "logstash"
      index => "logstash-ims-%{[host][name]}-%{+YYYY.MM.dd}"
      ssl_certificate_verification => false
    }
  }
  else if "mms" in [log][file][path] {
    opensearch {
      hosts => ["https://localhost:9200"]
      user => "logstash"
      password => "logstash"
      index => "logstash-mms-%{[host][name]}-%{+YYYY.MM.dd}"
      ssl_certificate_verification => false
    }
  }
  else {
    opensearch {
      hosts => ["https://localhost:9200"]
      user => "logstash"
      password => "logstash"
      index => "logstash-etc-%{[host][name]}-%{+YYYY.MM.dd}"
      ssl_certificate_verification => false
    }
  }
}
Code Block 54 beat-pipeline.conf

json-pipelines.conf(예제용)
# Sample Logstash configuration for creating a simple
# Beats -> Logstash -> Elasticsearch pipeline.
 
input {
  stdin {
    codec => json
  }
}
 
output {
  opensearch {
    hosts => ["https://localhost:9200"]
    user => "logstash"
    password => "logstash"
    index => "logstash-%{+YYYY.MM.dd}"
    ssl_certificate_verification => false
  }
}
Code Block 55 json-pipeline.conf

[OpenSearch] 대시보드 사용방법
로그인
접속 주소 : http://172.32.161.35:5601/
계정 및 패스워드 입력





 
Switch tenant 설정(개인설정 : private / 공통설정 : global)
기본 설정을 global 로 설정했으므로, 기존 설정된 내용을 보고 싶으시면 global 을 사용하시면 됩니다.

 
 
OpenSearch Dashboards
Overview
Discover
로그의 _raw 데이터를 검색하고 확인 가능
Index pattern 선택
오른쪽 상단의 index pattern 을 선택하여 원하는 인덱스 패턴을 선택
필요할 경우 텍스트 상자를 통해 검색도 가능
 
검색 기간 설정
왼쪽 상단의 달력 모양 버튼 또는 설정된 기간을 선택하여
빠르게 검색 기간을 지정 가능
 
필요할 경우 절대/상대적 시간 설정도 가능
 
검색 키워드(필터링) 선택
상단의 텍스트 박스를 이용하여 검색 내용 중 키워드 필터링이 가능(와일드 카드 사용 가능)
 
필드 선택
조건 선택 완료 후 기본 선택된 “_source” 로는 데이터 판단이 어려움
 
사전에 logstash 를 통해 정의한 필드인 “loglevel” 또는 “logmsg” 를 선택하여 검색 결과를 확인해야 함
 
 
Dashboard
시각화 도구를 이용한 대시보드 화면 구성이 가능함
 
Visualize
OpenSearch PlugIns

Query Workbench
SQL 을 통해 데이터를 테이블 형식으로 검색할 수 있는 기능
익숙한 SQL 을 통해 쉽게 데이터 조회 가능
1. SQL 작성 및 결과
 logstash-ims-pg_was_test-2021.10.27 index 의 logmsg 에  “xcetion” 이 포함된 데이터를 10개만 시간과 함께 검색
(select @timestamp, logmsg from logstash-ims-pg_was_test-2021.10.27 where logmsg LIKE '%xception%' LIMIT 10;)
 
검색 결과로 @timestamp 와 logmsg 가 결과로 검색 됨
 
Notebooks
 
 
Reporting
Alerting
특정 index 의 지정된 임계치 를 초과할 경우 경고를 발생 시킬 수 있도록 화면 구성이 가능함
 


Anomaly Detection
Trace Analytics
Index Management
Security
Management

Dev Tools
OpenSearch 의 Restful API 를 실행할 수 있는 개발툴
일반적으로 index 정보를 확인하거나 등록/수정/삭제 시 사용


 
 
Stack Management
Index Patterns
생성된 Index(data source) 를 패턴으로 묶어 Dashboard 와 Discover 에서 검색 단위를 만드는 데 사용합니다.
Create index pattern 클릭
 
Step 1 of 2 : Define an index pattern
index 이름을 입력하거나 wild card 를 이용해 다중의 index 를 선택 후, Next Step 클릭
 
Step 2 of 2 : Configure settings
시간 기준이 되는 필드를 선택하고, 추가로 커스텀 인덱스 패턴 ID 를 추가 설정할 수 있음
 
생성 완료 후 정보 확인
 

Saved Objects
저장되어 있는 Index pattern 또는 고급 설정 정보를 확인 가능
 
Advanced Settings
고급 설정 정보 변경 가능
[Opensearch] Trubleshooting

•	영향도 정보
•	An illegal reflective access operation has occurred
영향도 정보

영향도	내용
 해결됨 	해결된 이슈
 낮음 	시스템 동작에 영향을 주지 않거나 성능 하락에 미비한 정도의 이슈
 보통 	시스템 동작에 영향을 주지 않지만 성능 하락이 발생하는 이슈
 치명 	시스템이 동작하지 않거나 중요한 보안 이슈의 경우
An illegal reflective access operation has occurred

version	1.0.0
영향도	 낮음 
원인	opensearch-security-1.0.0.0.jar 의 reflective access 이슈
내용	WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.opensearch.security.support.Base64Helper$DescriptorNameSetter
(file:/data/opensearch/opensearch-1.0.0/plugins/opensearch-security/opensearch-security-1.0.0.0.jar) to field java.io.ObjectStreamClass.name
WARNING: Please consider reporting this to the maintainers of org.opensearch.security.support.Base64Helper$DescriptorNameSetter
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release

참고	간헐적 발생 및 Warning 로 서비스 영향 없으나, 발생 원인 추적 중
해결방법	실행 시 --illegal-access=permit 설정
_temp [opensearch] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.6 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드

서비스	안내 페이지	서비스 버전	다운로드 path
opensearch	https://opensearch.org/downloads.html
1.0.0  CURRENT 	https://artifacts.opensearch.org/releases/bundle/opensearch/1.1.0/opensearch-1.0.0-linux-x64.tar.gz

		1.1.0  TESTED 	https://artifacts.opensearch.org/releases/bundle/opensearch/1.1.0/opensearch-1.1.0-linux-x64.tar.gz

opensearch dashboard	https://opensearch.org/downloads.html
1.0.0  CURRENT 	https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/1.0.0/opensearch-dashboards-1.0.0-linux-x64.tar.gz

		1.1.0  TESTED 	https://artifacts.opensearch.org/releases/bundle/opensearch-dashboards/1.1.0/opensearch-dashboards-1.1.0-linux-x64.tar.gz

Ingest Tools	https://opensearch.org/downloads.html
7.13.2 CURRENT 	https://artifacts.opensearch.org/logstash/logstash-oss-with-opensearch-output-plugin-7.13.2-linux-x64.tar.gz

Filebeat OSS 7.12.1	https://www.elastic.co/downloads/past-releases/filebeat-oss-7-12-1
7.12.1 STABLE 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-windows-x86.zip
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-windows-x86_64.zip
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-linux-x86.tar.gz
https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-7.12.1-linux-x86_64.tar.gz

프로그램 설치 및 최초 실행
설치
[pg@zabbixt01 opensearch-1.1.0]$ pwd
/data/opensearch/opensearch-1.1.0
[pg@zabbixt01 opensearch-1.1.0]$ ls -al
합계 252
drwxr-xr-x 10 pg pg    263 10월  7 15:54 .
drwxr-xr-x  4 pg pg     65 10월  7 15:53 ..
-rw-r--r--  1 pg pg  11358 10월  7 15:53 LICENSE.txt
-rw-r--r--  1 pg pg 215355 10월  7 15:53 NOTICE.txt
-rw-r--r--  1 pg pg   1761 10월  7 15:53 README.md
drwxr-xr-x  2 pg pg    263 10월  7 15:53 bin
drwxr-xr-x  5 pg pg    279 10월  7 15:54 config
drwxr-xr-x  9 pg pg    107 10월  7 15:53 jdk
drwxr-xr-x  3 pg pg   4096 10월  7 15:53 lib
drwxr-xr-x  2 pg pg    336 10월  7 15:54 logs
-rw-r--r--  1 pg pg   3690 10월  7 15:53 manifest.yml
drwxr-xr-x 19 pg pg   4096 10월  7 15:53 modules
-rwxr-xr-x  1 pg pg   3092 10월  7 15:53 opensearch-tar-install.sh
drwxr-xr-x  6 pg pg     59 10월  7 15:53 performance-analyzer-rca
drwxr-xr-x 14 pg pg   4096 10월  7 15:53 plugins
-rwxr-xr-x  1 pg pg    375 10월  7 15:54 securityadmin_demo.sh
[pg@zabbixt01 opensearch-1.1.0]$ ./opensearch-tar-install.sh 
OpenSearch Security Demo Installer
 ** Warning: Do not use on production or public reachable systems **
Basedir: /data/opensearch/opensearch-1.1.0
OpenSearch install type: .tar.gz on NAME="Red Hat Enterprise Linux Server"
OpenSearch config dir: /data/opensearch/opensearch-1.1.0/config
OpenSearch config file: /data/opensearch/opensearch-1.1.0/config/opensearch.yml
OpenSearch bin dir: /data/opensearch/opensearch-1.1.0/bin
OpenSearch plugins dir: /data/opensearch/opensearch-1.1.0/plugins
OpenSearch lib dir: /data/opensearch/opensearch-1.1.0/lib
Detected OpenSearch Version: x-content-1.1.0
Detected OpenSearch Security Version: 1.1.0.0
/data/opensearch/opensearch-1.1.0/config/opensearch.yml seems to be already configured for Security. Quit.
Code Block 56 opensearch install

정상 실행 여부 확인
[root@zabbixt01 opensearch-1.1.0]# curl -u 'admin:admin' --insecure -X GET https://localhost:9200
{
  "name" : "zabbixt01",
  "cluster_name" : "opensearch",
  "cluster_uuid" : "0ShMTZmsQ0S8iOvzzRejWQ",
  "version" : {
    "distribution" : "opensearch",
    "number" : "1.1.0",
    "build_type" : "tar",
    "build_hash" : "15e9f137622d878b79103df8f82d78d782b686a1",
    "build_date" : "2021-10-04T21:29:03.079792Z",
    "build_snapshot" : false,
    "lucene_version" : "8.9.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "The OpenSearch Project: https://opensearch.org/"
}
[root@zabbixt01 opensearch-1.1.0]# curl -u 'admin:admin' --insecure -X GET https://localhost:9200/_cat/plugins?v
name      component                            version
zabbixt01 opensearch-alerting                  1.1.0.0
zabbixt01 opensearch-anomaly-detection         1.1.0.0
zabbixt01 opensearch-asynchronous-search       1.1.0.0
zabbixt01 opensearch-cross-cluster-replication 1.1.0.0
zabbixt01 opensearch-index-management          1.1.0.0
zabbixt01 opensearch-job-scheduler             1.1.0.0
zabbixt01 opensearch-knn                       1.1.0.0
zabbixt01 opensearch-notebooks                 1.1.0.0
zabbixt01 opensearch-performance-analyzer      1.1.0.0
zabbixt01 opensearch-reports-scheduler         1.1.0.0
zabbixt01 opensearch-security                  1.1.0.0
zabbixt01 opensearch-sql                       1.1.0.0
[root@zabbixt01 opensearch-1.1.0]# 
Code Block 57 opensearch curl command

opensearch start option
Option 	Description 
-E <KeyValuePair>	Configure a setting 
-V, --version 	Prints OpenSearch version information and exits 
-d, --daemonize	Starts OpenSearch in the background 
-h, --help 	Show help 
-p, --pidfile <Path> 	Creates a pid file in the specified path on start 
-q, --quiet 	Turns off standard output/error streams logging in console
-s, --silent 	Show minimal output 
-v, --verbose 	Show verbose output
opensearch-dashboard start option
Option	Description 
-e, --opensearch <uri1,uri2>	OpenSearch instances
-c, --config <path>	Path to the config file, use multiple --config args to include multiple config files (default: ["/data/opensearch/opensearch-dashboards-1.0.0/config/opensearch_dashboards.yml"])
-p, --port <port>	The port to bind to
-q, --quiet	Prevent all logging except errors
-Q, --silent	Prevent all logging
 --verbose	Turns on verbose logging
-H, --host <host>	The host to bind to
-l, --log-file <path>	The file to log to
--plugin-dir <path>	A path to scan for plugins, this can be specified multiple times to specify multiple directories (default: ["/data/opensearch/opensearch-dashboards-1.0.0/plugins"])
--plugin-path <path>	A path to a plugin which should be included by the server, this can be specified multiple times to specify multiple paths (default: [])
--plugins <path>	an alias for --plugin-dir
--optimize 	Deprecated, running the optimizer is no longer required
-h, --help	output usage information

logstash start option
Option 	Description 
-n, --node.name NAME 	Specify the name of this logstash instance, if no value is given
it will default to the current hostname.
(default: "zabbixt01")
-f, --path.config CONFIG_PATH	Load the logstash config from a specific file
or directory. If a directory is given, all
files in that directory will be concatenated
in lexicographical order and then parsed as a
single config file. You can also specify
wildcards (globs) and any matched files will
be loaded in the order described above.
-e, --config.string CONFIG_STRING	Use the given string as the configuration
data. Same syntax as the config file. If no
input is specified, then the following is
used as the default input:
"input { stdin { type => stdin } }"
and if no output is specified, then the
following is used as the default output:
"output { stdout { codec => rubydebug } }"
If you wish to use both defaults, please use
the empty string for the '-e' flag.
(default: nil)
--field-reference-parser MODE	(DEPRECATED) This option is no longer
configurable.

Use the given MODE when parsing field
references.

The field reference parser is used to expand
field references in your pipeline configs,
and has become more strict to better handle
ambiguous- and illegal-syntax inputs.

The only available MODE is:
- `STRICT`: parse in a strict manner; when
given ambiguous- or illegal-syntax input,
raises a runtime exception that should
be handled by the calling plugin.

(default: "STRICT")
--modules MODULES	Load Logstash modules.
Modules can be defined using multiple instances
'--modules module1 --modules module2',
or comma-separated syntax
'--modules=module1,module2'
Cannot be used in conjunction with '-e' or '-f'
Use of '--modules' will override modules declared
in the 'logstash.yml' file.
-M, --modules.variable MODULES_VARIABLE	Load variables for module template.
Multiple instances of '-M' or
'--modules.variable' are supported.
Ignored if '--modules' flag is not used.
Should be in the format of
'-M "MODULE_NAME.var.PLUGIN_TYPE.PLUGIN_NAME.VARIABLE_NAME=VALUE"'
as in
'-M "example.var.filter.mutate.fieldname=fieldvalue"'
--setup	Load index template into Elasticsearch, and saved searches,
index-pattern, visualizations, and dashboards into Kibana when
running modules.
(default: false)
--cloud.id CLOUD_ID
Sets the elasticsearch and kibana host settings for
module connections in Elastic Cloud.
Your Elastic Cloud User interface or the Cloud support
team should provide this.
Add an optional label prefix '<label>:' to help you
identify multiple cloud.ids.
e.g. 'staging:dXMtZWFzdC0xLmF3cy5mb3VuZC5pbyRub3RhcmVhbCRpZGVudGlmaWVy'
--cloud.auth CLOUD_AUTH	Sets the elasticsearch and kibana username and password
for module connections in Elastic Cloud
e.g. 'username:<password>'
--pipeline.id ID	Sets the ID of the pipeline.
(default: "main")
-w, --pipeline.workers COUNT	Sets the number of pipeline workers to run.
(default: 2)
--pipeline.ordered ORDERED	Preserve events order. Possible values are `auto` (default), `true` and `false`.
This setting
will only work when also using a single worker for the pipeline.
Note that when enabled, it may impact the performance of the filters
and ouput processing.
The `auto` option will automatically enable ordering if the
`pipeline.workers` setting is set to `1`.
Use `true` to enable ordering on the pipeline and prevent logstash
from starting if there are multiple workers.
Use `false` to disable any extra processing necessary for preserving
ordering.
(default: "auto")
--java-execution	Use Java execution engine.
(default: true)
--plugin-classloaders	(Beta) Load Java plugins in independent classloaders to isolate their dependencies.
(default: false)
-b, --pipeline.batch.size SIZE	Size of batches the pipeline is to work in.
(default: 125)
-u, --pipeline.batch.delay DELAY_IN_MS	When creating pipeline batches, how long to wait while polling
for the next event.
(default: 50)
--pipeline.unsafe_shutdown	Force logstash to exit during shutdown even
if there are still inflight events in memory.
By default, logstash will refuse to quit until all
received events have been pushed to the outputs.
(default: false)
--pipeline.ecs_compatibility STRING	Sets the pipeline's default value for `ecs_compatibility`,
a setting that is available to plugins that implement
an ECS Compatibility mode for use with the Elastic Common
Schema.
Possible values are:
- disabled (default)
- v1
- v2
This option allows the early opt-in (or preemptive opt-out)
of ECS Compatibility modes in plugins, which is scheduled to
be on-by-default in a future major release of Logstash.

Values other than `disabled` are currently considered BETA,
and may produce unintended consequences when upgrading Logstash.
(default: "disabled")
--path.data PATH	This should point to a writable directory. Logstash
will use this directory whenever it needs to store
data. Plugins will also have access to this path.
(default: "/data/opensearch/logstash-7.13.2/data")
-p, --path.plugins PATH	A path of where to find plugins. This flag
can be given multiple times to include
multiple paths. Plugins are expected to be
in a specific directory hierarchy:
'PATH/logstash/TYPE/NAME.rb' where TYPE is
'inputs' 'filters', 'outputs' or 'codecs'
and NAME is the name of the plugin.
(default: [])
-l, --path.logs PATH	Write logstash internal logs to the given
file. Without this flag, logstash will emit
logs to standard output.
(default: "/data/opensearch/logstash-7.13.2/logs")
--log.level LEVEL	Set the log level for logstash. Possible values are:
- fatal
- error
- warn
- info
- debug
- trace
(default: "info")
--config.debug	Print the compiled config ruby code out as a debug log (you must also have --log.level=debug enabled).
WARNING: This will include any 'password' options passed to plugin configs as plaintext, and may result
in plaintext passwords appearing in your logs!
(default: false)
-i, --interactive SHELL	Drop to shell instead of running as normal.
Valid shells are "irb" and "pry"
-V, --version	Emit the version of logstash and its friends,
then exit.
-t, --config.test_and_exit	Check configuration for valid syntax and then exit.
(default: false)
-r, --config.reload.automatic	Monitor configuration changes and reload
whenever it is changed.
NOTE: use SIGHUP to manually reload the config
(default: false)
--config.reload.interval RELOAD_INTERVAL	How frequently to poll the configuration location
for changes, in seconds.
(default: #<Java::OrgLogstashUtil::TimeValue:0x69b96cd>)
--http.enabled ENABLED	Can be used to disable the Web API, which is
enabled by default.
(default: true)
--http.host HTTP_HOST	Web API binding host (default: "127.0.0.1")
--http.port HTTP_PORT	Web API http port (default: 9600..9700)
--log.format FORMAT	Specify if Logstash should write its own logs in JSON form (one
event per line) or in plain text (using Ruby's Object#inspect)
(default: "plain")
--path.settings SETTINGS_DIR	Directory containing logstash.yml file. This can also be
set through the LS_SETTINGS_DIR environment variable.
(default: "/data/opensearch/logstash-7.13.2/config")
--verbose	Set the log level to info.
DEPRECATED: use --log.level=info instead.
--debug	Set the log level to debug.
DEPRECATED: use --log.level=debug instead.
--quiet	Set the log level to info.
DEPRECATED: use --log.level=info instead.
-h, --help	print help
#!/bin/bash
 
ARGV=$2
INSTNAME=$1
USER="pg"
OPENSEARCH_HOME_DIR=/data/opensearch
 
function user_check(){
  UNAME=`id -u -n`    
  if [ e$UNAME != "e$USER" ]; then
      echo -e " [\e[1;31m Use by only user account\e[0m [ \e[33m$USER\e[0m ] Start Fail - \e[1;33m$INSTNAME\e[0m ]"
      echo " "
      exit;
  fi    
}
 
case $ARGV in
start)
  user_check
    case $INSTNAME in
      opensearch)
            run_inst=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')
            if [ -z "$run_inst" ]; then
                $OPENSEARCH_HOME_DIR/opensearch-1.0.0/bin/opensearch -d
                echo -e " \e[1;34m Starting \e[0m [ \e[1;33m$INSTNAME\e[0m ....] "
                  while (true) 
              do
                      PID=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')    
                      if [ ! -z "$PID" ]; then
                          echo -e $INSTNAME" pid :" $PID " started."
                          echo " "
                          exit
                      else
                          sleep 1.5        
                      fi
                   done
            else
                echo -e " \e[1;33m Already Running\e[0m [ \e[1;33m$INSTNAME\e[0m (pid:$run_inst)] !!! "
                ERROR=$?
                echo " "        
            fi
      ;;
      opensearch_dashboard)
            run_inst=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
            if [ -z "$run_inst" ]; then
                nohup  $OPENSEARCH_HOME_DIR/opensearch-dashboards-1.0.0/bin/opensearch-dashboards serve -l /data/opensearch/opensearch-dashboards-1.0.0/logs/opensearch-dashboard.log  > /dev/null 2>&1 &
                echo -e " \e[1;34m Starting \e[0m [ \e[1;33m$INSTNAME\e[0m ....] "
                  while (true) 
                  do
                      PID=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
                      if [ ! -z "$PID" ]; then
                          echo -e $INSTNAME" pid :" $PID " started."
                          echo " "
                          exit
                      else
                          sleep 1.5
                      fi
                   done
            else
                echo -e " \e[1;33m Already Running\e[0m [ \e[1;33m$INSTNAME\e[0m (pid:$run_inst)] !!! "
                ERROR=$?
                echo " "        
            fi
      ;;
      logstash)
            run_inst=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
            if [ -z "$run_inst" ]; then
                nohup  $OPENSEARCH_HOME_DIR/logstash-7.13.2/bin/logstash --config.reload.automatic --pipeline.unsafe_shutdown > /dev/null 2>&1 &
                echo -e " \e[1;34m Starting \e[0m [ \e[1;33m$INSTNAME\e[0m ....] "
                  while (true) 
                  do
                      PID=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
                      if [ ! -z "$PID" ]; then
                          echo -e $INSTNAME" pid :" $PID " started."
                          echo " "
                          exit
                      else
                          sleep 1.5
                      fi
                   done
            else
                echo -e " \e[1;33m Already Running\e[0m [ \e[1;33m$INSTNAME\e[0m (pid:$run_inst)] !!! "
                ERROR=$?
                echo " "        
            fi
      ;;      
      filebeat)
    echo $INSTNAME
      ;;
      *)
    echo -e "instance list : [ \e[1;31m opensearch \e[0m | \e[1;31m opensearch_dashboard \e[0m | \e[1;31m logstash \e[0m | \e[1;31m fllebeat \e[0m ]"
      ;;
      esac
;;
stop)
  user_check
    case $INSTNAME in
      opensearch)
      runinst=$(lsof -i:9200 | grep 'LISTEN' | awk '{print $2}')
      echo "runinst : $runinst"
      kill $runinst
      echo -e " \e[1;31m Stopping \e[0m[ \e[1;33m$INSTNAME\e[0m ] "
      echo -e " \e[1;31m Instance\e[0m [ \e[1;35m$INSTNAME\e[0m ] \e[1;31mShutdown OK ! \e[0m"
      ;;
      opensearch_dashboard)
        echo $INSTNAME
      runinst=$(lsof -i:5601 | grep 'LISTEN' | awk '{print $2}')
      echo "runinst : $runinst"
      kill $runinst
      echo -e " \e[1;31m Stopping \e[0m[ \e[1;33m$INSTNAME\e[0m ] "
      echo -e " \e[1;31m Instance\e[0m [ \e[1;35m$INSTNAME\e[0m ] \e[1;31mShutdown OK ! \e[0m"
      ;;
      logstash)
      runinst=$(lsof -i:9600 | grep 'LISTEN' | awk '{print $2}')
      echo "runinst : $runinst"
      kill $runinst
      echo -e " \e[1;31m Stopping \e[0m[ \e[1;33m$INSTNAME\e[0m ] "
      echo -e " \e[1;31m Instance\e[0m [ \e[1;35m$INSTNAME\e[0m ] \e[1;31mShutdown OK ! \e[0m"
      ;;      
      filebeat)
        echo $INSTNAME
      ;;
      *)
        echo -e "instance list : [ \e[1;31m opensearch \e[0m | \e[1;31m opensearch_dashboard \e[0m | \e[1;31m logstash \e[0m | \e[1;31m fllebeat \e[0m ]"
      ;;
      esac
;;
status)
;;
*)
        echo " " 
        echo -e "Status : Invalid parameter [ \e[1;31m$ARGV\e[0m ]"
    echo "parameter start|stop"
 
;;
 
esac
 
exit $ERROR
Code Block 58 launcher.sh



실행 : 
opensearch-1.0.0/bin/opensearch -d -p pid.out
curl -u 'admin:admin' --insecure -X GET https://localhost:9200/_cat/indices?v
종료 :
kill pid
SIGINT

opensearch-dashboard
nohup  $OPENSEARCH_HOME_DIR/opensearch-dashboards-1.0.0/bin/opensearch-dashboards > /dev/null 2>&1 &
lsof -i:5601 | grep 'LISTEN'| awk '{print $2}'

logstash 실행
bin/logstash -f config/beat-pipelines.conf --config.reload.automatic
 ./logstash-7.13.2/bin/logstash -f logstash-7.13.2/config/beat-pipelines.conf --config.reload.automatic --pipeline.unsafe_shutdown


nohup  ./logstash-7.13.2/bin/logstash -f logstash-7.13.2/config/beat-pipelines.conf --config.reload.automatic --pipeline.unsafe_shutdown &
nohup  $OPENSEARCH_HOME_DIR/logstash-7.13.2/bin/logstash -f $OPENSEARCH_HOME_DIR/logstash-7.13.2/config/beat-pipelines.conf --config.reload.automatic --pipeline.unsafe_shutdown > /dev/null 2>&1 &

lsof -i:9600 | grep 'LISTEN' | awk '{print $2}'
실행(opensearch-dashboard)

Code Block 59 opensearch dashboard

.bash_profile
# .bash_profile
 
# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi
 
# User specific environment and startup programs
 
PATH=$PATH:$HOME/.local/bin:$HOME/bin
 
export PATH
 
OPENSEARCH_HOME_DIR=/data/opensearch



설정
/etc/elasticsearch/elasticsearch.yml 내 아래 정보 입력

Code Block 60 elasticsearch config

실행

Code Block 61 opensearch start

프로그램 종료


Code Block 62 opensearch stop

삭제(yum remove)

서비스 종료 후 수행해야 합니다.


Code Block 63 opensearch remove

bin/logstash -f config/beat-pipeline.conf 

[2021-10-12T13:04:52,943][WARN ][logstash.outputs.elasticsearch][main] Attempted to resurrect connection to dead ES instance, but got an error {:url=>"http://localhost:9200/", :exception=>LogStash::Outputs::ElasticSearch::HttpClient::Pool::HostUnreachableError, :message=>"Elasticsearch Unreachable: [http://localhost:9200/][Manticore::ClientProtocolException] localhost:9200 failed to respond"}
opensearch 계정정보 미입력 오류

/data/opensearch/opensearch-1.1.0/plugins/opensearch-security/securityconfig/internal_users.yml
Beats
 
개요
Beats 는 데이터를 Elasticsearch 로 보내기 위해 서버에 에이전트 방식으로 설치되는 오픈소스 데이터 수집기 입니다. 
Beats 는 아래와 같은 제품군이 존재합니다.
Beat 이름	용도	download URL
  Filebeat	경량 로그 수집기	https://www.elastic.co/kr/beats/filebeat

  Metricbeat	경량 메트릭 수집기	https://www.elastic.co/kr/beats/metricbeat

  Packetbeat	경량 네트워크 데이터 수집기	https://www.elastic.co/kr/beats/packetbeat

  Winlogbeat	경량 Windows 이벤트 로그 수집기	https://www.elastic.co/kr/beats/winlogbeat

  Auditbeat	Linux 경량 감사 데이터 수집기	https://www.elastic.co/kr/beats/auditbeat

  Heartbeat	서버 가용성 모니터링을 위한 경량 데이터 수집기	https://www.elastic.co/kr/beats/heartbeat

  Functionbeat	클라우드 데이터를 위한 서버리스(Faas) 수집기	https://www.elastic.co/kr/beats/functionbeat

Beats 는 직접 Elasticsearch 를 통해 데이터를 보낼 수 있습니다.
또는 Logstash 를 이용하여 데이터를 파싱 또는 필터링하여 데이터의 질을 향상시킬 수 있습니다.
하위 페이지
•	[Filebeat] 설치/실행 안내
•	[Filebeat] 환경설정 방법
[Filebeat] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.6 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드

서비스	안내 페이지	서비스 버전	다운로드 path
ElasticSearch	https://www.elastic.co/downloads/elasticsearch
	7.14.1	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.15.0-x86_64.rpm

Logstash	https://www.elastic.co/kr/downloads/logstash
7.14.1	https://artifacts.elastic.co/downloads/logstash/logstash-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/logstash/logstash-7.15.0-x86_64.rpm

Kibana	https://www.elastic.co/downloads/kibana
7.14.1	https://artifacts.elastic.co/downloads/kibana/kibana-7.14.1-x86_64.rpm

		7.15.0  CURRENT 	https://artifacts.elastic.co/downloads/kibana/kibana-7.15.0-x86_64.rpm

Filebeat	https://www.elastic.co/kr/downloads/beats/filebeat
7.14.1(64 bit)	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.14.1-x86_64.rpm

		7.15.0(64 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-x86_64.rpm

		7.15.0(32 bit)  CURRENT 	https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.15.0-i686.rpm

프로그램 설치 및 최초 실행
설치(yum install)
[root@zabbixt01 7.15.0]# yum install filebeat-7.15.0-x86_64.rpm 
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Examining filebeat-7.15.0-x86_64.rpm: filebeat-7.15.0-1.x86_64
Marking filebeat-7.15.0-x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package filebeat.x86_64 0:7.15.0-1 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
======================================================================================================================================================================
 Package                             Arch                              Version                               Repository                                          Size
======================================================================================================================================================================
Installing:
 filebeat                            x86_64                            7.15.0-1                              /filebeat-7.15.0-x86_64                            136 M
 
Transaction Summary
======================================================================================================================================================================
Install  1 Package
 
Total size: 136 M
Installed size: 136 M
Is this ok [y/d/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : filebeat-7.15.0-1.x86_64                                                                                                                           1/1 
  Verifying  : filebeat-7.15.0-1.x86_64                                                                                                                           1/1 
 
Installed:
  filebeat.x86_64 0:7.15.0-1                                                                                                                                          
 
Complete!
[root@zabbixt01 7.15.0]# 
Code Block 64 filebeat install

설치(tarball)
1.	다운로드 파일 압축 해제
tar -xvf filebeat-oss-7.12.1-linux-x86.tar.gz
2.	환경설정
[filebeat] 환경설정 방법 참고
설정
[Filebeat] 환경설정 방법 참고
yum install : /etc/filebeat/filebeat.yml
tarball : 압축푼 위치의 filebeat.yml
설정 파일 변경 적용
[root@zabbixt01 filebeat]# filebeat setup -e
2021-09-23T17:31:48.658+0900    INFO    instance/beat.go:665    Home path: [/usr/share/filebeat] Config path: [/etc/filebeat] Data path: [/var/lib/filebeat] Logs path: [/var/log/filebeat]
2021-09-23T17:31:48.658+0900    INFO    instance/beat.go:673    Beat ID: 75bcc3b0-f76f-4a09-a728-778b95f66a9b
2021-09-23T17:31:48.660+0900    INFO    [beat]  instance/beat.go:1014   Beat info   {"system_info": {"beat": {"path": {"config": "/etc/filebeat", "data": "/var/lib/filebeat", "home": "/usr/share/filebeat", "logs": "/var/log/filebeat"}, "type": "filebeat", "uuid": "75bcc3b0-f76f-4a09-a728-778b95f66a9b"}}}
2021-09-23T17:31:48.660+0900    INFO    [beat]  instance/beat.go:1023   Build info  {"system_info": {"build": {"commit": "9023152025ec6251bc6b6c38009b309157f10f17", "libbeat": "7.15.0", "time": "2021-09-16T03:16:09.000Z", "version": "7.15.0"}}}
2021-09-23T17:31:48.660+0900    INFO    [beat]  instance/beat.go:1026   Go runtime info {"system_info": {"go": {"os":"linux","arch":"amd64","max_procs":2,"version":"go1.16.6"}}}
2021-09-23T17:31:48.661+0900    INFO    [beat]  instance/beat.go:1030   Host info   {"system_info": {"host": {"architecture":"x86_64","boot_time":"2021-09-23T16:43:09+09:00","containerized":false,"name":"zabbixt01","ip":["127.0.0.1/8","172.32.161.35/24"],"kernel_version":"3.10.0-957.el7.x86_64","mac":["00:50:56:8d:0e:99"],"os":{"type":"linux","family":"redhat","platform":"rhel","name":"Red Hat Enterprise Linux Server","version":"7.6 (Maipo)","major":7,"minor":6,"patch":0,"codename":"Maipo"},"timezone":"KST","timezone_offset_sec":32400,"id":"ff43e759b6a745b7890621ffd4d1bdea"}}}
2021-09-23T17:31:48.661+0900    INFO    [beat]  instance/beat.go:1059   Process info    {"system_info": {"process": {"capabilities": {"inheritable":null,"permitted":["chown","dac_override","dac_read_search","fowner","fsetid","kill","setgid","setuid","setpcap","linux_immutable","net_bind_service","net_broadcast","net_admin","net_raw","ipc_lock","ipc_owner","sys_module","sys_rawio","sys_chroot","sys_ptrace","sys_pacct","sys_admin","sys_boot","sys_nice","sys_resource","sys_time","sys_tty_config","mknod","lease","audit_write","audit_control","setfcap","mac_override","mac_admin","syslog","wake_alarm","block_suspend"],"effective":["chown","dac_override","dac_read_search","fowner","fsetid","kill","setgid","setuid","setpcap","linux_immutable","net_bind_service","net_broadcast","net_admin","net_raw","ipc_lock","ipc_owner","sys_module","sys_rawio","sys_chroot","sys_ptrace","sys_pacct","sys_admin","sys_boot","sys_nice","sys_resource","sys_time","sys_tty_config","mknod","lease","audit_write","audit_control","setfcap","mac_override","mac_admin","syslog","wake_alarm","block_suspend"],"bounding":["chown","dac_override","dac_read_search","fowner","fsetid","kill","setgid","setuid","setpcap","linux_immutable","net_bind_service","net_broadcast","net_admin","net_raw","ipc_lock","ipc_owner","sys_module","sys_rawio","sys_chroot","sys_ptrace","sys_pacct","sys_admin","sys_boot","sys_nice","sys_resource","sys_time","sys_tty_config","mknod","lease","audit_write","audit_control","setfcap","mac_override","mac_admin","syslog","wake_alarm","block_suspend"],"ambient":null}, "cwd": "/etc/filebeat", "exe": "/usr/share/filebeat/bin/filebeat", "name": "filebeat", "pid": 10072, "ppid": 7425, "seccomp": {"mode":"disabled"}, "start_time": "2021-09-23T17:31:48.300+0900"}}}
2021-09-23T17:31:48.661+0900    INFO    instance/beat.go:309    Setup Beat: filebeat; Version: 7.15.0
2021-09-23T17:31:48.662+0900    INFO    [index-management]  idxmgmt/std.go:184  Set output.elasticsearch.index to 'filebeat-7.15.0' as ILM is enabled.
2021-09-23T17:31:48.662+0900    INFO    [esclientleg]   eslegclient/connection.go:100   elasticsearch url: http://localhost:9200
2021-09-23T17:31:48.662+0900    INFO    [publisher] pipeline/module.go:113  Beat name: zabbixt01
2021-09-23T17:31:48.663+0900    INFO    [esclientleg]   eslegclient/connection.go:100   elasticsearch url: http://localhost:9200
2021-09-23T17:31:48.669+0900    INFO    [esclientleg]   eslegclient/connection.go:273   Attempting to connect to Elasticsearch version 7.15.0
Overwriting ILM policy is disabled. Set `setup.ilm.overwrite: true` for enabling.
 
2021-09-23T17:31:48.689+0900    INFO    [index-management]  idxmgmt/std.go:261  Auto ILM enable success.
2021-09-23T17:31:48.690+0900    INFO    [index-management.ilm]  ilm/std.go:170  ILM policy filebeat exists already.
2021-09-23T17:31:48.690+0900    INFO    [index-management]  idxmgmt/std.go:401  Set setup.template.name to '{filebeat-7.15.0 {now/d}-000001}' as ILM is enabled.
2021-09-23T17:31:48.690+0900    INFO    [index-management]  idxmgmt/std.go:406  Set setup.template.pattern to 'filebeat-7.15.0-*' as ILM is enabled.
2021-09-23T17:31:48.690+0900    INFO    [index-management]  idxmgmt/std.go:440  Set settings.index.lifecycle.rollover_alias in template to {filebeat-7.15.0 {now/d}-000001} as ILM is enabled.
2021-09-23T17:31:48.690+0900    INFO    [index-management]  idxmgmt/std.go:444  Set settings.index.lifecycle.name in template to {filebeat {"policy":{"phases":{"hot":{"actions":{"rollover":{"max_age":"30d","max_size":"50gb"}}}}}}} as ILM is enabled.
2021-09-23T17:31:48.692+0900    INFO    template/load.go:229    Existing template will be overwritten, as overwrite is enabled.
2021-09-23T17:31:50.265+0900    INFO    template/load.go:132    Try loading template filebeat-7.15.0 to Elasticsearch
2021-09-23T17:31:50.465+0900    INFO    template/load.go:124    Template with name "filebeat-7.15.0" loaded.
2021-09-23T17:31:50.465+0900    INFO    [index-management]  idxmgmt/std.go:297  Loaded index template.
2021-09-23T17:31:50.467+0900    INFO    [index-management.ilm]  ilm/std.go:126  Index Alias filebeat-7.15.0 exists already.
Index setup finished.
Loading dashboards (Kibana must be running and reachable)
2021-09-23T17:31:50.467+0900    INFO    kibana/client.go:167    Kibana url: http://localhost:5601
2021-09-23T17:31:51.662+0900    INFO    [add_cloud_metadata]    add_cloud_metadata/add_cloud_metadata.go:101    add_cloud_metadata: hosting provider type not detected.
2021-09-23T17:31:52.564+0900    INFO    kibana/client.go:167    Kibana url: http://localhost:5601
2021-09-23T17:33:09.796+0900    INFO    instance/beat.go:848    Kibana dashboards successfully loaded.
Loaded dashboards
2021-09-23T17:33:09.796+0900    WARN    [cfgwarn]   instance/beat.go:574    DEPRECATED: Setting up ML using Filebeat is going to be removed. Please use the ML app to setup jobs. Will be removed in version: 8.0.0
Setting up ML using setup --machine-learning is going to be removed in 8.0.0. Please use the ML app instead.
See more: https://www.elastic.co/guide/en/machine-learning/current/index.html
2021-09-23T17:33:09.796+0900    INFO    [esclientleg]   eslegclient/connection.go:100   elasticsearch url: http://localhost:9200
2021-09-23T17:33:09.801+0900    INFO    [esclientleg]   eslegclient/connection.go:273   Attempting to connect to Elasticsearch version 7.15.0
2021-09-23T17:33:09.801+0900    INFO    kibana/client.go:167    Kibana url: http://localhost:5601
2021-09-23T17:33:09.830+0900    WARN    fileset/modules.go:425  X-Pack Machine Learning is not enabled
Loaded machine learning job configurations
2021-09-23T17:33:09.831+0900    INFO    [esclientleg]   eslegclient/connection.go:100   elasticsearch url: http://localhost:9200
2021-09-23T17:33:09.834+0900    INFO    [esclientleg]   eslegclient/connection.go:273   Attempting to connect to Elasticsearch version 7.15.0
2021-09-23T17:33:09.834+0900    INFO    cfgfile/reload.go:262   Loading of config files completed.
Loaded Ingest pipelines
[root@zabbixt01 filebeat]# 
Code Block 65 filebeat setup

실행(yum install)
[root@zabbixt01 filebeat]# systemctl start filebeat.service
[root@zabbixt01 filebeat]# systemctl status filebeat.service
● filebeat.service - Filebeat sends log files to Logstash or directly to Elasticsearch.
   Loaded: loaded (/usr/lib/systemd/system/filebeat.service; disabled; vendor preset: disabled)
   Active: active (running) since 목 2021-09-23 17:29:34 KST; 6s ago
     Docs: https://www.elastic.co/beats/filebeat
 Main PID: 9957 (filebeat)
   CGroup: /system.slice/filebeat.service
           └─9957 /usr/share/filebeat/bin/filebeat --environment systemd -c /etc/filebeat/filebeat.yml --path.home /usr/share/filebeat --path.config /etc/filebeat ...
 
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.523+0900        INFO        [esclientleg]        eslegclient/connection.go:273        Att...ion 7.15.0
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.542+0900        INFO        [index-management]        idxmgmt/std.go:261        Auto ILM ...e success.
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.544+0900        INFO        [index-management.ilm]        ilm/std.go:170        ILM polic...s already.
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.544+0900        INFO        [index-management]        idxmgmt/std.go:401        Set setup...s enabled.
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.544+0900        INFO        [index-management]        idxmgmt/std.go:406        Set setup...s enabled.
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.544+0900        INFO        [index-management]        idxmgmt/std.go:440        Set setti...s enabled.
 9월 23 17:29:38 zabbixt01 filebeat[9957]: 2021-09-23T17:29:38.544+0900        INFO        [index-management]        idxmgmt/std.go:444        Set setti...s enabled.
 9월 23 17:29:40 zabbixt01 filebeat[9957]: 2021-09-23T17:29:40.171+0900        INFO        template/load.go:132        Try loading template filebeat-7.1...sticsearch
 9월 23 17:29:40 zabbixt01 filebeat[9957]: 2021-09-23T17:29:40.405+0900        INFO        template/load.go:124        Template with name "filebeat-7.15.0" loaded.
 9월 23 17:29:40 zabbixt01 filebeat[9957]: 2021-09-23T17:29:40.405+0900        INFO        [index-management]        idxmgmt/std.go:297        Loaded index template.
Hint: Some lines were ellipsized, use -l to show in full.
[root@zabbixt01 filebeat]# 
Code Block 66 filebeat start

실행(tarball)
filebeat -d bin/logstash -f config/beat-pipelines.conf --config.reload.automatic --pipeline.unsafe_shutdown
filebeat start option
Option 	Description 
-E, --E setting=value	Configuration overwrite
-M, --M setting=value	Module configuration overwrite
-N, --N 	Disable actual publishing for testing
-c, --c string	Configuration file, relative to path.config (default "filebeat.yml")
--cpuprofile string	Write cpu profile to file
-d, --d string	Enable certain debug selectors
-e, --e	Log to stderr and disable syslog/file output
--environment environmentVar	set environment being ran in (default default)
-h, --help 	help for filebeat
--httpprof string	Start pprof http server
--memprofile string	Write memory profile to this file
--modules string	List of enabled modules (comma separated)
--once	Run filebeat only once until all harvesters reach EOF
--path.config string	Configuration path
--path.data string	Data path
--path.home string	Home path
--path.logs string	Logs path
--plugin pluginList	Load additional plugins
--strict.perms	Strict permission checking on config files (default true)
-v, --v	Log at INFO level
프로그램 종료

[root@zabbixt01 filebeat]# systemctl stop filebeat.service
[root@zabbixt01 filebeat]# systemctl status filebeat.service
● filebeat.service - Filebeat sends log files to Logstash or directly to Elasticsearch.
   Loaded: loaded (/usr/lib/systemd/system/filebeat.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://www.elastic.co/beats/filebeat
 
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.968+0900        INFO        [input.harvester]        log/harvester.go:336        Reader was closed. Closing.        {"input_id": "9b4c7561-eb15-4e9b-b793-524bcf247453", "source": "/var/log/elasticsearch/gc.log", "state_id": "native::8411534-2053",...
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.973+0900        INFO        beater/crawler.go:178        Crawler stopped
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.973+0900        INFO        [registrar]        registrar/registrar.go:132        Stopping Registrar
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.973+0900        INFO        [registrar]        registrar/registrar.go:166        Ending Registrar
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.974+0900        INFO        [registrar]        registrar/registrar.go:137        Registrar stopped
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.984+0900        INFO        [monitoring]        log/log.go:153        Total non-zero metrics        {"monitoring": {"metrics": {"beat":{"cpu":{"system":{"ticks":55990,"time":{"ms":55992}},"total":{"ticks":166310,"time":{"ms":166317},"value":166310...
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.984+0900        INFO        [monitoring]        log/log.go:154        Uptime: 138h47m59.879872929s
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.984+0900        INFO        [monitoring]        log/log.go:131        Stopping metrics logging.
 9월 23 10:08:44 zabbixt01 filebeat[23311]: 2021-09-23T10:08:44.995+0900        INFO        instance/beat.go:479        filebeat stopped.
 9월 23 10:08:45 zabbixt01 systemd[1]: Stopped Filebeat sends log files to Logstash or directly to Elasticsearch..
Hint: Some lines were ellipsized, use -l to show in full.
[root@zabbixt01 filebeat]# 
Code Block 67 filebeat stop

삭제(yum remove)

서비스 종료 후 수행해야 합니다.

[root@zabbixt01 7.15.0]# yum list | grep filebeat
 
filebeat.x86_64                         7.15.0-1                   installed    
[root@zabbixt01 7.15.0]# yum remove filebeat
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Resolving Dependencies
--> Running transaction check
---> Package filebeat.x86_64 0:7.15.0-1 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
======================================================================================================================================================================
 Package                                 Arch                                  Version                                 Repository                                Size
======================================================================================================================================================================
Removing:
 filebeat                                x86_64                                7.15.0-1                                installed                                136 M
 
Transaction Summary
======================================================================================================================================================================
Remove  1 Package
 
Installed size: 136 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Erasing    : filebeat-7.15.0-1.x86_64                                                                                                                           1/1 
  Verifying  : filebeat-7.15.0-1.x86_64                                                                                                                           1/1 
 
Removed:
  filebeat.x86_64 0:7.15.0-1                                                                                                                                          
 
Complete!
[root@zabbixt01 7.15.0]#
Code Block 68 filebeat remove

[Filebeat] 환경설정 방법
안내
해당 가이드는 Red Hat Enterprise Linux Server release 6.4 (Santiago) 기준으로 작성되었습니다. 설치 및 실행은 서비스(pg) 계정에서 수행하였습니다.

filebeat 수집 설정 방법
filebeat.yml 설정(전체 구성)
filebeat.inputs:
- type: log
  enabled: true
  encoding: euc-kr
  paths:
    - /data/tomcat_logs/ims/catalina.out.* 
  multiline.pattern: ^\[\d{4}-\d{2}-\d{2}\s\d{2}:\d{2}:\d{2}\]
  multiline.negate: true
  multiline.match: after
  tags : ["ims","catalina.out"]
- type: log
  enabled: false
  paths:
    - /data/tomcat_log/nicepay_nms/*.*
  multiline.pattern: ^\[\d{4}-\d{2}-\d{2}\s\d{2}:\d{2}:\d{2}\]
  multiline.negate: true
  multiline.match: after
  tags : ["mms","catalina.out"]
 
filebeat.config.modules:
  path: ${path.config}/modules.d/*.yml
  reload.enabled: false
 
output.logstash:
  hosts: ["172.32.161.35:5044"]
Code Block 69 beat-pipeline.conf

filebeat.inputs:
option#1	option#2	설명	예시
type: log		filebeat 에서 수집을 위한 선언
그 종류로는 log, filestream, stdin, redis, udp, tcp, syslog, container 가 있음	- type: log
	enabled	해당 수집 설정 사용 여부(true|false)	enabled: true
	encoding	수집되는 로그의 인코딩타입, logstash 는 UTF-8 로 수집되기 때문에 수집하려는 로그의 encoding 을 설정해야 convert 되어 수집 가능
http://www.w3.org/TR/encoding 내 인코딩 타입을사용 가능	encoding: euc-kr
	paths	수집하려는 metric의 위치. wild card 사용 가능	paths:
- /data/tomcat_logs/ims/catalina.out.*
	multiline	수집 metric 이 여러줄의 텍스트에 걸쳐 있는 경우, 하나의 시간으로 묶어 단일 이벤트로 처리하기 위한 옵션.
수집하려는 텍스트의 패턴, negative 및 매치 옵션을 통해 수집 방식을 결정함
세부옵션	설명	옵션
multiline.type	사용할 집계 방법을 정의
count 일 경우 일정한 수의 라인을 하나의 이벤트로 묶음	pattern|count
multiline.pattern	일치시킬 정규식 패턴을 지정	
multiline.negate	패턴이 부정되는지 여부를 정의	false|true
multiline.match	설정에 일치하는 줄을 하나의 이벤트로 결합할 때 해당 위치의 앞 또는 뒤에 연결하는 방법을 정의	after|before

negate	match	결과
false	after	패턴과 일치하는 연속행은 일치하지 않는 이전 행에 추가됨
false	before	패턴과 일치하는 연속행은 일치하지 않는 다음 행에 추가됨
true	after	패턴과 일치하지 않는 연속행은 일치하는 이전 행에 추가됨
true	before	패턴과 일치하지 않는 연속행은 일치하는 다음 행 앞에 추가됨
	multiline.pattern: ^\[\d{4}-\d{2}-\d{2}\s\d{2}:\d{2}:\d{2}\]
multiline.negate: true
multiline.match: after
	tags	수집된 로그에 tags 를 삽입 함. logstash 및 openseacrh 에서 tags 로 검색 가능	tags : ["ims","catalina.out"]
filebeat.config.modules:
option#1	option#2	설명	예시
path		filebeat 모듈 설정을 위한 모듈 path	path: ${path.config}/modules.d/*.yml
reload.enabled		모듈 변경 시 새로 읽음 옵션	reload.enabled: false
output.logstash:
option#1	option#2	설명	예시
hosts		logstash 의 접속 주소, IP:Port 형식으로 등록	hosts: ["172.32.161.35:5044"]
output.elasticsearch:
# ================================== Outputs ===================================
# ---------------------------- Elasticsearch Output ----------------------------
output.elasticsearch:                                     ## elasticsearch 사용시 앞에 주석(#) 제거
  # Array of hosts to connect to.
  hosts: ["localhost:9200"]                               ## elasticsearch 대상 서버IP, port
 
  # Protocol - either `http` (default) or `https`.
  #protocol: "https"
 
  # Authentication credentials - either API key or username/password.
  #api_key: "id:api_key"
  username: "elastic"                                    ## elasticsearch 접속계정
  password: "changeme"                                   ## elasticsearch 패스워드
 
# ------------------------------ Logstash Output -------------------------------
#output.logstash:                                         ## Logstach 사용시 앞에 주석(#) 제거
  # The Logstash hosts
  #hosts: ["localhost:5044"]                              ## Logstash 대상 서버IP, port
 
  # Optional SSL. By default is off.
  # List of root certificates for HTTPS server verifications
  #ssl.certificate_authorities: ["/etc/pki/root/ca.pem"]
 
  # Certificate for SSL client authentication
  #ssl.certificate: "/etc/pki/client/cert.pem"
 
  # Client Certificate Key
  #ssl.key: "/etc/pki/client/cert.key"
Code Block 70 filebeat config

OSS(Open Source Software) 기반 관제 시스템 구성도
사내 망 설치 기준 2021. 9. 28 
 
 
__temp
/**
 * InfluxdbPlugin.java
 * 
 * @version 1.0
 * 
 * @date 2021. 8. 2.
 * 
 *       copyright(c) 2021 www.nicepay.co.kr
 */
package scouter.plugin.server.influxdb;
 
import java.util.ArrayList;
import java.util.List;
 
import com.influxdb.client.InfluxDBClient;
import com.influxdb.client.InfluxDBClientFactory;
import com.influxdb.client.WriteApi;
import com.influxdb.client.write.Point;
 
import scouter.lang.pack.ObjectPack;
import scouter.lang.pack.Pack;
import scouter.lang.pack.PerfCounterPack;
import scouter.lang.pack.XLogPack;
import scouter.lang.plugin.PluginConstants;
import scouter.lang.plugin.annotation.ServerPlugin;
import scouter.server.Configure;
import scouter.server.Logger;
 
/**
 * <b>InfluxdbPlugin</b>
 * 
 * <pre>
 * InfluxDB2 에 scouter 의 성능카운터를 입력하는 플러그인
 * </pre>
 * <hr>
 *
 * @version 1.0 2021. 8. 2.
 * 
 * @author hsyou@nicepay.co.kr
 * 
 */
public class InfluxdbPlugin {
 
    Configure conf = Configure.getInstance();
 
    /**
     * InfluxDB 서버 접속정보
     */
    private static final String SERVER_URL = "ext_plugin_influxdb_server";
 
    /**
     * InfluxDB Token
     */
    private static final String TOKEN = "ext_plugin_influxdb_token";
 
    /**
     * InfluxDB bucket
     */
    private static final String BUCKET_NAME = "ext_plugin_influxdb_bucket";
 
    /**
     * InfluxDB organization
     */
    private static final String ORGANIZATION = "ext_plugin_influxdb_org";
 
    /**
     * {@link PluginConstants#PLUGIN_SERVER_COUNTER} 플러그인서버카운터
     */
    private static final String COUNTER_ENABLED = "ext_plugin_influxdb_counter_enabled";
 
    /**
     * {@link PluginConstants#PLUGIN_SERVER_OBJECT} 플러그인서버오브젝트
     */
    private static final String OBJECT_ENABLED = "ext_plugin_influxdb_object_enabled";
 
    /**
     * {@link PluginConstants#PLUGIN_SERVER_XLOG} 플러그인서버Xlog
     */
    private static final String XLOG_ENABLED = "ext_plugin_influxdb_xlog_enabled";
    
    /**
     * InfluxDB PLUGIN_SERVER_COUNTER measurement name
     */
    private static final String COUNTER_MEASUREMENT_NAME = "ext_plugin_influxdb_counter_measurement";
 
    /**
     * InfluxDB PLUGIN_SERVER_OBJECT measurement name
     */
    private static final String OBJECT_MEASUREMENT_NAME = "ext_plugin_influxdb_object_measurement";
    
    /**
     * InfluxDB PLUGIN_SERVER_XLOG measurement name
     */
    private static final String XLOG_MEASUREMENT_NAME = "ext_plugin_influxdb_xlog_measurement"; 
 
    /**
     * 예외처리 Object Name 이름 패턴
     */
    private static final String IGNORE_NAME_PATTERNS = "ext_plugin_influxdb_ignore_name_patterns";
 
    /**
     * debug mode value
     */
    private static final String DEBUG_VALUE = "ext_plugin_influxdb_debug";
 
    /**
     * <b> 기본 Constructor</b>
     * 
     */
    public InfluxdbPlugin() {
        super();
    }
 
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_COUNTER)
    public void counter(PerfCounterPack pack) {
        try {
            if (conf.getBoolean(COUNTER_ENABLED, true) && this.ignorePattern(pack.objName)) {
 
                Point point = this.packToPoint(conf.getValue(COUNTER_MEASUREMENT_NAME), pack);
                if (point != null) {
                    writeData(point);
                } else {
                    println("write data fail.");
                }
 
            }
        } catch (Exception e) {
            println(e.getMessage());
        }
 
    }
 
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_OBJECT)
    public void object(ObjectPack pack) {
        try {
            if (conf.getBoolean(OBJECT_ENABLED, true) && this.ignorePattern(pack.objName)) {
                Point point = this.packToPoint(conf.getValue(OBJECT_MEASUREMENT_NAME), pack);
                if (point != null) {
                    writeData(point);
                } else {
                    println("write data fail.");
                }
 
            }
        } catch (Exception e) {
            println(e.getMessage());
        }
    }
    
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_XLOG)
    public void xlog(XLogPack pack){
        try {
            if (conf.getBoolean(XLOG_ENABLED, true)) { //TODO ignore 패턴 수정
                Point point = this.packToPoint(conf.getValue(XLOG_MEASUREMENT_NAME), pack);
                if (point != null) {
                    writeData(point);
                } else {
                    println("write data fail.");
                }
 
            }
        } catch (Exception e) {
            println(e.getMessage());
        }
        
        /*
         * if(conf.getBoolean("ext_plugin_null_xlog_enabled", true)) {
         * println("[NullPlugin-xlog] " + pack);
         * }
         */
    }
    
    public void printAll(PerfCounterPack pPack, ObjectPack oPack, XLogPack xPack) {
        try {
            
            String objName2 = pPack.objName;            
            
            int objHash2 = oPack.objHash;
            String objName = oPack.objName;
            String objType = oPack.objType;
            String address = oPack.address;
            boolean alive = oPack.alive;
            
            int objHash = xPack.objHash;
            int service = xPack.service;
            long txid = xPack.txid;
            long caller = xPack.caller;
            long gxid = xPack.gxid;
            int elapsed = xPack.elapsed;
            int error = xPack.error;
 
 
            //return Point.measurement(measurementName).addField("objHash", oPack.objHash).addTag("objName", oPack.objName)=.addTag("objType", oPack.objType).addTag("address", oPack.address).addField("alive", oPack.alive);
            
        } catch (Exception e) {
            // TODO: handle exception
        }
    }
    
 
    /**
     * 
     * <b class="comment_method">packToPoint</b><br/>
     * 
     * <pre>
     * {@link Pack} 을 {@link Point} 로 변환
     * </pre>
     * <hr>
     * 
     * @param measurementName influxDB 에 저장할 measurement 이름
     * @param pack 현재 {@link PerfCounterPack} 과 {@link ObjectPack} 만 지원
     * @return {@link Point}
     * @throws Exception
     */
    private Point packToPoint(String measurementName, Pack pack) throws Exception {
 
        try {
            if (pack instanceof PerfCounterPack) {
                PerfCounterPack pPack = (PerfCounterPack) pack;
 
                return Point.measurement(measurementName).addTag("objName", pPack.objName)
                        .addField("Cpu", pPack.data.getFloat("Cpu"))
                        .addField("SysCpu", pPack.data.getFloat("SysCpu"))
                        .addField("UserCpu", pPack.data.getFloat("UserCpu"))
                        .addField("Mem", pPack.data.getFloat("Mem"))
                        .addField("MemA", pPack.data.getFloat("MemA"))
                        .addField("MemU", pPack.data.getFloat("MemU"))
                        .addField("MemT", pPack.data.getFloat("MemT"))
                        .addField("PageIn", pPack.data.getFloat("PageIn"))
                        .addField("PageOut", pPack.data.getFloat("PageOut"))
                        .addField("Swap", pPack.data.getFloat("Swap"))
                        .addField("SwapT", pPack.data.getFloat("SwapT"))
                        .addField("SwapU", pPack.data.getFloat("SwapU"))
                        .addField("NetInBound", pPack.data.getFloat("NetInBound"))
                        .addField("NetOutBound", pPack.data.getFloat("NetOutBound"))
                        .addField("TcpStatCLS", pPack.data.getFloat("TcpStatCLS"))
                        .addField("TcpStatTIM", pPack.data.getFloat("TcpStatTIM"))
                        .addField("TcpStatFIN", pPack.data.getFloat("TcpStatFIN"))
                        .addField("TcpStatEST", pPack.data.getFloat("TcpStatEST"))
                        .addField("NetRxBytes", pPack.data.getFloat("NetRxBytes"))
                        .addField("NetTxBytes", pPack.data.getFloat("NetTxBytes"))
                        .addField("DiskReadBytes", pPack.data.getFloat("DiskReadBytes"))
                        .addField("DiskWriteBytes", pPack.data.getFloat("DiskWriteBytes"))
                        .addField("RecentUser", pPack.data.getFloat("RecentUser"))
                        .addField("HeapTotUsage", pPack.data.getFloat("HeapTotUsage"))
                        .addField("GcCount", pPack.data.getFloat("GcCount"))
                        .addField("ServiceCount", pPack.data.getFloat("ServiceCount"))
                        .addField("ErrorRate", pPack.data.getFloat("ErrorRate"))
                        .addField("HeapUsed", pPack.data.getFloat("HeapUsed"))
                        .addField("HeapTotal", pPack.data.getFloat("HeapTotal"))
                        .addField("ElapsedTime", pPack.data.getFloat("ElapsedTime"))
                        .addField("SqlTimeByService", pPack.data.getFloat("SqlTimeByService"))
                        .addField("ApiTimeByService", pPack.data.getFloat("ApiTimeByService"))
                        .addField("QueuingTime", pPack.data.getFloat("QueuingTime"))
                        .addField("ActiveService", pPack.data.getFloat("ActiveService"))
                        .addField("GcTime", pPack.data.getFloat("GcTime"))
                        .addField("TPS", pPack.data.getFloat("TPS"))
                        .addField("ProcCpu", pPack.data.getFloat("ProcCpu"))
                        .addField("PermUsed", pPack.data.getFloat("PermUsed"))
                        .addField("PermPercent", pPack.data.getFloat("PermPercent"))
                        .addField("FdUsage", pPack.data.getFloat("FdUsage"));
 
            } else if (pack instanceof ObjectPack) {
                ObjectPack oPack = (ObjectPack) pack;
 
                return Point.measurement(measurementName).addTag("objHash", Integer.toString(oPack.objHash)).addTag("objName", oPack.objName)
                        .addTag("objType", oPack.objType).addTag("address", oPack.address).addField("alive", oPack.alive);
            } else if (pack instanceof XLogPack) {
                XLogPack xPack = (XLogPack) pack;
                
                println("xlog:" + xPack.toString());
 
                return Point.measurement(measurementName).addTag("objHash", Integer.toString(xPack.objHash)).addField("service", xPack.service).addField("txid", xPack.txid)
                        .addField("caller", xPack.caller).addField("gxid", xPack.gxid).addField("elapsed", xPack.elapsed).addField("error", xPack.error);
 
                /*
                 * return Point.measurement(measurementName).addField("objHash", oPack.objHash).addTag("objName", oPack.objName)
                 * .addTag("objType", oPack.objType).addTag("address", oPack.address).addField("alive", oPack.alive);
                 */
            } else {
                println("Unsupported Pack : " + pack.getPackType());
                return null;
            }
        } catch (Exception e) {
            throw e;
        }
 
    }
 
    /**
     * 
     * <b class="comment_method">writeData</b><br/>
     * 
     * <pre>
     * InfluxDB 에 데이터 입력(Using {@link Point})
     * </pre>
     * <hr>
     * 
     * @param point {@link Point} Object
     * @throws Exception
     */
    private void writeData(Point point) throws Exception {
        try {
 
            String serverUrl = conf.getValue(SERVER_URL);
            String token = conf.getValue(TOKEN);
            String bucket = conf.getValue(BUCKET_NAME);
            String org = conf.getValue(ORGANIZATION);
 
            InfluxDBClient client = InfluxDBClientFactory.create(serverUrl, token.toCharArray());
 
            WriteApi writeApi = client.getWriteApi();
            writeApi.writePoint(bucket, org, point);
        } catch (Exception e) {
            throw e;
        }
    }
 
    /**
     * 
     * <b class="comment_method">ignorePattern</b><br/>
     * 
     * <pre>
     * 설정된 이름을 예외처리
     * </pre>
     * <hr>
     * 
     * @param objectName
     * @return
     */
    private boolean ignorePattern(String objectName) {
        boolean isIgnore = true;
 
        try {
 
            String ignoreNamePattern = conf.getValue(IGNORE_NAME_PATTERNS);
 
            if (ignoreNamePattern != null && !"".equals(ignoreNamePattern)) {
                for (String pattern : ignoreNamePattern.split(",")) {
                    if (objectName.matches(pattern.replaceAll("\\*", ".*"))) {
                        isIgnore = false;
                    }
                }
            }
 
        } catch (Exception e) {
            // ignore
            println("[Error] : " + e.getMessage());
        }
 
        return isIgnore;
    }
 
    /**
     * 
     * <b class="comment_method">println</b><br/>
     * 
     * <pre>
     * Logger Print
     * </pre>
     * <hr>
     * 
     * @param o
     */
    private void println(Object o) {
        if (conf.getBoolean(DEBUG_VALUE, false)) {
            Logger.println(o);
        }
    }
 
}
Code Block 71 InfluxdbPlugin

/*
 *  Copyright 2016 Scouter Project.
 *
 *  Licensed under the Apache License, Version 2.0 (the "License"); 
 *  you may not use this file except in compliance with the License.
 *  You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 *  Unless required by applicable law or agreed to in writing, software
 *  distributed under the License is distributed on an "AS IS" BASIS,
 *  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 *  See the License for the specific language governing permissions and
 *  limitations under the License. 
 *  
 *  @author Sang-Cheon Park
 */
package scouter.plugin.server.alert.telegram;
 
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.atomic.AtomicInteger;
 
import org.apache.commons.codec.Charsets;
import org.apache.http.HttpResponse;
import org.apache.http.HttpStatus;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;
 
import com.google.gson.Gson;
 
import scouter.lang.AlertLevel;
import scouter.lang.TextTypes;
import scouter.lang.TimeTypeEnum;
import scouter.lang.counters.CounterConstants;
import scouter.lang.pack.AlertPack;
import scouter.lang.pack.MapPack;
import scouter.lang.pack.ObjectPack;
import scouter.lang.pack.PerfCounterPack;
import scouter.lang.pack.XLogPack;
import scouter.lang.plugin.PluginConstants;
import scouter.lang.plugin.annotation.ServerPlugin;
import scouter.net.RequestCmd;
import scouter.server.Configure;
import scouter.server.CounterManager;
import scouter.server.Logger;
import scouter.server.core.AgentManager;
import scouter.server.db.TextRD;
import scouter.server.netio.AgentCall;
import scouter.util.DateUtil;
import scouter.util.HashUtil;
 
/**
 * Scouter server plugin to send alert via telegram
 * 
 * @author Sang-Cheon Park(nices96@gmail.com) on 2016. 3. 28.
 */
public class TelegramPlugin {
 
    // Get singleton Configure instance from server
    final Configure conf = Configure.getInstance();
 
    private static AtomicInteger ai = new AtomicInteger(0);
    private static List<Integer> javaeeObjHashList = new ArrayList<Integer>();
    private static AlertPack lastPack;
    private static long lastSentTimestamp;
 
    public TelegramPlugin() {
        if (ai.incrementAndGet() == 1) {
            ScheduledExecutorService executor = Executors.newScheduledThreadPool(1);
 
            // thread count check
            executor.scheduleAtFixedRate(new Runnable() {
                @Override
                public void run() {
                    for (int objHash : javaeeObjHashList) {
                        try {
                            if (AgentManager.isActive(objHash)) {
                                ObjectPack objectPack = AgentManager.getAgent(objHash);
                                MapPack mapPack = new MapPack();
                                mapPack.put("objHash", objHash);
 
                                mapPack = AgentCall.call(objectPack, RequestCmd.OBJECT_THREAD_LIST, mapPack);
 
                                int threadCountThreshold = conf.getInt("ext_plugin_thread_count_threshold", 0);
                                int threadCount = mapPack.getList("name").size();
 
                                if (threadCountThreshold != 0 && threadCount > threadCountThreshold) {
                                    AlertPack ap = new AlertPack();
 
                                    ap.level = AlertLevel.WARN;
                                    ap.objHash = objHash;
                                    ap.title = "Thread count exceed a threshold.";
                                    ap.message = objectPack.objName + "'s Thread count(" + threadCount + ") exceed a threshold.";
                                    ap.time = System.currentTimeMillis();
                                    ap.objType = objectPack.objType;
 
                                    alert(ap);
                                }
                            }
                        } catch (Exception e) {
                            // ignore
                        }
                    }
                }
            }, 0, 5, TimeUnit.SECONDS);
        }
    }
 
    /**
     * 
     * <b class="comment_method">alert</b><br/>
     * <pre>
     * Plugin Server Alert 및 telegram 발송 부분
     * 
     * 2021.07.26 hsyou alert 주기를 설정할 수 있도록 ext_plugin_ignore_continuous_dup_alert_time 추가 구현
     * 2021.07.26 hsyou telegram 한글 발송하도록 수정
     * 2021.07.26 hsyou type 제외, html 사용 가능하도록 수정
     * </pre>
     * <hr>
     * @param pack
     */
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_ALERT)
    public void alert(final AlertPack pack) {
        if (conf.getBoolean("ext_plugin_telegram_send_alert", false)) {
 
            // Get log level (0 : INFO, 1 : WARN, 2 : ERROR, 3 : FATAL)
            int level = conf.getInt("ext_plugin_telegram_level", 0);
 
            if (level <= pack.level) {
                new Thread() {
                    public void run() {
                        try {
                            // Get server configurations for telegram
                            String token = conf.getValue("ext_plugin_telegram_bot_token");
                            String chatId = conf.getValue("ext_plugin_telegram_chat_id");
 
                            assert token != null;
                            assert chatId != null;
 
                            // Make a request URL using telegram bot api
                            String url = "https://api.telegram.org/bot" + token + "/sendMessage";
 
                            // Get the agent Name
                            String name = AgentManager.getAgentName(pack.objHash) == null ? "N/A" : AgentManager.getAgentName(pack.objHash);
 
                            if (name.equals("N/A") && pack.message.endsWith("connected.")) {
                                int idx = pack.message.indexOf("connected");
                                if (pack.message.indexOf("reconnected") > -1) {
                                    name = pack.message.substring(0, idx - 6);
                                } else {
                                    name = pack.message.substring(0, idx - 4);
                                }
                            }
 
                            String title = pack.title;
                            String msg = pack.message;
                            if (title.equals("INACTIVE_OBJECT")) {
                                title = "해당 object 가 inactive 상태입니다. 재기동 여부 체크 바랍니다.";
                                msg = pack.message.substring(0, pack.message.indexOf("OBJECT") - 1);
                            }
 
                            try {
                                String ignoreNamePattern = conf.getValue("ext_plugin_ignore_name_patterns");
                                String ignoreTitlePattern = conf.getValue("ext_plugin_ignore_title_patterns");
                                String ignoreMessagePattern = conf.getValue("ext_plugin_ignore_message_patterns");
 
                                if (ignoreNamePattern != null && !"".equals(ignoreNamePattern)) {
                                    for (String pattern : ignoreNamePattern.split(",")) {
                                        if (name.matches(pattern.replaceAll("\\*", ".*"))) {
                                            return;
                                        }
                                    }
                                }
 
                                if (ignoreTitlePattern != null && !"".equals(ignoreTitlePattern)) {
                                    for (String pattern : ignoreTitlePattern.split(",")) {
                                        if (title.matches(pattern.replaceAll("\\*", ".*"))) {
                                            return;
                                        }
                                    }
                                }
 
                                if (ignoreMessagePattern != null && !"".equals(ignoreMessagePattern)) {
                                    for (String pattern : ignoreMessagePattern.split(",")) {
                                        if (msg.matches(pattern.replaceAll("\\*", ".*")
                                                .replaceAll("\\(", "\\\\(").replaceAll("\\)", "\\\\)")
                                                .replaceAll("\\[", "\\\\[").replaceAll("\\]", "\\\\]"))) {
                                            return;
                                        }
                                    }
                                }
 
                                /** alert 주기를 설정할 수 있도록 ext_plugin_ignore_continuous_dup_alert_time 추가 구현 */
                                if (conf.getBoolean("ext_plugin_ignore_continuous_dup_alert", false) && lastPack != null) {
                                    long diff = System.currentTimeMillis() - lastSentTimestamp;
                                    
                                      long alertTime = conf.getLong("ext_plugin_ignore_continuous_dup_alert_time", DateUtil.MILLIS_PER_HOUR);
                                      
                                      if (lastPack.objHash == pack.objHash && lastPack.title.equals(pack.title) && diff < alertTime) {
                                          return;
                                      }
                                }
 
                                lastPack = pack;
                            } catch (Exception e) {
                                // ignore
                                println("[Error] : " + e.getMessage());
                            }
 
                            // Make message contents
                            title = "<b>" + title + "</b>";
                            String contents =   title + "\n\n" +
                            /** 주석 처리
                                                "[타입    ] : " + pack.objType.toUpperCase() + "\n" + 
                            */
                                                "[Target     ] : " + name+ "\n" + 
                                                "[Alert Level] : " + AlertLevel.getName(pack.level) + "\n" + 
                                                "[메시지  ] : " + msg;
 
                            Message message = new Message(chatId, contents);
                            String param = new Gson().toJson(message);
 
                            url = url+"?parse_mode=html";
                            HttpPost post = new HttpPost(url);
                            post.addHeader("Content-Type", "application/json; charset=utf-8");
                            post.setEntity(new StringEntity(param, Charsets.UTF_8));
 
                            CloseableHttpClient client = HttpClientBuilder.create().build();
 
                            // send the post request
                            HttpResponse response = client.execute(post);
 
                            if (response.getStatusLine().getStatusCode() == HttpStatus.SC_OK) {
                                lastSentTimestamp = System.currentTimeMillis();
                                println("Telegram message sent to [" + chatId + "] successfully.");
                            } else {
                                println("Telegram message sent failed. Verify below information.");
                                println("[URL] : " + url);
                                println("[Message] : " + param);
                                println("[Reason] : " + EntityUtils.toString(response.getEntity(), "UTF-8"));
                            }
                        } catch (Exception e) {
                            println("[Error] : " + e.getMessage());
 
                            if (conf._trace) {
                                e.printStackTrace();
                            }
                        }
                    }
                }.start();
            }
        }
    }
 
    /**
     * 
     * <b class="comment_method">object</b><br/>
     * <pre>
     * Object 관련 설정
     * 
     * 2021.07.26 hsyou 일부 메시지 한글화
     * </pre>
     * <hr>
     * @param pack
     */
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_OBJECT)
    public void object(ObjectPack pack) {
        if (pack.version != null && pack.version.length() > 0) {
            AlertPack ap = null;
            ObjectPack op = AgentManager.getAgent(pack.objHash);
 
            if (op == null && pack.wakeup == 0L) {
                // in case of new agent connected
                ap = new AlertPack();
                ap.level = AlertLevel.INFO;
                ap.objHash = pack.objHash;
                ap.title = "해당 object 가 활성화 되었습니다.";
                ap.message = pack.objName + " 이(가) Scouter 와 연결 되었습니다.";
                ap.time = System.currentTimeMillis();
 
                if (AgentManager.getAgent(pack.objHash) != null) {
                    ap.objType = AgentManager.getAgent(pack.objHash).objType;
                } else {
                    ap.objType = "scouter";
                }
 
                alert(ap);
            } else if (op.alive == false) {
                // in case of agent reconnected
                ap = new AlertPack();
                ap.level = AlertLevel.INFO;
                ap.objHash = pack.objHash;
                ap.title = "해당 object 가 활성화 되었습니다.";
                ap.message = pack.objName + " 이(가) Scouter 와 다시 연결 되었습니다.";
                ap.time = System.currentTimeMillis();
                ap.objType = AgentManager.getAgent(pack.objHash).objType;
 
                alert(ap);
            }
            // inactive state can be handled in alert() method.
        }
    }
 
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_XLOG)
    public void xlog(XLogPack pack) {
        try {
            int elapsedThreshold = conf.getInt("ext_plugin_elapsed_time_threshold", 0);
 
            if (elapsedThreshold != 0 && pack.elapsed > elapsedThreshold) {
                String serviceName = TextRD.getString(DateUtil.yyyymmdd(pack.endTime), TextTypes.SERVICE, pack.service);
 
                AlertPack ap = new AlertPack();
 
                ap.level = AlertLevel.WARN;
                ap.objHash = pack.objHash;
                ap.title = "Elapsed time exceed a threshold.";
                ap.message = "[" + AgentManager.getAgentName(pack.objHash) + "] " 
                                    + pack.service + "(" + serviceName + ") " 
                                    + "elapsed time(" + pack.elapsed + " ms) exceed a threshold.";
                ap.time = System.currentTimeMillis();
                ap.objType = AgentManager.getAgent(pack.objHash).objType;
 
                alert(ap);
            }
        } catch (Exception e) {
            Logger.printStackTrace(e);
        }
    }
 
    @ServerPlugin(PluginConstants.PLUGIN_SERVER_COUNTER)
    public void counter(PerfCounterPack pack) {
        String objName = pack.objName;
        int objHash = HashUtil.hash(objName);
        String objType = null;
        String objFamily = null;
 
        if (AgentManager.getAgent(objHash) != null) {
            objType = AgentManager.getAgent(objHash).objType;
        }
 
        if (objType != null) {
            objFamily = CounterManager.getInstance().getCounterEngine().getObjectType(objType).getFamily().getName();
        }
 
        try {
            // in case of objFamily is javaee
            if (CounterConstants.FAMILY_JAVAEE.equals(objFamily)) {
                // save javaee type's objHash
                if (!javaeeObjHashList.contains(objHash)) {
                    javaeeObjHashList.add(objHash);
                }
 
                if (pack.timetype == TimeTypeEnum.REALTIME) {
                    long gcTimeThreshold = conf.getLong("ext_plugin_gc_time_threshold", 0);
                    long gcTime = pack.data.getLong(CounterConstants.JAVA_GC_TIME);
 
                    if (gcTimeThreshold != 0 && gcTime > gcTimeThreshold) {
                        AlertPack ap = new AlertPack();
 
                        ap.level = AlertLevel.WARN;
                        ap.objHash = objHash;
                        ap.title = "GC time exceed a threshold.";
                        ap.message = objName + "'s GC time(" + gcTime + " ms) exceed a threshold.";
                        ap.time = System.currentTimeMillis();
                        ap.objType = objType;
 
                        alert(ap);
                    }
                    
                    /** Active Servoce Count 설정하기 */
/*                    long activeServiceCount = conf.getLong("ext_plugin_active_service_count", 0);
                    long activeService = pack.data.getLong(CounterConstants.WAS_ACTIVE_SERVICE);
                    
                    if (activeServiceCount != 0 && activeService > activeServiceCount) {
                        AlertPack ap2 = new AlertPack();
                        
                        ap2.level = AlertLevel.WARN;
                        ap2.objHash = objHash;
                        ap2.title = "Active Service EQ is Over.";
                        ap2.message = objName + "'s Active Service Count : " + pack.data.getInt(CounterConstants.WAS_ACTIVE_SERVICE);
                        ap2.time = System.currentTimeMillis();
                        ap2.objType = objType;
                        
                        alert(ap2);
                    }
*/
                }
            }
        } catch (Exception e) {
            Logger.printStackTrace(e);
        }
    }
 
    private void println(Object o) {
        if (conf.getBoolean("ext_plugin_telegram_debug", false)) {
            Logger.println(o);
        }
    }
}
Code Block 72 TelegramPlugin.java



prometheus :https://codewizardly.com/prometheus-on-aws-ec2-part1/ 






 
### security.showInsecureClusterWarning: false



 
Maven dependencies download
개요
maven 의존성 라이브러리를 한번에 받을 수 있는 pom.xml 파일
사용방법
PC 에 maven 설치 후 아래 pom.xml 파일 위치에서 mvn install 실행

<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>jar.download</groupId>
    <artifactId>jar.down</artifactId>
    <version>1.0</version>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <dependencies>
 
<!-- 필요로 하는 maven 라이브러리 등록-시작 -->
    <dependency>
        <groupId>com.influxdb</groupId>
        <artifactId>influxdb-client-java</artifactId>
        <version>3.1.0</version>
    </dependency>
<!-- 필요로 하는 maven 라이브러리 등록-끝 -->
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <version>2.8</version>
                <executions>
                    <execution>
                        <id>download-dependencies</id>
                        <phase>generate-resources</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <outputDirectory> ${project.build.directory}/dependencies </outputDirectory>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
Code Block 73 pom.xml

Container : docker
[docker] 디스크 볼륨 관리
prune 명령어를 통한 볼륨 관리
이름없는 모든 이미지 삭제
docker image prune -a
[root@almt01 containers]# docker image prune -a
WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
Total reclaimed space: 0B
Code Block 74 docker image prune -a


실행 중지된 컨테이너, 사용하지 않는 네트워크, 사용하지 않는 레이어를 모두 삭제
docker system prune -a
[root@almt01 overlay2]# df -h | grep var | grep /dev/
/dev/sda5        15G   15G   20K 100% /var
[root@almt01 containers]# docker system prune -a
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all images without at least one container associated to them
  - all build cache
 
Are you sure you want to continue? [y/N] y
Deleted Images:
deleted: sha256:17d5117a2e3715b4632b30df670f1768082a5d0c9a578112cf468c346eceb481
deleted: sha256:00953f7a61a51b59f4ac00f37277087e2fcacba4213fbd025c530e337f3013fa
deleted: sha256:9cc51fb244651cf1108aaec0da191eb27e049750a758af8ea11c1d9d21ef6b61
deleted: sha256:558c4364ec91e5fb21d3f28005bfc8ee1fca9d63255151cdfd1b15f33a324250
deleted: sha256:165e5cf07f7838560dced7bf9b5c87b666fb6f9f6f061e231032a16a8207ec89
deleted: sha256:bd85c337734a034314ee81a3dc5fefaa3934b7b06a929b95799a2b680fdb4911
deleted: sha256:268dc5da8cab3074992cbcdda5fe8fb4e26086454954526e0eae44fd327b3ec2
deleted: sha256:e6fa212a7165a143d61823d67be268e19c7745a9c168756b71a0791831ebcc16
deleted: sha256:6f3c18e03a8828f895bc8e7fc1df5b7a6c199160370f29c7272c7ed5bcedb2ce
deleted: sha256:281e4ad18351d1556bd4764e674986d15572b52ec96137d7417fd4cc071c12ab
deleted: sha256:a0c1e01578b7e57d891b82a53a9debdb52dc642c581de3e9231d395989d39a03
 
Total reclaimed space: 1.761GB
[root@almt01 overlay2]# df -h | grep var | grep /dev/
/dev/sda5        15G   14G  1.9G  88% /var
Code Block 75 docker system prune -a

[docker] 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
rpm 다운로드(bastion 서버 활용)
bastion 서버 에 docker repo 정보 등록(centOS 7, RHEL 7 적용 가능)
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
Code Block 76 batstion : docker repo add

대상 docker 버전 확인
https://download.docker.com/linux/centos/7/x86_64/stable/Packages/ 에서 docker 의 버전 확인

 

의존성 rpm 다운로드
yum install -y docker-ce-20.10.11-3.el7 docker-ce-cli-20.10.11-3.el7 containerd.io container-selinux --downloadonly --downloaddir=$download_path
Code Block 77 batstion : docker rpm download

rpm 이동(설치 대상 서버 이동)
download_path 의 파일을 설치 대상 서버로 이동
파일명	비고
container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm	
containerd.io-1.4.12-3.1.el7.x86_64.rpm	
docker-ce-20.10.11-3.el7.x86_64.rpm	docker core
docker-ce-cli-20.10.11-3.el7.x86_64.rpm	docker cli 용 추가 설치파일
docker-ce-rootless-extras-20.10.11-3.el7.x86_64.rpm	rootless 기능용 패키지
docker-scan-plugin-0.9.0-3.el7.x86_64.rpm	docker-ce-cli 의존성 패키지
fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm	docker-ce 의존성 패키지
fuse3-libs-3.6.1-4.el7.x86_64.rpm	docker-ce 의존성 패키지
slirp4netns-0.4.3-4.el7_8.x86_64.rpm	docker-ce 의존성 패키지
프로그램 설치 및 최초 실행
설치
 [root@almt01 docker-rhel]# yum install policycoreutils-python.x86_64 libseccomp.x86_64 fuse3-libs-3.6.1-4.el7.x86_64.rpm
 fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm slirp4netns-0.4.3-4.el7_8.x86_64.rpm container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm
 docker-scan-plugin-0.9.0-3.el7.x86_64.rpm docker-ce-cli-20.10.11-3.el7.x86_64.rpm containerd.io-1.4.12-3.1.el7.x86_64.rpm
 docker-ce-rootless-extras-20.10.11-3.el7.x86_64.rpm docker-ce-20.10.11-3.el7.x86_64.rpm
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Examining fuse3-libs-3.6.1-4.el7.x86_64.rpm: fuse3-libs-3.6.1-4.el7.x86_64
Marking fuse3-libs-3.6.1-4.el7.x86_64.rpm to be installed
Examining fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm: fuse-overlayfs-0.7.2-6.el7_8.x86_64
Marking fuse-overlayfs-0.7.2-6.el7_8.x86_64.rpm to be installed
Examining slirp4netns-0.4.3-4.el7_8.x86_64.rpm: slirp4netns-0.4.3-4.el7_8.x86_64
Marking slirp4netns-0.4.3-4.el7_8.x86_64.rpm to be installed
Examining container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm: 2:container-selinux-2.119.2-1.911c772.el7_8.noarch
Marking container-selinux-2.119.2-1.911c772.el7_8.noarch.rpm to be installed
Examining docker-scan-plugin-0.9.0-3.el7.x86_64.rpm: docker-scan-plugin-0.9.0-3.el7.x86_64
Marking docker-scan-plugin-0.9.0-3.el7.x86_64.rpm to be installed
Examining docker-ce-cli-20.10.11-3.el7.x86_64.rpm: 1:docker-ce-cli-20.10.11-3.el7.x86_64
Marking docker-ce-cli-20.10.11-3.el7.x86_64.rpm to be installed
Examining containerd.io-1.4.12-3.1.el7.x86_64.rpm: containerd.io-1.4.12-3.1.el7.x86_64
Marking containerd.io-1.4.12-3.1.el7.x86_64.rpm to be installed
Examining docker-ce-rootless-extras-20.10.11-3.el7.x86_64.rpm: docker-ce-rootless-extras-20.10.11-3.el7.x86_64
Marking docker-ce-rootless-extras-20.10.11-3.el7.x86_64.rpm to be installed
Examining docker-ce-20.10.11-3.el7.x86_64.rpm: 3:docker-ce-20.10.11-3.el7.x86_64
Marking docker-ce-20.10.11-3.el7.x86_64.rpm to be installed
Resolving Dependencies
--> Running transaction check
---> Package container-selinux.noarch 2:2.119.2-1.911c772.el7_8 will be installed
---> Package containerd.io.x86_64 0:1.4.12-3.1.el7 will be installed
---> Package docker-ce.x86_64 3:20.10.11-3.el7 will be installed
---> Package docker-ce-cli.x86_64 1:20.10.11-3.el7 will be installed
---> Package docker-ce-rootless-extras.x86_64 0:20.10.11-3.el7 will be installed
---> Package docker-scan-plugin.x86_64 0:0.9.0-3.el7 will be installed
---> Package fuse-overlayfs.x86_64 0:0.7.2-6.el7_8 will be installed
---> Package fuse3-libs.x86_64 0:3.6.1-4.el7 will be installed
---> Package libseccomp.x86_64 0:2.3.1-3.el7 will be installed
---> Package policycoreutils-python.x86_64 0:2.5-29.el7 will be installed
---> Package slirp4netns.x86_64 0:0.4.3-4.el7_8 will be installed
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================
 Package                            Arch            Version                               Repository                                                  Size
===========================================================================================================================================================
Installing:
 container-selinux                  noarch          2:2.119.2-1.911c772.el7_8             /container-selinux-2.119.2-1.911c772.el7_8.noarch           41 k
 containerd.io                      x86_64          1.4.12-3.1.el7                        /containerd.io-1.4.12-3.1.el7.x86_64                       108 M
 docker-ce                          x86_64          3:20.10.11-3.el7                      /docker-ce-20.10.11-3.el7.x86_64                            96 M
 docker-ce-cli                      x86_64          1:20.10.11-3.el7                      /docker-ce-cli-20.10.11-3.el7.x86_64                       139 M
 docker-ce-rootless-extras          x86_64          20.10.11-3.el7                        /docker-ce-rootless-extras-20.10.11-3.el7.x86_64            20 M
 docker-scan-plugin                 x86_64          0.9.0-3.el7                           /docker-scan-plugin-0.9.0-3.el7.x86_64                      13 M
 fuse-overlayfs                     x86_64          0.7.2-6.el7_8                         /fuse-overlayfs-0.7.2-6.el7_8.x86_64                       116 k
 fuse3-libs                         x86_64          3.6.1-4.el7                           /fuse3-libs-3.6.1-4.el7.x86_64                             270 k
 libseccomp                         x86_64          2.3.1-3.el7                           local-repo                                                  56 k
 policycoreutils-python             x86_64          2.5-29.el7                            local-repo                                                 456 k
 slirp4netns                        x86_64          0.4.3-4.el7_8                         /slirp4netns-0.4.3-4.el7_8.x86_64                          169 k
 
Transaction Summary
===========================================================================================================================================================
Install  11 Packages
 
Total size: 377 M
Total download size: 511 k
Installed size: 378 M
Is this ok [y/d/N]: y
Downloading packages:
-----------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                      141 MB/s | 511 kB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : libseccomp-2.3.1-3.el7.x86_64                                                                                                          1/11 
  Installing : docker-scan-plugin-0.9.0-3.el7.x86_64                                                                                                  2/11 
  Installing : 1:docker-ce-cli-20.10.11-3.el7.x86_64                                                                                                  3/11 
  Installing : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                       4/11 
  Installing : policycoreutils-python-2.5-29.el7.x86_64                                                                                               5/11 
  Installing : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                     6/11 
setsebool:  SELinux is disabled.
  Installing : containerd.io-1.4.12-3.1.el7.x86_64                                                                                                    7/11 
  Installing : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                          8/11 
  Installing : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                    9/11 
  Installing : docker-ce-rootless-extras-20.10.11-3.el7.x86_64                                                                                       10/11 
  Installing : 3:docker-ce-20.10.11-3.el7.x86_64                                                                                                     11/11 
  Verifying  : 1:docker-ce-cli-20.10.11-3.el7.x86_64                                                                                                  1/11 
  Verifying  : docker-scan-plugin-0.9.0-3.el7.x86_64                                                                                                  2/11 
  Verifying  : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                          3/11 
  Verifying  : 3:docker-ce-20.10.11-3.el7.x86_64                                                                                                      4/11 
  Verifying  : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                    5/11 
  Verifying  : policycoreutils-python-2.5-29.el7.x86_64                                                                                               6/11 
  Verifying  : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                       7/11 
  Verifying  : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                     8/11 
  Verifying  : libseccomp-2.3.1-3.el7.x86_64                                                                                                          9/11 
  Verifying  : docker-ce-rootless-extras-20.10.11-3.el7.x86_64                                                                                       10/11 
  Verifying  : containerd.io-1.4.12-3.1.el7.x86_64                                                                                                   11/11 
 
Installed:
  container-selinux.noarch 2:2.119.2-1.911c772.el7_8     containerd.io.x86_64 0:1.4.12-3.1.el7                 docker-ce.x86_64 3:20.10.11-3.el7          
  docker-ce-cli.x86_64 1:20.10.11-3.el7                  docker-ce-rootless-extras.x86_64 0:20.10.11-3.el7     docker-scan-plugin.x86_64 0:0.9.0-3.el7    
  fuse-overlayfs.x86_64 0:0.7.2-6.el7_8                  fuse3-libs.x86_64 0:3.6.1-4.el7                       libseccomp.x86_64 0:2.3.1-3.el7            
  policycoreutils-python.x86_64 0:2.5-29.el7             slirp4netns.x86_64 0:0.4.3-4.el7_8                   
 
Complete!
[root@almt01 docker-rhel]# 
Code Block 78 docker install

system control 등록
[root@almt01 docker-rhel]# systemctl enable docker --now
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[root@almt01 docker-rhel]# 
Code Block 79 docker systemctl enable

실행
[root@almt01 docker-rhel]# systemctl start docker.service
[root@almt01 docker-rhel]# systemctl status docker.service
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since 화 2021-11-23 16:18:02 KST; 1min 9s ago
     Docs: https://docs.docker.com
 Main PID: 27796 (dockerd)
    Tasks: 8
   Memory: 30.2M
   CGroup: /system.slice/docker.service
           └─27796 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
 
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.328711725+09:00" level=info msg="[graphdriver] using prior storage driver: overlay2"
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.330844403+09:00" level=info msg="Loading containers: start."
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.361847869+09:00" level=info msg="failed to read ipv6 net.ipv6.conf.<bridge>....accept_ra
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.405436978+09:00" level=info msg="Default bridge (docker0) is assigned with a... address"
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.405571627+09:00" level=info msg="failed to read ipv6 net.ipv6.conf.<bridge>....accept_ra
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.436687451+09:00" level=info msg="Loading containers: done."
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.450489164+09:00" level=info msg="Docker daemon" commit=847da18 graphdriver(s...=20.10.11
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.450550410+09:00" level=info msg="Daemon has completed initialization"
11월 23 16:18:02 almt01 systemd[1]: Started Docker Application Container Engine.
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.463038684+09:00" level=info msg="API listen on /var/run/docker.sock"
Hint: Some lines were ellipsized, use -l to show in full.
[root@almt01 docker-rhel]# 
Code Block 80 docker start

상태확인
[root@almt01 docker-rhel]# systemctl status docker.service
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since 화 2021-11-23 16:18:02 KST; 1min 9s ago
     Docs: https://docs.docker.com
 Main PID: 27796 (dockerd)
    Tasks: 8
   Memory: 30.2M
   CGroup: /system.slice/docker.service
           └─27796 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
 
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.328711725+09:00" level=info msg="[graphdriver] using prior storage driver: overlay2"
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.330844403+09:00" level=info msg="Loading containers: start."
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.361847869+09:00" level=info msg="failed to read ipv6 net.ipv6.conf.<bridge>....accept_ra
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.405436978+09:00" level=info msg="Default bridge (docker0) is assigned with a... address"
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.405571627+09:00" level=info msg="failed to read ipv6 net.ipv6.conf.<bridge>....accept_ra
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.436687451+09:00" level=info msg="Loading containers: done."
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.450489164+09:00" level=info msg="Docker daemon" commit=847da18 graphdriver(s...=20.10.11
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.450550410+09:00" level=info msg="Daemon has completed initialization"
11월 23 16:18:02 almt01 systemd[1]: Started Docker Application Container Engine.
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.463038684+09:00" level=info msg="API listen on /var/run/docker.sock"
Hint: Some lines were ellipsized, use -l to show in full.
[root@almt01 docker-rhel]# 
Code Block 81 docker status

프로그램 종료


[root@almt01 docker-rhel]# systemctl stop docker
Warning: Stopping docker.service, but it can still be activated by:
  docker.socket
[root@almt01 docker-rhel]# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: inactive (dead) since 화 2021-11-23 16:19:58 KST; 3s ago
     Docs: https://docs.docker.com
  Process: 27796 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=0/SUCCESS)
 Main PID: 27796 (code=exited, status=0/SUCCESS)
 
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.436687451+09:00" level=info msg="Loading containers: done."
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.450489164+09:00" level=info msg="Docker daemon" commit=847da18 graphdriver(s...=20.10.11
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.450550410+09:00" level=info msg="Daemon has completed initialization"
11월 23 16:18:02 almt01 systemd[1]: Started Docker Application Container Engine.
11월 23 16:18:02 almt01 dockerd[27796]: time="2021-11-23T16:18:02.463038684+09:00" level=info msg="API listen on /var/run/docker.sock"
11월 23 16:19:58 almt01 systemd[1]: Stopping Docker Application Container Engine...
11월 23 16:19:58 almt01 dockerd[27796]: time="2021-11-23T16:19:58.737125294+09:00" level=info msg="Processing signal 'terminated'"
11월 23 16:19:58 almt01 dockerd[27796]: time="2021-11-23T16:19:58.739383370+09:00" level=info msg="stopping event stream following graceful sh...pace=moby
11월 23 16:19:58 almt01 dockerd[27796]: time="2021-11-23T16:19:58.739412748+09:00" level=info msg="Daemon shutdown complete"
11월 23 16:19:58 almt01 systemd[1]: Stopped Docker Application Container Engine.
Hint: Some lines were ellipsized, use -l to show in full.
[root@almt01 docker-rhel]# 
Code Block 82 docker stop

삭제(yum remove)

docker service 종료 후 수행해야 합니다.

[root@almt01 docker-rhel]# yum remove docker-ce.x86_64 docker-ce-cli.x86_64 docker-ce-rootless-extras.x86_64 docker-scan-plugin.x86_64
 policycoreutils-python.x86_64 fuse3-libs.x86_64 fuse-overlayfs.x86_64 slirp4netns.x86_64 containerd.io.x86_64 container-selinux.noarch
 libseccomp.x86_64 libseccomp.x86_64 container-selinux.noarch
 
Loaded plugins: product-id, search-disabled-repos, subscription-manager
This system is not registered with an entitlement server. You can use subscription-manager to register.
Resolving Dependencies
--> Running transaction check
---> Package container-selinux.noarch 2:2.119.2-1.911c772.el7_8 will be erased
---> Package containerd.io.x86_64 0:1.4.12-3.1.el7 will be erased
---> Package docker-ce.x86_64 3:20.10.11-3.el7 will be erased
---> Package docker-ce-cli.x86_64 1:20.10.11-3.el7 will be erased
---> Package docker-ce-rootless-extras.x86_64 0:20.10.11-3.el7 will be erased
---> Package docker-scan-plugin.x86_64 0:0.9.0-3.el7 will be erased
---> Package fuse-overlayfs.x86_64 0:0.7.2-6.el7_8 will be erased
---> Package fuse3-libs.x86_64 0:3.6.1-4.el7 will be erased
---> Package libseccomp.x86_64 0:2.3.1-3.el7 will be erased
---> Package policycoreutils-python.x86_64 0:2.5-29.el7 will be erased
---> Package slirp4netns.x86_64 0:0.4.3-4.el7_8 will be erased
--> Finished Dependency Resolution
 
Dependencies Resolved
 
===========================================================================================================================================================
 Package                                      Arch                      Version                                       Repository                      Size
===========================================================================================================================================================
Removing:
 container-selinux                            noarch                    2:2.119.2-1.911c772.el7_8                     installed                       41 k
 containerd.io                                x86_64                    1.4.12-3.1.el7                                installed                      108 M
 docker-ce                                    x86_64                    3:20.10.11-3.el7                              installed                       96 M
 docker-ce-cli                                x86_64                    1:20.10.11-3.el7                              installed                      139 M
 docker-ce-rootless-extras                    x86_64                    20.10.11-3.el7                                installed                       20 M
 docker-scan-plugin                           x86_64                    0.9.0-3.el7                                   installed                       13 M
 fuse-overlayfs                               x86_64                    0.7.2-6.el7_8                                 installed                      116 k
 fuse3-libs                                   x86_64                    3.6.1-4.el7                                   installed                      270 k
 libseccomp                                   x86_64                    2.3.1-3.el7                                   @local-repo                    297 k
 policycoreutils-python                       x86_64                    2.5-29.el7                                    @local-repo                    1.2 M
 slirp4netns                                  x86_64                    0.4.3-4.el7_8                                 installed                      169 k
 
Transaction Summary
===========================================================================================================================================================
Remove  11 Packages
 
Installed size: 378 M
Is this ok [y/N]: y
Downloading packages:
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Erasing    : docker-ce-rootless-extras-20.10.11-3.el7.x86_64                                                                                        1/11 
  Erasing    : 3:docker-ce-20.10.11-3.el7.x86_64                                                                                                      2/11 
  Erasing    : containerd.io-1.4.12-3.1.el7.x86_64                                                                                                    3/11 
  Erasing    : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                     4/11 
  Erasing    : docker-scan-plugin-0.9.0-3.el7.x86_64                                                                                                  5/11 
  Erasing    : 1:docker-ce-cli-20.10.11-3.el7.x86_64                                                                                                  6/11 
  Erasing    : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                    7/11 
  Erasing    : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                       8/11 
  Erasing    : libseccomp-2.3.1-3.el7.x86_64                                                                                                          9/11 
  Erasing    : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                         10/11 
  Erasing    : policycoreutils-python-2.5-29.el7.x86_64                                                                                              11/11 
  Verifying  : 1:docker-ce-cli-20.10.11-3.el7.x86_64                                                                                                  1/11 
  Verifying  : docker-scan-plugin-0.9.0-3.el7.x86_64                                                                                                  2/11 
  Verifying  : fuse3-libs-3.6.1-4.el7.x86_64                                                                                                          3/11 
  Verifying  : libseccomp-2.3.1-3.el7.x86_64                                                                                                          4/11 
  Verifying  : fuse-overlayfs-0.7.2-6.el7_8.x86_64                                                                                                    5/11 
  Verifying  : policycoreutils-python-2.5-29.el7.x86_64                                                                                               6/11 
  Verifying  : slirp4netns-0.4.3-4.el7_8.x86_64                                                                                                       7/11 
  Verifying  : 2:container-selinux-2.119.2-1.911c772.el7_8.noarch                                                                                     8/11 
  Verifying  : 3:docker-ce-20.10.11-3.el7.x86_64                                                                                                      9/11 
  Verifying  : docker-ce-rootless-extras-20.10.11-3.el7.x86_64                                                                                       10/11 
  Verifying  : containerd.io-1.4.12-3.1.el7.x86_64                                                                                                   11/11 
 
Removed:
  container-selinux.noarch 2:2.119.2-1.911c772.el7_8     containerd.io.x86_64 0:1.4.12-3.1.el7                 docker-ce.x86_64 3:20.10.11-3.el7          
  docker-ce-cli.x86_64 1:20.10.11-3.el7                  docker-ce-rootless-extras.x86_64 0:20.10.11-3.el7     docker-scan-plugin.x86_64 0:0.9.0-3.el7    
  fuse-overlayfs.x86_64 0:0.7.2-6.el7_8                  fuse3-libs.x86_64 0:3.6.1-4.el7                       libseccomp.x86_64 0:2.3.1-3.el7            
  policycoreutils-python.x86_64 0:2.5-29.el7             slirp4netns.x86_64 0:0.4.3-4.el7_8                   
 
Complete!
[root@almt01 docker-rhel]# 
Code Block 83 docker remove

기타
계정에 docker 수행 권한부여
[root@almt01 run]# ls -al | grep docker
drwx------   6 root  root    140 11월 30 14:29 docker
-rw-r--r--   1 root  root      5 11월 30 14:29 docker.pid
srw-rw----   1 root  root      0 11월 23 16:17 docker.sock
[root@almt01 run]# chmod 666 /var/run/docker.sock
[root@almt01 run]# ls -al | grep docker
drwx------   6 root  root    140 11월 30 14:29 docker
-rw-r--r--   1 root  root      5 11월 30 14:29 docker.pid
srw-rw-rw-   1 root  root      0 11월 23 16:17 docker.sock

[docker] compose v2 설치/실행 안내
안내
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
실행파일 다운로드 (bastion 서버 활용)
https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-linux-x86_64
bastion 서버 에서 실행파일 다운로드
[root@openwebt01 docker-rhel]# wget https://github.com/docker/compose/releases/download/v2.1.1/docker-compose-linux-x86_64
--2021-12-03 11:13:55--  https://github.com/docker/compose/releases/download/v2.1.1/docker-compose-linux-x86_64
Resolving github.com (github.com)... 15.164.81.167
Connecting to github.com (github.com)|15.164.81.167|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://objects.githubusercontent.com/github-production-release-asset-2e65be/15045751/207c804d-4aa9-40bc-b5bb-b139
f1c430e5?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20211203%2Fus-east-1%2Fs3%2Faws4_request&
X-Amz-Date=20211203T021355Z&X-Amz-Expires=300&X-Amz-Signature=bd4d9476b2155b1d4b77470b1aa5de9a7aa4175d112ae387461fcf047e054
cdd&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=15045751&response-content-disposition=attachment%3B%20filename%3D
docker-compose-linux-x86_64&response-content-type=application%2Foctet-stream [following]
--2021-12-03 11:13:55--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/15045751/207c804d-4aa9
-40bc-b5bb-b139f1c430e5?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20211203%2Fus-east-1%2Fs3%2F
aws4_request&X-Amz-Date=20211203T021355Z&X-Amz-Expires=300&X-Amz-Signature=bd4d9476b2155b1d4b77470b1aa5de9a7aa4175d112ae38746
1fcf047e054cdd&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=15045751&response-content-disposition=attachment%3B%20fil
ename%3Ddocker-compose-linux-x86_64&response-content-type=application%2Foctet-stream
Resolving objects.githubusercontent.com (objects.githubusercontent.com)... 185.199.110.133, 185.199.111.133, 185.199.109.133, ...
Connecting to objects.githubusercontent.com (objects.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 24637440 (23M) [application/octet-stream]
Saving to: ‘docker-compose-linux-x86_64’
 
100%[======================================================================================>] 24,637,440  9.49MB/s   in 2.5s   
 
2021-12-03 11:13:59 (9.49 MB/s) - ‘docker-compose-linux-x86_64’ saved [24637440/24637440]
 
[root@openwebt01 docker-rhel]# 
Code Block 84 batstion : docker compose download

파일 이동(설치 대상 서버 이동)
프로그램 설치
설치
[root@almt01 ~]# mkdir -p /usr/local/lib/docker/cli-plugins
 
[root@almt01 ~]# cd /usr/local/lib/docker/cli-plugins/
[root@almt01 cli-plugins]# pwd
/usr/local/lib/docker/cli-plugins
[root@almt01 cli-plugins]# cp -rf /home/docker/docker-rhel/docker-compose-linux-x86_64 /usr/local/lib/docker/cli-plugins
[root@almt01 cli-plugins]# mv docker-compose-linux-x86_64 docker-compose
[root@almt01 cli-plugins]# chmod +x docker-compose
Code Block 85 docker compose install

system control 재시작 및 compose 설치 확인
[root@almt01 bin]# systemctl stop docker
Warning: Stopping docker.service, but it can still be activated by:
  docker.socket
[root@almt01 bin]# systemctl start docker.service
[root@almt01 bin]# docker --help | grep compose
  compose*    Docker Compose (Docker Inc., v2.1.1)
[root@almt01 bin]# docker compose version
Docker Compose version v2.1.1
[root@almt01 bin]# 
Code Block 86 docker restart  & compose version check

[docker] 이미지 관리
신규 이미지 네트워크 분리된 서버에 등록 작업순서
1.	bastion 서버 에서 이미지 다운로드(pull)
2.	다운로드 받은 이미지를 추출(save)
3.	대상서버로 이미지 전송하여 이미지 등록(load)
4.	bastion 서버에서 이미지 삭제(rmi)
이미지 목록 확인(image)
docker image ls 또는 docker images <옵션>
docker images <이름> <옵션>
옵션
옵션	설명	예시
--digests	digest 정보 출력	
a, --all	부모 이미지 출력 설정	--all=false, 부모 이미지까지 모두 출력
-f	출력결과 필터 설정	-f "dangling=true", 이름이 없는 이미지 출력
--no-trunc	내용 생략 여부 설정	--no-trunc=false, 내용이 길어 생략된 부분까지 출력
q,--quiet	이미지 ID 만 출력	--quiet=false 이미지 ID 만 출력


[root@openwebt01 pg]# docker images
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
nginx                    latest              ed3d41941dba        3 months ago        133MB
backup                   latest              67d728a2deaf        3 months ago        4.03MB
yangsuite                latest              6998cfad0c06        3 months ago        842MB
ubuntu                   18.04               39a8cfeef173        4 months ago        63.1MB
nginx                    <none>              08b152afcfae        4 months ago        133MB
store/gitlab/gitlab-ce   11.10.4-ce.0        17d5117a2e37        2 years ago         1.76GB
alpine                   3.6                 43773d1dba76        2 years ago         4.03MB
[root@openwebt01 pg]# docker image ls
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
nginx                    latest              ed3d41941dba        3 months ago        133MB
backup                   latest              67d728a2deaf        3 months ago        4.03MB
yangsuite                latest              6998cfad0c06        3 months ago        842MB
ubuntu                   18.04               39a8cfeef173        4 months ago        63.1MB
nginx                    <none>              08b152afcfae        4 months ago        133MB
store/gitlab/gitlab-ce   11.10.4-ce.0        17d5117a2e37        2 years ago         1.76GB
alpine                   3.6                 43773d1dba76        2 years ago         4.03MB
[root@openwebt01 pg]# docker images --digests
REPOSITORY               TAG                 DIGEST                                                                    IMAGE ID            CREATED             SIZE
nginx                    latest              <none>                                                                    ed3d41941dba        3 months ago        133MB
backup                   latest              <none>                                                                    67d728a2deaf        3 months ago        4.03MB
yangsuite                latest              <none>                                                                    6998cfad0c06        3 months ago        842MB
ubuntu                   18.04               sha256:7bd7a9ca99f868bf69c4b6212f64f2af8e243f97ba13abb3e641e03a7ceb59e8   39a8cfeef173        4 months ago        63.1MB
nginx                    <none>              sha256:8f335768880da6baf72b70c701002b45f4932acae8d574dedfddaf967fc3ac90   08b152afcfae        4 months ago        133MB
store/gitlab/gitlab-ce   11.10.4-ce.0        sha256:cb3f9217c3159918bcc4b40d8452e8c59493222ec2395b3bdb43f9be21551fe1   17d5117a2e37        2 years ago         1.76GB
alpine                   3.6                 sha256:66790a2b79e1ea3e1dabac43990c54aca5d1ddf268d9a5a0285e4167c8b24475   43773d1dba76        2 years ago         4.03MB
[root@openwebt01 pg]# docker images alpine
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              3.6                 43773d1dba76        2 years ago         4.03MB
[root@openwebt01 pg]#
Code Block 87 docker image

이미지 다운로드(pull)
docker pull <docker hub 의 저장소 주소>
[root@openwebt01 ~]# docker pull store/gitlab/gitlab-ce:11.10.4-ce.0
11.10.4-ce.0: Pulling from store/gitlab/gitlab-ce
7e6591854262: Extracting [===========================>                       ]  24.31MB/43.75MB
089d60cb4e0a: Download complete 
9c461696bc09: Download complete 
45085432511a: Download complete 
fe923449954f: Download complete 
f7944584e435: Download complete 
47472ef1aa19: Download complete 
80d72d7c3c00: Download complete 
bb2031d6299d: Download complete 
7b6ae18e4081: Downloading [>                                                  ]  9.657MB/627.6MB
7b6ae18e4081: Extracting [=======>                                           ]  88.01MB/627.6MB
 
Digest: sha256:cb3f9217c3159918bcc4b40d8452e8c59493222ec2395b3bdb43f9be21551fe1
Status: Downloaded newer image for store/gitlab/gitlab-ce:11.10.4-ce.0
docker.io/store/gitlab/gitlab-ce:11.10.4-ce.0
[root@openwebt01 ~]# docker images --digests
REPOSITORY               TAG                 DIGEST                                                                    IMAGE ID            CREATED             SIZE
nginx                    latest              <none>                                                                    ed3d41941dba        3 months ago        133MB
<none>                   <none>              <none>                                                                    199451ce536f        3 months ago        842MB
<none>                   <none>              <none>                                                                    d0ed68d8fb84        3 months ago        842MB
<none>                   <none>              <none>                                                                    3a58c92c8a8d        3 months ago        842MB
backup                   latest              <none>                                                                    67d728a2deaf        3 months ago        4.03MB
yangsuite                latest              <none>                                                                    6998cfad0c06        3 months ago        842MB
ubuntu                   18.04               sha256:7bd7a9ca99f868bf69c4b6212f64f2af8e243f97ba13abb3e641e03a7ceb59e8   39a8cfeef173        3 months ago        63.1MB
nginx                    <none>              sha256:8f335768880da6baf72b70c701002b45f4932acae8d574dedfddaf967fc3ac90   08b152afcfae        4 months ago        133MB
store/gitlab/gitlab-ce   11.10.4-ce.0        sha256:cb3f9217c3159918bcc4b40d8452e8c59493222ec2395b3bdb43f9be21551fe1   17d5117a2e37        2 years ago         1.76GB
alpine                   3.6                 sha256:66790a2b79e1ea3e1dabac43990c54aca5d1ddf268d9a5a0285e4167c8b24475   43773d1dba76        2 years ago         4.03MB
[root@openwebt01 ~]# 
Code Block 88 docker pull

이미지 추출(save)
docker save -o <추출할파일명> REPOSITORY 정보: TAG 정보
[root@openwebt01 pg]# docker images
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
nginx                    latest              ed3d41941dba        3 months ago        133MB
<none>                   <none>              199451ce536f        3 months ago        842MB
<none>                   <none>              d0ed68d8fb84        3 months ago        842MB
<none>                   <none>              3a58c92c8a8d        3 months ago        842MB
backup                   latest              67d728a2deaf        3 months ago        4.03MB
yangsuite                latest              6998cfad0c06        3 months ago        842MB
ubuntu                   18.04               39a8cfeef173        4 months ago        63.1MB
nginx                    <none>              08b152afcfae        4 months ago        133MB
store/gitlab/gitlab-ce   11.10.4-ce.0        17d5117a2e37        2 years ago         1.76GB
alpine                   3.6                 43773d1dba76        2 years ago         4.03MB
[root@openwebt01 pg]# docker save -o gitlab.tar store/gitlab/gitlab-ce:11.10.4-ce.0
[root@openwebt01 pg]# ls -al | grep *.tar
-rw-------. 1 root root  1826008064 11월 30 14:42 gitlab.tar
[root@openwebt01 pg]# 
Code Block 89 docker save

이미지 등록(load)
docker load < <이미지파일명>
[root@almt01 docker]# docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[root@almt01 docker]# docker load < gitlab.tar 
a0c1e01578b7: Loading layer [==================================================>]  122.7MB/122.7MB
89ec57aea3bf: Loading layer [==================================================>]  15.87kB/15.87kB
7ccfaa7554e3: Loading layer [==================================================>]  11.78kB/11.78kB
d908c11b1a82: Loading layer [==================================================>]  3.072kB/3.072kB
5cc2ae7d798d: Loading layer [==================================================>]  75.91MB/75.91MB
315685ecc9e0: Loading layer [==================================================>]  2.048kB/2.048kB
32ae865ad85b: Loading layer [==================================================>]  2.048kB/2.048kB
f6fa7568d3f6: Loading layer [==================================================>]  2.048kB/2.048kB
c65a2dd94b6f: Loading layer [==================================================>]   16.9kB/16.9kB
e418a1f769d2: Loading layer [===========================================>       ]    1.4GB/1.627GB
Loaded image: store/gitlab/gitlab-ce:11.10.4-ce.0
[root@almt01 images]# docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
store/gitlab/gitlab-ce   11.10.4-ce.0   17d5117a2e37   2 years ago   1.76GB
[root@almt01 images]# 
Code Block 90 docker load

이미지 삭제(rmi)
docker rmi <image ID>
[root@openwebt01 ~]# docker images --digests
REPOSITORY               TAG                 DIGEST                                                                    IMAGE ID            CREATED             SIZE
nginx                    latest              <none>                                                                    ed3d41941dba        3 months ago        133MB
<none>                   <none>              <none>                                                                    199451ce536f        3 months ago        842MB
<none>                   <none>              <none>                                                                    d0ed68d8fb84        3 months ago        842MB
<none>                   <none>              <none>                                                                    3a58c92c8a8d        3 months ago        842MB
backup                   latest              <none>                                                                    67d728a2deaf        3 months ago        4.03MB
yangsuite                latest              <none>                                                                    6998cfad0c06        3 months ago        842MB
ubuntu                   18.04               sha256:7bd7a9ca99f868bf69c4b6212f64f2af8e243f97ba13abb3e641e03a7ceb59e8   39a8cfeef173        3 months ago        63.1MB
nginx                    <none>              sha256:8f335768880da6baf72b70c701002b45f4932acae8d574dedfddaf967fc3ac90   08b152afcfae        4 months ago        133MB
store/gitlab/gitlab-ce   11.10.4-ce.0        sha256:cb3f9217c3159918bcc4b40d8452e8c59493222ec2395b3bdb43f9be21551fe1   17d5117a2e37        2 years ago         1.76GB
alpine                   3.6                 sha256:66790a2b79e1ea3e1dabac43990c54aca5d1ddf268d9a5a0285e4167c8b24475   43773d1dba76        2 years ago         4.03MB
[root@openwebt01 ~]# docker rmi 17d5117a2e37
Untagged: store/gitlab/gitlab-ce:11.10.4-ce.0
Untagged: store/gitlab/gitlab-ce@sha256:cb3f9217c3159918bcc4b40d8452e8c59493222ec2395b3bdb43f9be21551fe1
Deleted: sha256:17d5117a2e3715b4632b30df670f1768082a5d0c9a578112cf468c346eceb481
Deleted: sha256:00953f7a61a51b59f4ac00f37277087e2fcacba4213fbd025c530e337f3013fa
Deleted: sha256:9cc51fb244651cf1108aaec0da191eb27e049750a758af8ea11c1d9d21ef6b61
Deleted: sha256:558c4364ec91e5fb21d3f28005bfc8ee1fca9d63255151cdfd1b15f33a324250
Deleted: sha256:165e5cf07f7838560dced7bf9b5c87b666fb6f9f6f061e231032a16a8207ec89
Deleted: sha256:bd85c337734a034314ee81a3dc5fefaa3934b7b06a929b95799a2b680fdb4911
Deleted: sha256:268dc5da8cab3074992cbcdda5fe8fb4e26086454954526e0eae44fd327b3ec2
Deleted: sha256:e6fa212a7165a143d61823d67be268e19c7745a9c168756b71a0791831ebcc16
Deleted: sha256:6f3c18e03a8828f895bc8e7fc1df5b7a6c199160370f29c7272c7ed5bcedb2ce
Deleted: sha256:281e4ad18351d1556bd4764e674986d15572b52ec96137d7417fd4cc071c12ab
Deleted: sha256:a0c1e01578b7e57d891b82a53a9debdb52dc642c581de3e9231d395989d39a03
[root@openwebt01 ~]# docker images --digests
REPOSITORY          TAG                 DIGEST                                                                    IMAGE ID            CREATED             SIZE
nginx               latest              <none>                                                                    ed3d41941dba        3 months ago        133MB
<none>              <none>              <none>                                                                    199451ce536f        3 months ago        842MB
<none>              <none>              <none>                                                                    d0ed68d8fb84        3 months ago        842MB
<none>              <none>              <none>                                                                    3a58c92c8a8d        3 months ago        842MB
backup              latest              <none>                                                                    67d728a2deaf        3 months ago        4.03MB
yangsuite           latest              <none>                                                                    6998cfad0c06        3 months ago        842MB
ubuntu              18.04               sha256:7bd7a9ca99f868bf69c4b6212f64f2af8e243f97ba13abb3e641e03a7ceb59e8   39a8cfeef173        3 months ago        63.1MB
nginx               <none>              sha256:8f335768880da6baf72b70c701002b45f4932acae8d574dedfddaf967fc3ac90   08b152afcfae        4 months ago        133MB
alpine              3.6                 sha256:66790a2b79e1ea3e1dabac43990c54aca5d1ddf268d9a5a0285e4167c8b24475   43773d1dba76        2 years ago         4.03MB
[root@openwebt01 ~]# 
Code Block 91 docker rmi

[docker] 컨테이너 관리
컨테이너 목록
docker container ls <옵션>또는 docker ps <옵션>
옵션 정보
옵션	설명	예시
a, --all	전체 목록 출력	--all, 정지된 컨테이너 목록까지 모두 출력
[docker@almt01 ~]$ docker ps -all
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                       PORTS     NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Exited (137) 2 minutes ago             gitlab
[docker@almt01 ~]$ docker container ls --all
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                       PORTS     NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Exited (137) 3 minutes ago             gitlab
[docker@almt01 ~]$ 
Code Block 92 docker container list

컨테이너 실행(새로운 컨테이너 생성)
docker run <옵션><컨테이너이름>
docker run --detach \
  --hostname docker.nicepay.co.kr \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/home/docker/gitlab \
  --volume /srv/gitlab/logs:/home/docker/gitlab/logs \
  --volume /srv/gitlab/data:/home/docker/gitlab/data \
gitlab/gitlab-ce:latest
Code Block 93 docker run command

[docker@almt01 ~]$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[docker@almt01 ~]$ docker run --detach \
>   --hostname docker.nicepay.co.kr \
>   --publish 443:443 --publish 80:80 \
>   --name gitlab \
>   --volume /srv/gitlab/config:/home/docker/gitlab \
>   --volume /srv/gitlab/logs:/home/docker/gitlab/logs \
>   --volume /srv/gitlab/data:/home/docker/gitlab/data \
> 17d5117a2e37
1051e4f9a981e66dab277d014e750c2eaabbdbb3df48becfbd1f481c620aa54a
[docker@almt01 ~]$ 
Code Block 94 docker container first run

컨테이너 시작
docker start <컨테이너이름>
[docker@almt01 ~]$ clear
[docker@almt01 ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                       PORTS     NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Exited (137) 5 minutes ago             gitlab
[docker@almt01 ~]$ docker start gitlab
gitlab
[docker@almt01 ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                            PORTS                                 NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Up 5 seconds (health: starting)   22/tcp, 443/tcp, 0.0.0.0:80->80/tcp   gitlab
[docker@almt01 ~]$ 
Code Block 95 docker container start

컨테이너 정지
docker container stop <컨테이너이름>
[docker@almt01 ~]$ clear
[docker@almt01 ~]$ docker ps
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                        PORTS                                 NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Up About a minute (healthy)   22/tcp, 443/tcp, 0.0.0.0:80->80/tcp   gitlab
[docker@almt01 ~]$ docker stop gitlab
gitlab
[docker@almt01 ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                     PORTS     NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Exited (0) 6 seconds ago             gitlab
[docker@almt01 ~]$ 
Code Block 96 docker container stop

컨테이너 재시작
docker container restart <컨테이너이름>
[docker@almt01 ~]$ docker ps
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                            PORTS                                 NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Up 7 seconds (health: starting)   22/tcp, 443/tcp, 0.0.0.0:80->80/tcp   gitlab
[docker@almt01 ~]$ docker container restart gitlab
gitlab
[docker@almt01 ~]$ docker ps
CONTAINER ID   IMAGE          COMMAND             CREATED        STATUS                            PORTS                                 NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   47 hours ago   Up 6 seconds (health: starting)   22/tcp, 443/tcp, 0.0.0.0:80->80/tcp   gitlab
[docker@almt01 ~]$ 
Code Block 97 docker container restart

컨테이너 삭제
docker rm <컨테이너ID>
[docker@almt01 ~]$ docker ps -a
CONTAINER ID   IMAGE          COMMAND             CREATED      STATUS                      PORTS     NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   2 days ago   Exited (0) 17 seconds ago             gitlab
[docker@almt01 ~]$ docker rm 4de758149014
4de758149014
[docker@almt01 ~]$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[docker@almt01 ~]$ 
Code Block 98 docker container remove

컨테이너 강제삭제
docker rm -f <컨테이너ID>
[root@almt01 docker]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS                   PORTS                                              NAMES
2de33a1a5996   1c520775844c   "/sbin/tini -- /usr/…"   17 hours ago   Up 17 hours              0.0.0.0:8080->8080/tcp, 0.0.0.0:4000->50000/tcp    jenkins
5db4ce88dab3   4062f34e61f6   "/assets/wrapper"        7 weeks ago    Up 7 weeks (unhealthy)   0.0.0.0:80->80/tcp, 22/tcp, 0.0.0.0:443->443/tcp   gitlab
[root@almt01 docker]# docker rm -f 5db4ce88dab3
5db4ce88dab3
[root@almt01 docker]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS        PORTS                                             NAMES
2de33a1a5996   1c520775844c   "/sbin/tini -- /usr/…"   17 hours ago   Up 17 hours   0.0.0.0:8080->8080/tcp, 0.0.0.0:4000->50000/tcp   jenkins
[root@almt01 docker]# 
Code Block 99 docker container force remove

컨테이너 명령
docker exec <옵션> <컨테이너ID> <접속shell>
옵션 정보
옵션	설명	예시
-d, --detach	명령을 백그라운드로 실행	
-i, --interactive	표준 입력(stdin) 을 활성화	docker exec -it 4de758149014 /bin/bash
-t, --tty	pseudo-TTY(teletypewriter) 가상콘솔 사용	docker exec -it 4de758149014 /bin/bash
-w, --workdir	프로세스 실행 위치 변경	docker execit -workdir /tmp ghost bash
[docker@almt01 ~]$ docker ps
CONTAINER ID   IMAGE          COMMAND             CREATED      STATUS                    PORTS                                 NAMES
4de758149014   17d5117a2e37   "/assets/wrapper"   2 days ago   Up 25 minutes (healthy)   22/tcp, 443/tcp, 0.0.0.0:80->80/tcp   gitlab
[docker@almt01 ~]$ docker exec -it 4de758149014 /bin/bash
root@gitlab:/# pwd
/
root@gitlab:/# ls -al
total 4
drwxr-xr-x   1 root root  74 Nov 30 06:23 .
drwxr-xr-x   1 root root  74 Nov 30 06:23 ..
-rwxr-xr-x   1 root root   0 Nov 30 06:23 .dockerenv
-rw-r--r--   1 root root 159 May  1  2019 RELEASE
drwxr-xr-x   2 root root 120 May  1  2019 assets
drwxr-xr-x   1 root root  31 May  1  2019 bin
drwxr-xr-x   2 root root   6 Apr 12  2016 boot
drwxr-xr-x   5 root root 340 Dec  2 06:16 dev
drwxr-xr-x   1 root root  22 Nov 30 06:23 etc
drwxr-xr-x   1 root root  20 Nov 30 06:23 home
drwxr-xr-x   1 root root  45 Sep 13  2015 lib
drwxr-xr-x   2 root root  34 Apr 25  2019 lib64
drwxr-xr-x   2 root root   6 Apr 25  2019 media
drwxr-xr-x   2 root root   6 Apr 25  2019 mnt
drwxr-xr-x   1 root root  20 May  1  2019 opt
dr-xr-xr-x 296 root root   0 Dec  2 06:16 proc
drwx------   1 root root  27 Dec  2 06:17 root
drwxr-xr-x   1 root root  34 Dec  2 06:16 run
drwxr-xr-x   1 root root  21 Apr 26  2019 sbin
drwxr-xr-x   2 root root   6 Apr 25  2019 srv
dr-xr-xr-x  13 root root   0 Nov 22 01:49 sys
drwxrwxrwt   1 root root  62 Dec  2 06:16 tmp
drwxr-xr-x   1 root root  17 Apr 25  2019 usr
drwxr-xr-x   1 root root  39 Apr 25  2019 var
root@gitlab:/# exit
exit
[docker@almt01 ~]$ 
Code Block 100 docker container exec

[docker] compose 구성 및 실행
docker compose 구성

version: '3.0'
services:
  web:
    image: "17d5117a2e37"
    restart: always
    hostname: "docker.nicepay.co.kr"
    container_name : "gitlab"
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://gitlab.example.com'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - "/srv/gitlab/config:/home/docker/gitlab"
      - "/srv/gitlab/logs:/home/docker/gitlab/logs"
      - "/srv/gitlab/data:/home/docker/gitlab/data"
Code Block 101 docker-compose.yml


docker compose 실행(yaml 파일 위치 내 실행)

[docker@almt01 gitlab-ee]$ docker compose up -d
[+] Running 2/2
 ⠿ Network gitlab-ee_default  Created                                                                                                                   0.0s
 ⠿ Container gitlab           Started                                                                                                                   0.4s
[docker@almt01 gitlab-ee]$ docker ps
CONTAINER ID   IMAGE          COMMAND             CREATED         STATUS                            PORTS                                              NAMES
0af0b8388222   17d5117a2e37   "/assets/wrapper"   2 minutes ago   Up 2 minutes (health: starting)   0.0.0.0:80->80/tcp, 22/tcp, 0.0.0.0:443->443/tcp   gitlab
[docker@almt01 gitlab-ee]$ 
Code Block 102 docker compose up

CI/CD : GitLab
GitLab 이란
GitLab
 - 2014년 설립
 - 2020년 말 직원 1,3000 명 규모
 - 개발에서 운영 까지 단일툴로 제공



GitLab vs. 다른 도구들
[Gitlab] 운영자 가이드
[Gitlab] 설치/실행 안내
docker 를 이용한 Gitlab 설치
bastion host 다운로드 대상
docker image name	Docker Pull Command
gitlab enterprise edition	docker pull gitlab/gitlab-ee
gitlab community edition	docker pull gitlab/gitlab-ce
이미지 업로드
[root@almt01 docker]# docker images REPOSITORY TAG IMAGE ID CREATED SIZE 
[root@almt01 docker]# docker load < gitlab-ee.tar 
a0c1e01578b7: Loading layer [==================================================>] 122.7MB/122.7MB 
89ec57aea3bf: Loading layer [==================================================>] 15.87kB/15.87kB 
7ccfaa7554e3: Loading layer [==================================================>] 11.78kB/11.78kB 
d908c11b1a82: Loading layer [==================================================>] 3.072kB/3.072kB 
5cc2ae7d798d: Loading layer [==================================================>] 75.91MB/75.91MB 
315685ecc9e0: Loading layer [==================================================>] 2.048kB/2.048kB 
32ae865ad85b: Loading layer [==================================================>] 2.048kB/2.048kB 
f6fa7568d3f6: Loading layer [==================================================>] 2.048kB/2.048kB 
c65a2dd94b6f: Loading layer [==================================================>] 16.9kB/16.9kB 
e418a1f769d2: Loading layer [===========================================>       ] 1.4GB/1.627GB 
Loaded image: store/gitlab/gitlab-ee:latest 
[root@almt01 images]# docker images REPOSITORY TAG IMAGE ID CREATED SIZE gitlab/gitlab-ee latest 4062f34e61f6 42 hours ago 2.5GB 
[root@almt01 images]#
Code Block 103 gitlab docker load

docker 를 이용한 Gitlab 실행
방법1) docker run 활용
[docker@almt01 ~]$ docker ps -a 
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES 
[docker@almt01 ~]$ docker run --detach \ 
> --hostname docker.nicepay.co.kr \ 
> --publish 443:443 --publish 80:80 \ 
> --name gitlab \ 
> --volume /srv/gitlab/config:/home/docker/gitlab \ 
> --volume /srv/gitlab/logs:/home/docker/gitlab/logs \ 
> --volume /srv/gitlab/data:/home/docker/gitlab/data \ 
> 4062f34e61f6 1051e4f9a981e66dab277d014e750c2eaabbdbb3df48becfbd1f481c620aa54a 
[docker@almt01 ~]$
Code Block 104 gitlab docker run

방법2) docker compose 활용
프로젝트 디렉토리 생성 후 docker-compose.yml 파일 생성
version: '3.0'
services:
  web:
    image: '4062f34e61f6'
    #restart: always
    hostname: 'docker.nicepay.co.kr'
    container_name : 'gitlab'
    environment:
      GITLAB_OMNIBUS_CONFIG:
        external_url 'http://172.32.161.36'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '80:80'
      - '443:443'
    volumes:
      - '/srv/gitlab/config:/home/docker/gitlab'
      - '/srv/gitlab/logs:/home/docker/gitlab/logs'
      - '/srv/gitlab/data:/home/docker/gitlab/data'
Code Block 105 gitlab-ee docker-compose.yml

docker compose 실행
[docker@almt01 gitlab-ee]$ docker compose up -d 
[+] Running 1/1 ⠿ Container gitlab Started 0.4s 
[docker@almt01 gitlab-ee]$ docker ps
Code Block 106 gitlab docker compose up

[Gitlab] SMTP 설정
SSL 없이 SMTP 설정
gitlab config 파일(/etc/gitlab/gitlab.rb) 파일 에 아래 내용 추가
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = '대상 주소'
gitlab_rails['smtp_port'] = 대상port
gitlab_rails['smtp_user_name'] = '발송자 메일주소'
gitlab_rails['smtp_domain'] = '대상 주소'
gitlab_rails['smtp_tls'] = false
gitlab_rails['smtp_openssl_verify_mode'] = 'none'
gitlab_rails['smtp_enable_starttls_auto'] = false
gitlab_rails['smtp_ssl'] = false
gitlab_rails['smtp_force_ssl'] = false
 
gitlab_rails['gitlab_email_from'] = '보내는 사람 메일 제목'
gitlab_rails['gitlab_email_display_name'] = '보내는 사람 이름'
Code Block 107 /etc/gitlab/gitlab.rb

gitlab-ctl reconfigure 입력
root@docker:/etc/gitlab# gitlab-ctl reconfigure
Starting Chef Infra Client, version 15.17.4
resolving cookbooks for run list: ["gitlab-ee"]
Synchronizing Cookbooks:
  - gitlab-ee (0.0.1)
  - package (0.1.0)
  - gitlab (0.0.1)
  - consul (0.1.0)
  - patroni (0.1.0)
  - pgbouncer (0.1.0)
  - runit (5.1.3)
  - logrotate (0.1.0)
  - postgresql (0.1.0)
  - redis (0.1.0)
  - monitoring (0.1.0)
  - registry (0.1.0)
  - mattermost (0.1.0)
  - gitaly (0.1.0)
  - praefect (0.1.0)
  - gitlab-pages (0.1.0)
  - letsencrypt (0.1.0)
  - gitlab-kas (0.1.0)
  - nginx (0.1.0)
  - acme (4.1.3)
  - crond (0.1.0)
Installing Cookbook Gems:
Compiling Cookbooks...
Recipe: gitlab::default
  * directory[/etc/gitlab] action create (up to date)
  Converging 282 resources
  * directory[/etc/gitlab] action create (up to date)
  * directory[Create /var/opt/gitlab] action create (up to date)
  * directory[Create /var/log/gitlab] action create (up to date)
  * directory[/opt/gitlab/embedded/etc] action create (up to date)
  * template[/opt/gitlab/embedded/etc/gitconfig] action create (up to date)
Recipe: gitlab::web-server
  * account[Webserver user and group] action create (up to date)
Recipe: gitlab::users
  * directory[/var/opt/gitlab] action create (up to date)
  * account[GitLab user and group] action create (up to date)
  * template[/var/opt/gitlab/.gitconfig] action create (up to date)
  * directory[/var/opt/gitlab/.bundle] action create (up to date)
Recipe: gitlab::gitlab-shell
  * storage_directory[/var/opt/gitlab/.ssh] action create
    * ruby_block[directory resource: /var/opt/gitlab/.ssh] action run (skipped due to not_if)
     (up to date)
  * directory[/var/log/gitlab/gitlab-shell/] action create (up to date)
  * directory[/var/opt/gitlab/gitlab-shell] action create (up to date)
  * templatesymlink[Create a config.yml and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-shell/config.yml] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-shell/config.yml to /var/opt/gitlab/gitlab-shell/config.yml] action create (up to date)
     (up to date)
  * link[/opt/gitlab/embedded/service/gitlab-shell/.gitlab_shell_secret] action create (up to date)
  * file[/var/opt/gitlab/.ssh/authorized_keys] action create_if_missing (up to date)
Recipe: gitlab::gitlab-rails
  * storage_directory[/var/opt/gitlab/git-data] action create
    * ruby_block[directory resource: /var/opt/gitlab/git-data] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/git-data/repositories] action create
    * ruby_block[directory resource: /var/opt/gitlab/git-data/repositories] action run (skipped due to not_if)
     (up to date)
Recipe: gitlab::rails_pages_shared_path
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/pages] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/pages] action run (skipped due to not_if)
     (up to date)
Recipe: gitlab::gitlab-rails
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/artifacts] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/artifacts] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/external-diffs] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/external-diffs] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/lfs-objects] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/lfs-objects] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/packages] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/packages] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/dependency_proxy] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/dependency_proxy] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/terraform_state] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/terraform_state] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/encrypted_settings] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/encrypted_settings] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/uploads] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/uploads] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-ci/builds] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-ci/builds] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/cache] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/cache] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/var/opt/gitlab/gitlab-rails/shared/tmp] action create
    * ruby_block[directory resource: /var/opt/gitlab/gitlab-rails/shared/tmp] action run (skipped due to not_if)
     (up to date)
  * storage_directory[/opt/gitlab/embedded/service/gitlab-rails/public] action create (skipped due to only_if)
  * directory[create /var/opt/gitlab/gitlab-rails/etc] action create (up to date)
  * directory[create /opt/gitlab/etc/gitlab-rails] action create (up to date)
  * directory[create /var/opt/gitlab/gitlab-rails/working] action create (up to date)
  * directory[create /var/opt/gitlab/gitlab-rails/tmp] action create (up to date)
  * directory[create /var/opt/gitlab/gitlab-rails/upgrade-status] action create (up to date)
  * directory[create /var/log/gitlab/gitlab-rails] action create (up to date)
  * storage_directory[/var/opt/gitlab/backups] action create
    * ruby_block[directory resource: /var/opt/gitlab/backups] action run (skipped due to not_if)
     (up to date)
  * directory[/var/opt/gitlab/gitlab-rails] action create (up to date)
  * directory[/var/opt/gitlab/gitlab-ci] action create (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/gitlab-registry.key] action create (skipped due to only_if)
  * template[/opt/gitlab/etc/gitlab-rails-rc] action create (up to date)
  * file[/opt/gitlab/etc/gitlab-rails/gitlab-rails-rc] action delete (up to date)
  * file[/opt/gitlab/embedded/service/gitlab-rails/.secret] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/secret] action delete (up to date)
  * templatesymlink[Create a database.yml and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/database.yml] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/config/database.yml to /var/opt/gitlab/gitlab-rails/etc/database.yml] action create (up to date)
     (up to date)
  * templatesymlink[Create a secrets.yml and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/secrets.yml] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/config/secrets.yml to /var/opt/gitlab/gitlab-rails/etc/secrets.yml] action create (up to date)
     (up to date)
  * templatesymlink[Create a resque.yml and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/resque.yml] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/config/resque.yml to /var/opt/gitlab/gitlab-rails/etc/resque.yml] action create (up to date)
     (up to date)
  * templatesymlink[Create a cable.yml and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/cable.yml] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/config/cable.yml to /var/opt/gitlab/gitlab-rails/etc/cable.yml] action create (up to date)
     (up to date)
  * templatesymlink[Create a redis.cache.yml and create a symlink to Rails root] action create (skipped due to not_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/config/redis.cache.yml] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/redis.cache.yml] action delete (up to date)
  * templatesymlink[Create a redis.queues.yml and create a symlink to Rails root] action create (skipped due to not_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/config/redis.queues.yml] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/redis.queues.yml] action delete (up to date)
  * templatesymlink[Create a redis.shared_state.yml and create a symlink to Rails root] action create (skipped due to not_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/config/redis.shared_state.yml] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/redis.shared_state.yml] action delete (up to date)
  * templatesymlink[Create a redis.trace_chunks.yml and create a symlink to Rails root] action create (skipped due to not_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/config/redis.trace_chunks.yml] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/redis.trace_chunks.yml] action delete (up to date)
  * templatesymlink[Create a redis.rate_limiting.yml and create a symlink to Rails root] action create (skipped due to not_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/config/redis.rate_limiting.yml] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/redis.rate_limiting.yml] action delete (up to date)
  * templatesymlink[Create a redis.sessions.yml and create a symlink to Rails root] action create (skipped due to not_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/config/redis.sessions.yml] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/redis.sessions.yml] action delete (up to date)
  * templatesymlink[Create a smtp_settings.rb and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/smtp_settings.rb] action create
      - create new file /var/opt/gitlab/gitlab-rails/etc/smtp_settings.rb
      - update content in file /var/opt/gitlab/gitlab-rails/etc/smtp_settings.rb from none to 106d43
      --- /var/opt/gitlab/gitlab-rails/etc/smtp_settings.rb 2021-12-08 00:11:26.641817884 +0000
      +++ /var/opt/gitlab/gitlab-rails/etc/.chef-smtp_settings20211208-13995-16zlgw9.rb 2021-12-08 00:11:26.641817884 +0000
      @@ -1 +1,26 @@
      +# This file is managed by gitlab-ctl. Manual changes will be
      +# erased! To change the contents below, edit /etc/gitlab/gitlab.rb
      +# and run `sudo gitlab-ctl reconfigure`.
      +
      +if Rails.env.production?
      +  secrets = Gitlab::Email::SmtpConfig.secrets
      +  smtp_settings = {
      +    user_name: secrets.username,
      +    password: secrets.password,
      +    address: "172.28.121.10",
      +    port: 25,
      +    domain: "172.28.121.10",
      +    enable_starttls_auto: false,
      +    tls: false,
      +    ssl: false,
      +    openssl_verify_mode: "none",
      +    
      +    ca_file: "/opt/gitlab/embedded/ssl/certs/cacert.pem",
      +  }
      +
      +  Gitlab::Application.config.action_mailer.delivery_method = :smtp
      +  ActionMailer::Base.delivery_method = :smtp
      +
      +  ActionMailer::Base.smtp_settings = smtp_settings
      +end
      - change mode from '' to '0644'
      - change owner from '' to 'root'
      - change group from '' to 'root'
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/config/initializers/smtp_settings.rb to /var/opt/gitlab/gitlab-rails/etc/smtp_settings.rb] action create
      - create symlink at /opt/gitlab/embedded/service/gitlab-rails/config/initializers/smtp_settings.rb to /var/opt/gitlab/gitlab-rails/etc/smtp_settings.rb
  
  * templatesymlink[Create a gitlab.yml and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/gitlab.yml] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml to /var/opt/gitlab/gitlab-rails/etc/gitlab.yml] action create (up to date)
     (up to date)
  * templatesymlink[Create a gitlab_workhorse_secret and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/gitlab_workhorse_secret] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/.gitlab_workhorse_secret to /var/opt/gitlab/gitlab-rails/etc/gitlab_workhorse_secret] action create (up to date)
     (up to date)
  * templatesymlink[Create a gitlab_shell_secret and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/gitlab_shell_secret] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/.gitlab_shell_secret to /var/opt/gitlab/gitlab-rails/etc/gitlab_shell_secret] action create (up to date)
     (up to date)
  * templatesymlink[Create a gitlab_pages_secret and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/gitlab_pages_secret] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/.gitlab_pages_secret to /var/opt/gitlab/gitlab-rails/etc/gitlab_pages_secret] action create (up to date)
     (up to date)
  * templatesymlink[Create a gitlab_kas_secret and create a symlink to Rails root] action create
    * template[/var/opt/gitlab/gitlab-rails/etc/gitlab_kas_secret] action create (up to date)
    * link[Link /opt/gitlab/embedded/service/gitlab-rails/.gitlab_kas_secret to /var/opt/gitlab/gitlab-rails/etc/gitlab_kas_secret] action create (up to date)
     (up to date)
  * link[/opt/gitlab/embedded/service/gitlab-rails/config/initializers/relative_url.rb] action delete (up to date)
  * file[/var/opt/gitlab/gitlab-rails/etc/relative_url.rb] action delete (up to date)
  * env_dir[/opt/gitlab/etc/gitlab-rails/env] action create
    * directory[/opt/gitlab/etc/gitlab-rails/env] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/HOME] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/RAILS_ENV] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/LD_PRELOAD] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/BUNDLE_GEMFILE] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/SIDEKIQ_MEMORY_KILLER_MAX_RSS] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/PATH] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/ICU_DATA] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/PYTHONPATH] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/EXECJS_RUNTIME] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-rails/env/TZ] action create (up to date)
     (up to date)
  * link[/opt/gitlab/embedded/service/gitlab-rails/tmp] action create (up to date)
  * link[/opt/gitlab/embedded/service/gitlab-rails/public/uploads] action create (up to date)
  * link[/opt/gitlab/embedded/service/gitlab-rails/log] action create (up to date)
  * link[/var/log/gitlab/gitlab-rails/sidekiq.log] action delete (skipped due to only_if)
  * file[/opt/gitlab/embedded/service/gitlab-rails/db/structure.sql] action create (up to date)
  * remote_file[/var/opt/gitlab/gitlab-rails/VERSION] action create/opt/gitlab/embedded/lib/ruby/gems/2.7.0/gems/chef-15.17.4/lib/chef/provider/remote_file/local_file.rb:43: warning: URI.unescape is obsolete
 (up to date)
  * remote_file[/var/opt/gitlab/gitlab-rails/REVISION] action create/opt/gitlab/embedded/lib/ruby/gems/2.7.0/gems/chef-15.17.4/lib/chef/provider/remote_file/local_file.rb:43: warning: URI.unescape is obsolete
 (up to date)
  * version_file[Create version file for Rails] action create
    * file[/var/opt/gitlab/gitlab-rails/RUBY_VERSION] action create (up to date)
     (up to date)
  * execute[clear the gitlab-rails cache] action nothing (skipped due to action :nothing)
  * file[/var/opt/gitlab/gitlab-rails/config.ru] action delete (up to date)
Recipe: gitlab::selinux
  * bash[Set proper security context on ssh files for selinux] action nothing (skipped due to action :nothing)
Recipe: gitlab::add_trusted_certs
  * directory[/etc/gitlab/trusted-certs] action create (up to date)
  * directory[/opt/gitlab/embedded/ssl/certs] action create (up to date)
  * file[/opt/gitlab/embedded/ssl/certs/README] action create (up to date)
  * ruby_block[Move existing certs and link to /opt/gitlab/embedded/ssl/certs] action run (skipped due to only_if)
Recipe: gitlab::default
  * service[create a temporary puma service] action nothing (skipped due to action :nothing)
  * service[create a temporary sidekiq service] action nothing (skipped due to action :nothing)
  * service[create a temporary mailroom service] action nothing (skipped due to action :nothing)
Recipe: package::sysctl
  * execute[reload all sysctl conf] action nothing (skipped due to action :nothing)
Recipe: logrotate::folders_and_configs
  * directory[/var/opt/gitlab/logrotate] action create (up to date)
  * directory[/var/opt/gitlab/logrotate/logrotate.d] action create (up to date)
  * directory[/var/log/gitlab/logrotate] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.conf] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/nginx] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/puma] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/gitlab-rails] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/gitlab-shell] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/gitlab-workhorse] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/gitlab-pages] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/gitlab-kas] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/gitaly] action create (up to date)
  * template[/var/opt/gitlab/logrotate/logrotate.d/mailroom] action create (up to date)
Recipe: logrotate::enable
  * service[logrotate] action nothing (skipped due to action :nothing)
  * runit_service[logrotate] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/logrotate] action create (up to date)
    * template[/opt/gitlab/sv/logrotate/run] action create (up to date)
    * directory[/opt/gitlab/sv/logrotate/log] action create (up to date)
    * directory[/opt/gitlab/sv/logrotate/log/main] action create (up to date)
    * template[/opt/gitlab/sv/logrotate/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_logrotate] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/logrotate/config] action create (up to date)
    * template[/opt/gitlab/sv/logrotate/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/logrotate/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for logrotate service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/logrotate/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/logrotate/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/logrotate/control] action create (up to date)
    * template[/opt/gitlab/sv/logrotate/control/t] action create (up to date)
    * link[/opt/gitlab/init/logrotate] action create (up to date)
    * file[/opt/gitlab/sv/logrotate/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/logrotate] action create (up to date)
    * ruby_block[wait for logrotate service socket] action run (skipped due to not_if)
     (up to date)
Recipe: redis::enable
  * redis_service[redis] action create
    * account[user and group for redis] action create (up to date)
    * group[Socket group] action create (up to date)
    * directory[/var/opt/gitlab/redis] action create (up to date)
    * directory[/var/log/gitlab/redis] action create (up to date)
    * template[/var/opt/gitlab/redis/redis.conf] action create (up to date)
  Recipe: <Dynamically Defined Resource>
    * service[redis] action nothing (skipped due to action :nothing)
    * runit_service[redis] action enable
      * ruby_block[restart_service] action nothing (skipped due to action :nothing)
      * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
      * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
      * directory[/opt/gitlab/sv/redis] action create (up to date)
      * template[/opt/gitlab/sv/redis/run] action create (up to date)
      * directory[/opt/gitlab/sv/redis/log] action create (up to date)
      * directory[/opt/gitlab/sv/redis/log/main] action create (up to date)
      * template[/opt/gitlab/sv/redis/log/config] action create (up to date)
      * ruby_block[verify_chown_persisted_on_redis] action nothing (skipped due to action :nothing)
      * link[/var/log/gitlab/redis/config] action create (up to date)
      * template[/opt/gitlab/sv/redis/log/run] action create (up to date)
      * directory[/opt/gitlab/sv/redis/env] action create (up to date)
      * ruby_block[Delete unmanaged env files for redis service] action run (skipped due to only_if)
      * template[/opt/gitlab/sv/redis/check] action create (skipped due to only_if)
      * template[/opt/gitlab/sv/redis/finish] action create (skipped due to only_if)
      * directory[/opt/gitlab/sv/redis/control] action create (up to date)
      * link[/opt/gitlab/init/redis] action create (up to date)
      * file[/opt/gitlab/sv/redis/down] action nothing (skipped due to action :nothing)
      * directory[/opt/gitlab/service] action create (up to date)
      * link[/opt/gitlab/service/redis] action create (up to date)
      * ruby_block[wait for redis service socket] action run (skipped due to not_if)
       (up to date)
    * ruby_block[warn pending redis restart] action run (skipped due to only_if)
     (up to date)
Recipe: redis::enable
  * template[/opt/gitlab/etc/gitlab-redis-cli-rc] action create (up to date)
Recipe: gitaly::enable
  * directory[/var/opt/gitlab/gitaly] action create (up to date)
  * directory[/var/log/gitlab/gitaly] action create (up to date)
  * directory[/var/opt/gitlab/gitaly/internal_sockets] action create (up to date)
  * env_dir[/opt/gitlab/etc/gitaly/env] action create
    * directory[/opt/gitlab/etc/gitaly/env] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/HOME] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/PATH] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/TZ] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/PYTHONPATH] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/ICU_DATA] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/SSL_CERT_DIR] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/GITALY_PID_FILE] action create (up to date)
    * file[/opt/gitlab/etc/gitaly/env/WRAPPER_JSON_LOGGING] action create (up to date)
     (up to date)
  * template[Create Gitaly config.toml] action create (up to date)
  * service[gitaly] action nothing (skipped due to action :nothing)
  * runit_service[gitaly] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/gitaly] action create (up to date)
    * template[/opt/gitlab/sv/gitaly/run] action create (up to date)
    * directory[/opt/gitlab/sv/gitaly/log] action create (up to date)
    * directory[/opt/gitlab/sv/gitaly/log/main] action create (up to date)
    * template[/opt/gitlab/sv/gitaly/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_gitaly] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/gitaly/config] action create (up to date)
    * template[/opt/gitlab/sv/gitaly/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/gitaly/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for gitaly service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/gitaly/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/gitaly/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/gitaly/control] action create (up to date)
    * link[/opt/gitlab/init/gitaly] action create (up to date)
    * file[/opt/gitlab/sv/gitaly/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/gitaly] action create (up to date)
    * ruby_block[wait for gitaly service socket] action run (skipped due to not_if)
     (up to date)
  * version_file[Create version file for Gitaly] action create
    * file[/var/opt/gitlab/gitaly/VERSION] action create (up to date)
     (up to date)
  * version_file[Create Ruby version file for Gitaly] action create
    * file[/var/opt/gitlab/gitaly/RUBY_VERSION] action create (up to date)
     (up to date)
  * consul_service[gitaly] action delete
    * file[/var/opt/gitlab/consul/config.d/gitaly-service.json] action delete (up to date)
     (up to date)
Recipe: postgresql::bin
  * ruby_block[check_postgresql_version] action run (skipped due to not_if)
  * ruby_block[check_postgresql_version_is_deprecated] action run (skipped due to not_if)
  * ruby_block[Link postgresql bin files to the correct version] action run (skipped due to only_if)
  * template[/opt/gitlab/etc/gitlab-psql-rc] action create (up to date)
Recipe: postgresql::user
  * account[Postgresql user and group] action create (up to date)
  * directory[/var/opt/gitlab/postgresql] action create (up to date)
  * file[/var/opt/gitlab/postgresql/.profile] action create (up to date)
Recipe: postgresql::sysctl
  * gitlab_sysctl[kernel.shmmax] action create
    * directory[create /etc/sysctl.d for kernel.shmmax] action create (skipped due to only_if)
    * file[create /opt/gitlab/embedded/etc/90-omnibus-gitlab-kernel.shmmax.conf kernel.shmmax] action create (skipped due to only_if)
    * link[/etc/sysctl.d/90-omnibus-gitlab-kernel.shmmax.conf] action create (skipped due to only_if)
    * execute[load sysctl conf kernel.shmmax] action nothing (skipped due to action :nothing)
     (up to date)
  * gitlab_sysctl[kernel.shmall] action create
    * directory[create /etc/sysctl.d for kernel.shmall] action create (skipped due to only_if)
    * file[create /opt/gitlab/embedded/etc/90-omnibus-gitlab-kernel.shmall.conf kernel.shmall] action create (skipped due to only_if)
    * link[/etc/sysctl.d/90-omnibus-gitlab-kernel.shmall.conf] action create (skipped due to only_if)
    * execute[load sysctl conf kernel.shmall] action nothing (skipped due to action :nothing)
     (up to date)
  * gitlab_sysctl[kernel.sem] action create
    * directory[create /etc/sysctl.d for kernel.sem] action create (skipped due to only_if)
    * file[create /opt/gitlab/embedded/etc/90-omnibus-gitlab-kernel.sem.conf kernel.sem] action create (skipped due to only_if)
    * link[/etc/sysctl.d/90-omnibus-gitlab-kernel.sem.conf] action create (skipped due to only_if)
    * execute[load sysctl conf kernel.sem] action nothing (skipped due to action :nothing)
     (up to date)
Recipe: postgresql::enable
  * directory[/var/opt/gitlab/postgresql] action create (up to date)
  * directory[/var/opt/gitlab/postgresql/data] action create (up to date)
  * directory[/var/log/gitlab/postgresql] action create (up to date)
  * directory[/var/opt/gitlab/postgresql/data] action create (up to date)
  * execute[/opt/gitlab/embedded/bin/initdb -D /var/opt/gitlab/postgresql/data -E UTF8] action run (skipped due to not_if)
  * file[/var/opt/gitlab/postgresql/data/server.crt] action create (up to date)
  * file[/var/opt/gitlab/postgresql/data/server.key] action create (up to date)
  * postgresql_config[gitlab] action create
    * template[/var/opt/gitlab/postgresql/data/postgresql.conf] action create (up to date)
    * template[/var/opt/gitlab/postgresql/data/runtime.conf] action create (up to date)
    * template[/var/opt/gitlab/postgresql/data/pg_hba.conf] action create (up to date)
    * template[/var/opt/gitlab/postgresql/data/pg_ident.conf] action create (up to date)
     (up to date)
Recipe: postgresql::standalone
  * service[postgresql] action nothing (skipped due to action :nothing)
  * runit_service[postgresql] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/postgresql] action create (up to date)
    * template[/opt/gitlab/sv/postgresql/run] action create (up to date)
    * directory[/opt/gitlab/sv/postgresql/log] action create (up to date)
    * directory[/opt/gitlab/sv/postgresql/log/main] action create (up to date)
    * template[/opt/gitlab/sv/postgresql/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_postgresql] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/postgresql/config] action create (up to date)
    * template[/opt/gitlab/sv/postgresql/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/postgresql/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for postgresql service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/postgresql/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/postgresql/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/postgresql/control] action create (up to date)
    * template[/opt/gitlab/sv/postgresql/control/t] action create (up to date)
    * link[/opt/gitlab/init/postgresql] action create (up to date)
    * file[/opt/gitlab/sv/postgresql/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/postgresql] action create (up to date)
    * ruby_block[wait for postgresql service socket] action run (skipped due to not_if)
    * directory[/opt/gitlab/service/postgresql/supervise] action create (up to date)
    * directory[/opt/gitlab/service/postgresql/log/supervise] action create (up to date)
    * file[/opt/gitlab/service/postgresql/supervise/ok] action touch (skipped due to only_if)
    * file[/opt/gitlab/service/postgresql/log/supervise/ok] action touch (skipped due to only_if)
    * file[/opt/gitlab/service/postgresql/supervise/status] action touch (skipped due to only_if)
    * file[/opt/gitlab/service/postgresql/log/supervise/status] action touch
      - change owner from 'root' to 'gitlab-psql'
      - change group from 'root' to 'gitlab-psql'
      - update utime on file /opt/gitlab/service/postgresql/log/supervise/status
    * file[/opt/gitlab/service/postgresql/supervise/control] action touch (skipped due to only_if)
    * file[/opt/gitlab/service/postgresql/log/supervise/control] action touch (skipped due to only_if)
  
  * database_objects[postgresql] action create
    * postgresql_user[gitlab] action create
      * execute[create gitlab postgresql user] action run (skipped due to not_if)
       (up to date)
    * postgresql_user[gitlab_replicator] action create
      * execute[create gitlab_replicator postgresql user] action run (skipped due to not_if)
      * execute[set options for gitlab_replicator postgresql user] action run (skipped due to not_if)
       (up to date)
    * postgresql_database[gitlabhq_production] action create
      * execute[create database gitlabhq_production] action run (skipped due to not_if)
       (up to date)
    * postgresql_extension[pg_trgm] action enable
      * postgresql_query[enable pg_trgm extension] action run (skipped due to only_if)
       (up to date)
    * postgresql_extension[btree_gist] action enable
      * postgresql_query[enable btree_gist extension] action run (skipped due to only_if)
       (up to date)
     (up to date)
  * ruby_block[warn pending postgresql restart] action run (skipped due to only_if)
  * execute[reload postgresql] action nothing (skipped due to action :nothing)
  * execute[start postgresql] action nothing (skipped due to action :nothing)
Recipe: praefect::disable
  * service[praefect] action nothing (skipped due to action :nothing)
  * runit_service[praefect] action disable
    * ruby_block[disable praefect] action run (skipped due to only_if)
     (up to date)
  * consul_service[praefect] action delete
    * file[/var/opt/gitlab/consul/config.d/praefect-service.json] action delete (up to date)
     (up to date)
Recipe: gitlab-kas::disable
  * service[gitlab-kas] action nothing (skipped due to action :nothing)
  * runit_service[gitlab-kas] action disable
    * ruby_block[disable gitlab-kas] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab::database_migrations
  * ruby_block[check remote PG version] action nothing (skipped due to action :nothing)
  * rails_migration[gitlab-rails] action run
    * bash[migrate gitlab-rails database] action run (skipped due to not_if)
     (up to date)
Recipe: crond::disable
  * service[crond] action nothing (skipped due to action :nothing)
  * runit_service[crond] action disable
    * ruby_block[disable crond] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab::puma
  * directory[/var/log/gitlab/puma] action create (up to date)
  * directory[/opt/gitlab/var/puma] action create (up to date)
  * directory[/var/opt/gitlab/gitlab-rails/sockets] action create (up to date)
  * puma_config[/var/opt/gitlab/gitlab-rails/etc/puma.rb] action create
    * directory[/var/opt/gitlab/gitlab-rails/etc] action create (up to date)
    * template[/var/opt/gitlab/gitlab-rails/etc/puma.rb] action create (up to date)
     (up to date)
  * service[puma] action nothing (skipped due to action :nothing)
  * runit_service[puma] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/puma] action create (up to date)
    * template[/opt/gitlab/sv/puma/run] action create (up to date)
    * directory[/opt/gitlab/sv/puma/log] action create (up to date)
    * directory[/opt/gitlab/sv/puma/log/main] action create (up to date)
    * template[/opt/gitlab/sv/puma/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_puma] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/puma/config] action create (up to date)
    * template[/opt/gitlab/sv/puma/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/puma/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for puma service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/puma/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/puma/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/puma/control] action create (up to date)
    * template[/opt/gitlab/sv/puma/control/t] action create (up to date)
    * template[/opt/gitlab/sv/puma/control/h] action create (up to date)
    * link[/opt/gitlab/init/puma] action create (up to date)
    * file[/opt/gitlab/sv/puma/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/puma] action create (up to date)
    * ruby_block[wait for puma service socket] action run (skipped due to not_if)
     (up to date)
  * consul_service[rails] action delete
    * file[/var/opt/gitlab/consul/config.d/rails-service.json] action delete (up to date)
     (up to date)
  * gitlab_sysctl[net.core.somaxconn] action create
    * directory[create /etc/sysctl.d for net.core.somaxconn] action create (skipped due to only_if)
    * file[create /opt/gitlab/embedded/etc/90-omnibus-gitlab-net.core.somaxconn.conf net.core.somaxconn] action create (skipped due to only_if)
    * link[/etc/sysctl.d/90-omnibus-gitlab-net.core.somaxconn.conf] action create (skipped due to only_if)
    * execute[load sysctl conf net.core.somaxconn] action nothing (skipped due to action :nothing)
     (up to date)
Recipe: gitlab::sidekiq
  * sidekiq_service[sidekiq] action enable
    * directory[/var/log/gitlab/sidekiq] action create (up to date)
  Recipe: <Dynamically Defined Resource>
    * service[sidekiq] action nothing (skipped due to action :nothing)
    * runit_service[sidekiq] action enable
      * ruby_block[restart_service] action nothing (skipped due to action :nothing)
      * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
      * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
      * directory[/opt/gitlab/sv/sidekiq] action create (up to date)
      * template[/opt/gitlab/sv/sidekiq/run] action create (up to date)
      * directory[/opt/gitlab/sv/sidekiq/log] action create (up to date)
      * directory[/opt/gitlab/sv/sidekiq/log/main] action create (up to date)
      * template[/opt/gitlab/sv/sidekiq/log/config] action create (up to date)
      * ruby_block[verify_chown_persisted_on_sidekiq] action nothing (skipped due to action :nothing)
      * link[/var/log/gitlab/sidekiq/config] action create (up to date)
      * template[/opt/gitlab/sv/sidekiq/log/run] action create (up to date)
      * directory[/opt/gitlab/sv/sidekiq/env] action create (up to date)
      * ruby_block[Delete unmanaged env files for sidekiq service] action run (skipped due to only_if)
      * template[/opt/gitlab/sv/sidekiq/check] action create (skipped due to only_if)
      * template[/opt/gitlab/sv/sidekiq/finish] action create (skipped due to only_if)
      * directory[/opt/gitlab/sv/sidekiq/control] action create (up to date)
      * link[/opt/gitlab/init/sidekiq] action create (up to date)
      * file[/opt/gitlab/sv/sidekiq/down] action nothing (skipped due to action :nothing)
      * directory[/opt/gitlab/service] action create (up to date)
      * link[/opt/gitlab/service/sidekiq] action create (up to date)
      * ruby_block[wait for sidekiq service socket] action run (skipped due to not_if)
       (up to date)
     (up to date)
Recipe: gitlab::sidekiq
  * consul_service[sidekiq] action delete
    * file[/var/opt/gitlab/consul/config.d/sidekiq-service.json] action delete (up to date)
     (up to date)
Recipe: gitlab::gitlab-workhorse
  * directory[/var/opt/gitlab/gitlab-workhorse] action create (up to date)
  * directory[/var/opt/gitlab/gitlab-workhorse/sockets] action create (up to date)
  * directory[/var/log/gitlab/gitlab-workhorse] action create (up to date)
  * directory[/opt/gitlab/etc/gitlab-workhorse] action create (up to date)
  * env_dir[/opt/gitlab/etc/gitlab-workhorse/env] action create
    * directory[/opt/gitlab/etc/gitlab-workhorse/env] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-workhorse/env/PATH] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-workhorse/env/HOME] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-workhorse/env/SSL_CERT_DIR] action create (up to date)
     (up to date)
  * service[gitlab-workhorse] action nothing (skipped due to action :nothing)
  * runit_service[gitlab-workhorse] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/gitlab-workhorse] action create (up to date)
    * template[/opt/gitlab/sv/gitlab-workhorse/run] action create (up to date)
    * directory[/opt/gitlab/sv/gitlab-workhorse/log] action create (up to date)
    * directory[/opt/gitlab/sv/gitlab-workhorse/log/main] action create (up to date)
    * template[/opt/gitlab/sv/gitlab-workhorse/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_gitlab-workhorse] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/gitlab-workhorse/config] action create (up to date)
    * template[/opt/gitlab/sv/gitlab-workhorse/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/gitlab-workhorse/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for gitlab-workhorse service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/gitlab-workhorse/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/gitlab-workhorse/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/gitlab-workhorse/control] action create (up to date)
    * link[/opt/gitlab/init/gitlab-workhorse] action create (up to date)
    * file[/opt/gitlab/sv/gitlab-workhorse/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/gitlab-workhorse] action create (up to date)
    * ruby_block[wait for gitlab-workhorse service socket] action run (skipped due to not_if)
     (up to date)
  * consul_service[workhorse] action delete
    * file[/var/opt/gitlab/consul/config.d/workhorse-service.json] action delete (up to date)
     (up to date)
  * version_file[Create version file for Workhorse] action create
    * file[/var/opt/gitlab/gitlab-workhorse/VERSION] action create (up to date)
     (up to date)
  * template[/var/opt/gitlab/gitlab-workhorse/config.toml] action create (up to date)
Recipe: gitlab::mailroom_disable
  * service[mailroom] action nothing (skipped due to action :nothing)
  * runit_service[mailroom] action disable
    * ruby_block[disable mailroom] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab::nginx
  * directory[/var/opt/gitlab/nginx] action create (up to date)
  * directory[/var/opt/gitlab/nginx/conf] action create (up to date)
  * directory[/var/log/gitlab/nginx] action create (up to date)
  * link[/var/opt/gitlab/nginx/logs] action create (up to date)
  * template[/var/opt/gitlab/nginx/conf/gitlab-http.conf] action create (up to date)
  * template[/var/opt/gitlab/nginx/conf/gitlab-smartcard-http.conf] action delete (up to date)
  * template[/var/opt/gitlab/nginx/conf/gitlab-health.conf] action create (up to date)
  * template[/var/opt/gitlab/nginx/conf/gitlab-pages.conf] action delete (up to date)
  * template[/var/opt/gitlab/nginx/conf/gitlab-registry.conf] action delete (up to date)
  * template[/var/opt/gitlab/nginx/conf/gitlab-mattermost-http.conf] action delete (up to date)
  * template[/var/opt/gitlab/nginx/conf/nginx-status.conf] action create (up to date)
  * consul_service[nginx] action delete
    * file[/var/opt/gitlab/consul/config.d/nginx-service.json] action delete (up to date)
     (up to date)
  * template[/var/opt/gitlab/nginx/conf/nginx.conf] action create (up to date)
Recipe: nginx::enable
  * service[nginx] action nothing (skipped due to action :nothing)
  * runit_service[nginx] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/nginx] action create (up to date)
    * template[/opt/gitlab/sv/nginx/run] action create (up to date)
    * directory[/opt/gitlab/sv/nginx/log] action create (up to date)
    * directory[/opt/gitlab/sv/nginx/log/main] action create (up to date)
    * template[/opt/gitlab/sv/nginx/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_nginx] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/nginx/config] action create (up to date)
    * template[/opt/gitlab/sv/nginx/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/nginx/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for nginx service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/nginx/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/nginx/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/nginx/control] action create (up to date)
    * link[/opt/gitlab/init/nginx] action create (up to date)
    * file[/opt/gitlab/sv/nginx/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/nginx] action create (up to date)
    * ruby_block[wait for nginx service socket] action run (skipped due to not_if)
     (up to date)
  * execute[reload nginx] action nothing (skipped due to action :nothing)
Recipe: gitlab::remote-syslog_disable
  * service[remote-syslog] action nothing (skipped due to action :nothing)
  * runit_service[remote-syslog] action disable
    * ruby_block[disable remote-syslog] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab::storage-check_disable
  * service[storage-check] action nothing (skipped due to action :nothing)
  * runit_service[storage-check] action disable
    * ruby_block[disable storage-check] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab-pages::disable
  * service[gitlab-pages] action nothing (skipped due to action :nothing)
  * runit_service[gitlab-pages] action disable
    * ruby_block[disable gitlab-pages] action run (skipped due to only_if)
     (up to date)
Recipe: registry::disable
  * service[registry] action nothing (skipped due to action :nothing)
  * runit_service[registry] action disable
    * ruby_block[disable registry] action run (skipped due to only_if)
     (up to date)
Recipe: mattermost::disable
  * service[mattermost] action nothing (skipped due to action :nothing)
  * runit_service[mattermost] action disable
    * ruby_block[disable mattermost] action run (skipped due to only_if)
     (up to date)
Recipe: letsencrypt::disable
  * crond_job[letsencrypt-renew] action delete
    * file[/var/opt/gitlab/crond/letsencrypt-renew] action delete (up to date)
     (up to date)
Recipe: gitlab::gitlab-healthcheck
  * template[/opt/gitlab/etc/gitlab-healthcheck-rc] action create (up to date)
Recipe: monitoring::pgbouncer-exporter_disable
  * service[pgbouncer-exporter] action nothing (skipped due to action :nothing)
  * runit_service[pgbouncer-exporter] action disable
    * ruby_block[disable pgbouncer-exporter] action run (skipped due to only_if)
     (up to date)
Recipe: monitoring::node-exporter_disable
  * service[node-exporter] action nothing (skipped due to action :nothing)
  * runit_service[node-exporter] action disable
    * ruby_block[disable node-exporter] action run (skipped due to only_if)
     (up to date)
  * consul_service[node-exporter] action delete
    * file[/var/opt/gitlab/consul/config.d/node-exporter-service.json] action delete (up to date)
     (up to date)
Recipe: monitoring::gitlab-exporter
  * directory[/var/opt/gitlab/gitlab-exporter] action create (up to date)
  * directory[/var/log/gitlab/gitlab-exporter] action create (up to date)
  * env_dir[/opt/gitlab/etc/gitlab-exporter/env] action create
    * directory[/opt/gitlab/etc/gitlab-exporter/env] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-exporter/env/LD_PRELOAD] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-exporter/env/MALLOC_CONF] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-exporter/env/RUBY_GC_HEAP_INIT_SLOTS] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-exporter/env/RUBY_GC_HEAP_FREE_SLOTS_MIN_RATIO] action create (up to date)
    * file[/opt/gitlab/etc/gitlab-exporter/env/RUBY_GC_HEAP_FREE_SLOTS_MAX_RATIO] action create (up to date)
     (up to date)
  * template[/var/opt/gitlab/gitlab-exporter/gitlab-exporter.yml] action create (up to date)
  * version_file[Create version file for GitLab-Exporter] action create
    * file[/var/opt/gitlab/gitlab-exporter/RUBY_VERSION] action create (up to date)
     (up to date)
  * service[gitlab-exporter] action nothing (skipped due to action :nothing)
  * runit_service[gitlab-exporter] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/gitlab-exporter] action create (up to date)
    * template[/opt/gitlab/sv/gitlab-exporter/run] action create (up to date)
    * directory[/opt/gitlab/sv/gitlab-exporter/log] action create (up to date)
    * directory[/opt/gitlab/sv/gitlab-exporter/log/main] action create (up to date)
    * template[/opt/gitlab/sv/gitlab-exporter/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_gitlab-exporter] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/gitlab-exporter/config] action create (up to date)
    * template[/opt/gitlab/sv/gitlab-exporter/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/gitlab-exporter/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for gitlab-exporter service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/gitlab-exporter/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/gitlab-exporter/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/gitlab-exporter/control] action create (up to date)
    * link[/opt/gitlab/init/gitlab-exporter] action create (up to date)
    * file[/opt/gitlab/sv/gitlab-exporter/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/gitlab-exporter] action create (up to date)
    * ruby_block[wait for gitlab-exporter service socket] action run (skipped due to not_if)
     (up to date)
  * consul_service[gitlab-exporter] action delete
    * file[/var/opt/gitlab/consul/config.d/gitlab-exporter-service.json] action delete (up to date)
     (up to date)
Recipe: monitoring::redis-exporter
  * directory[/var/log/gitlab/redis-exporter] action create (up to date)
  * directory[/opt/gitlab/etc/redis-exporter/env] action create (up to date)
  * env_dir[/opt/gitlab/etc/redis-exporter/env] action create
    * directory[/opt/gitlab/etc/redis-exporter/env] action create (up to date)
    * file[/opt/gitlab/etc/redis-exporter/env/SSL_CERT_DIR] action create (up to date)
     (up to date)
  * service[redis-exporter] action nothing (skipped due to action :nothing)
  * runit_service[redis-exporter] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/redis-exporter] action create (up to date)
    * template[/opt/gitlab/sv/redis-exporter/run] action create (up to date)
    * directory[/opt/gitlab/sv/redis-exporter/log] action create (up to date)
    * directory[/opt/gitlab/sv/redis-exporter/log/main] action create (up to date)
    * template[/opt/gitlab/sv/redis-exporter/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_redis-exporter] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/redis-exporter/config] action create (up to date)
    * template[/opt/gitlab/sv/redis-exporter/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/redis-exporter/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for redis-exporter service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/redis-exporter/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/redis-exporter/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/redis-exporter/control] action create (up to date)
    * link[/opt/gitlab/init/redis-exporter] action create (up to date)
    * file[/opt/gitlab/sv/redis-exporter/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/redis-exporter] action create (up to date)
    * ruby_block[wait for redis-exporter service socket] action run (skipped due to not_if)
     (up to date)
  * consul_service[redis-exporter] action delete
    * file[/var/opt/gitlab/consul/config.d/redis-exporter-service.json] action delete (up to date)
     (up to date)
Recipe: monitoring::user
  * account[Prometheus user and group] action create (up to date)
Recipe: monitoring::prometheus
  * directory[/var/opt/gitlab/prometheus] action create (up to date)
  * directory[/var/opt/gitlab/prometheus/rules] action create (up to date)
  * directory[/var/log/gitlab/prometheus] action create (up to date)
  * directory[/opt/gitlab/etc/prometheus/env] action create (up to date)
  * env_dir[/opt/gitlab/etc/prometheus/env] action create
    * directory[/opt/gitlab/etc/prometheus/env] action create (up to date)
    * file[/opt/gitlab/etc/prometheus/env/SSL_CERT_DIR] action create (up to date)
     (up to date)
  * execute[reload prometheus] action nothing (skipped due to action :nothing)
  * file[Prometheus config] action create (up to date)
  * service[prometheus] action nothing (skipped due to action :nothing)
  * runit_service[prometheus] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/prometheus] action create (up to date)
    * template[/opt/gitlab/sv/prometheus/run] action create (up to date)
    * directory[/opt/gitlab/sv/prometheus/log] action create (up to date)
    * directory[/opt/gitlab/sv/prometheus/log/main] action create (up to date)
    * template[/opt/gitlab/sv/prometheus/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_prometheus] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/prometheus/config] action create (up to date)
    * template[/opt/gitlab/sv/prometheus/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/prometheus/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for prometheus service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/prometheus/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/prometheus/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/prometheus/control] action create (up to date)
    * link[/opt/gitlab/init/prometheus] action create (up to date)
    * file[/opt/gitlab/sv/prometheus/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/prometheus] action create (up to date)
    * ruby_block[wait for prometheus service socket] action run (skipped due to not_if)
     (up to date)
  * consul_service[prometheus] action delete
    * file[/var/opt/gitlab/consul/config.d/prometheus-service.json] action delete (up to date)
     (up to date)
  * template[/var/opt/gitlab/prometheus/rules/gitlab.rules] action create (up to date)
  * template[/var/opt/gitlab/prometheus/rules/node.rules] action create (up to date)
Recipe: monitoring::alertmanager
  * directory[/var/opt/gitlab/alertmanager] action create (up to date)
  * directory[/var/log/gitlab/alertmanager] action create (up to date)
  * directory[/opt/gitlab/etc/alertmanager/env] action create (up to date)
  * env_dir[/opt/gitlab/etc/alertmanager/env] action create
    * directory[/opt/gitlab/etc/alertmanager/env] action create (up to date)
    * file[/opt/gitlab/etc/alertmanager/env/SSL_CERT_DIR] action create (up to date)
     (up to date)
  * file[Alertmanager config] action create
    - update content in file /var/opt/gitlab/alertmanager/alertmanager.yml from 21b7be to d67d8a
    --- /var/opt/gitlab/alertmanager/alertmanager.yml   2021-12-03 05:11:12.278522959 +0000
    +++ /var/opt/gitlab/alertmanager/.chef-alertmanager20211208-13995-b7dkiu.yml    2021-12-08 00:11:30.334834793 +0000
    @@ -1,5 +1,7 @@
     ---
    -global: {}
    +global:
    +  smtp_from: gitlab@172.32.161.36
    +  smtp_smarthost: 172.28.121.10:25
     templates: []
     route:
       receiver: default-receiver
  * service[alertmanager] action nothing (skipped due to action :nothing)
  * runit_service[alertmanager] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/alertmanager] action create (up to date)
    * template[/opt/gitlab/sv/alertmanager/run] action create (up to date)
    * directory[/opt/gitlab/sv/alertmanager/log] action create (up to date)
    * directory[/opt/gitlab/sv/alertmanager/log/main] action create (up to date)
    * template[/opt/gitlab/sv/alertmanager/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_alertmanager] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/alertmanager/config] action create (up to date)
    * template[/opt/gitlab/sv/alertmanager/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/alertmanager/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for alertmanager service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/alertmanager/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/alertmanager/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/alertmanager/control] action create (up to date)
    * link[/opt/gitlab/init/alertmanager] action create (up to date)
    * file[/opt/gitlab/sv/alertmanager/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/alertmanager] action create (up to date)
    * ruby_block[wait for alertmanager service socket] action run (skipped due to not_if)
     (up to date)
Recipe: monitoring::postgres-exporter
  * directory[/var/log/gitlab/postgres-exporter] action create (up to date)
  * directory[/var/opt/gitlab/postgres-exporter] action create (up to date)
  * env_dir[/opt/gitlab/etc/postgres-exporter/env] action create
    * directory[/opt/gitlab/etc/postgres-exporter/env] action create (up to date)
    * file[/opt/gitlab/etc/postgres-exporter/env/SSL_CERT_DIR] action create (up to date)
    * file[/opt/gitlab/etc/postgres-exporter/env/DATA_SOURCE_NAME] action create (up to date)
     (up to date)
  * service[postgres-exporter] action nothing (skipped due to action :nothing)
  * runit_service[postgres-exporter] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/postgres-exporter] action create (up to date)
    * template[/opt/gitlab/sv/postgres-exporter/run] action create (up to date)
    * directory[/opt/gitlab/sv/postgres-exporter/log] action create (up to date)
    * directory[/opt/gitlab/sv/postgres-exporter/log/main] action create (up to date)
    * template[/opt/gitlab/sv/postgres-exporter/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_postgres-exporter] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/postgres-exporter/config] action create (up to date)
    * template[/opt/gitlab/sv/postgres-exporter/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/postgres-exporter/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for postgres-exporter service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/postgres-exporter/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/postgres-exporter/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/postgres-exporter/control] action create (up to date)
    * link[/opt/gitlab/init/postgres-exporter] action create (up to date)
    * file[/opt/gitlab/sv/postgres-exporter/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/postgres-exporter] action create (up to date)
    * ruby_block[wait for postgres-exporter service socket] action run (skipped due to not_if)
     (up to date)
  * template[/var/opt/gitlab/postgres-exporter/queries.yaml] action create (up to date)
  * consul_service[postgres-exporter] action delete
    * file[/var/opt/gitlab/consul/config.d/postgres-exporter-service.json] action delete (up to date)
     (up to date)
Recipe: monitoring::grafana
  * directory[/var/log/gitlab/grafana] action create (up to date)
  * directory[/var/opt/gitlab/grafana] action create (up to date)
  * directory[/var/opt/gitlab/grafana/provisioning] action create (up to date)
  * directory[/var/opt/gitlab/grafana/provisioning/dashboards] action create (up to date)
  * directory[/var/opt/gitlab/grafana/provisioning/datasources] action create (up to date)
  * directory[/var/opt/gitlab/grafana/provisioning/notifiers] action create (up to date)
  * file[/var/opt/gitlab/grafana/CVE_reset_status] action delete (up to date)
  * link[/var/opt/gitlab/grafana/conf] action create (up to date)
  * link[/var/opt/gitlab/grafana/public] action create (up to date)
  * directory[/opt/gitlab/etc/grafana/env] action create (up to date)
  * ruby_block[populate Grafana configuration options] action run
    - execute the ruby block populate Grafana configuration options
  * env_dir[/opt/gitlab/etc/grafana/env] action create
    * directory[/opt/gitlab/etc/grafana/env] action create (up to date)
    * file[/opt/gitlab/etc/grafana/env/SSL_CERT_DIR] action create (up to date)
     (up to date)
  * template[/var/opt/gitlab/grafana/grafana.ini] action create (up to date)
  * file[/var/opt/gitlab/grafana/provisioning/dashboards/gitlab_dashboards.yml] action create (up to date)
  * file[/var/opt/gitlab/grafana/provisioning/datasources/gitlab_datasources.yml] action create (up to date)
  * service[grafana] action nothing (skipped due to action :nothing)
  * runit_service[grafana] action enable
    * ruby_block[restart_service] action nothing (skipped due to action :nothing)
    * ruby_block[restart_log_service] action nothing (skipped due to action :nothing)
    * ruby_block[reload_log_service] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/sv/grafana] action create (up to date)
    * template[/opt/gitlab/sv/grafana/run] action create (up to date)
    * directory[/opt/gitlab/sv/grafana/log] action create (up to date)
    * directory[/opt/gitlab/sv/grafana/log/main] action create (up to date)
    * template[/opt/gitlab/sv/grafana/log/config] action create (up to date)
    * ruby_block[verify_chown_persisted_on_grafana] action nothing (skipped due to action :nothing)
    * link[/var/log/gitlab/grafana/config] action create (up to date)
    * template[/opt/gitlab/sv/grafana/log/run] action create (up to date)
    * directory[/opt/gitlab/sv/grafana/env] action create (up to date)
    * ruby_block[Delete unmanaged env files for grafana service] action run (skipped due to only_if)
    * template[/opt/gitlab/sv/grafana/check] action create (skipped due to only_if)
    * template[/opt/gitlab/sv/grafana/finish] action create (skipped due to only_if)
    * directory[/opt/gitlab/sv/grafana/control] action create (up to date)
    * link[/opt/gitlab/init/grafana] action create (up to date)
    * file[/opt/gitlab/sv/grafana/down] action nothing (skipped due to action :nothing)
    * directory[/opt/gitlab/service] action create (up to date)
    * link[/opt/gitlab/service/grafana] action create (up to date)
    * ruby_block[wait for grafana service socket] action run (skipped due to not_if)
     (up to date)
Recipe: gitlab::database_reindexing_disable
  * crond_job[database-reindexing] action delete
    * file[/var/opt/gitlab/crond/database-reindexing] action delete (up to date)
     (up to date)
Recipe: gitlab-ee::sentinel_disable
  * sentinel_service[redis] action disable
  Recipe: <Dynamically Defined Resource>
    * service[sentinel] action nothing (skipped due to action :nothing)
    * runit_service[sentinel] action disable
      * ruby_block[disable sentinel] action run (skipped due to only_if)
       (up to date)
    * file[/var/opt/gitlab/sentinel/sentinel.conf] action delete (up to date)
    * directory[/var/opt/gitlab/sentinel] action delete (up to date)
     (up to date)
Recipe: gitlab-ee::geo-postgresql_disable
  * service[geo-postgresql] action nothing (skipped due to action :nothing)
  * runit_service[geo-postgresql] action disable
    * ruby_block[disable geo-postgresql] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab-ee::geo-logcursor_disable
  * service[geo-logcursor] action nothing (skipped due to action :nothing)
  * runit_service[geo-logcursor] action disable
    * ruby_block[disable geo-logcursor] action run (skipped due to only_if)
     (up to date)
Recipe: consul::disable_daemon
  * service[consul] action nothing (skipped due to action :nothing)
  * runit_service[consul] action disable
    * ruby_block[disable consul] action run (skipped due to only_if)
     (up to date)
Recipe: pgbouncer::disable
  * service[pgbouncer] action nothing (skipped due to action :nothing)
  * runit_service[pgbouncer] action disable
    * ruby_block[disable pgbouncer] action run (skipped due to only_if)
     (up to date)
Recipe: patroni::disable
  * service[patroni] action nothing (skipped due to action :nothing)
  * runit_service[patroni] action disable
    * ruby_block[disable patroni] action run (skipped due to only_if)
     (up to date)
Recipe: gitlab-ee::geo-secondary_disable
  * templatesymlink[Removes database_geo.yml symlink] action delete
    * file[/var/opt/gitlab/gitlab-rails/etc/database_geo.yml] action delete (up to date)
    * link[/opt/gitlab/embedded/service/gitlab-rails/config/database_geo.yml] action delete (up to date)
     (up to date)
Recipe: gitlab::puma
  * runit_service[puma] action restart (up to date)
Recipe: gitlab::sidekiq
  * sidekiq_service[sidekiq] action restart
  Recipe: <Dynamically Defined Resource>
    * service[sidekiq] action nothing (skipped due to action :nothing)
    * runit_service[sidekiq] action restart (up to date)
     (up to date)
Recipe: monitoring::alertmanager
  * runit_service[alertmanager] action restart (up to date)
 
Running handlers:
Running handlers complete
Chef Infra Client finished, 7/760 resources updated in 16 seconds
 
Notes:
Found old initial root password file at /etc/gitlab/initial_root_password and deleted it.
 
gitlab Reconfigured!
root@docker:/etc/gitlab#
Code Block 108 gitlab-ctl reconfigure

SMTP 전송 테스트
gitlab 콘솔 접속 및 메일 발송 테스트 정보 입력
Notify.test_email('<받을사람주소>','<제목>','<메일 내용>').deliver_now
root@docker:/etc/gitlab# gitlab-rails console
--------------------------------------------------------------------------------
 Ruby:         ruby 2.7.4p191 (2021-07-07 revision a21a3b7d23) [x86_64-linux]
 GitLab:       14.5.1-ee (cd2049cb286) EE
 GitLab Shell: 13.22.1
 PostgreSQL:   12.7
--------------------------------------------------------------------------------
Loading production environment (Rails 6.1.4.1)
irb(main):001:0> Notify.test_email('hsyou@nicepay.co.kr','test mail','test mail contents').deliver_now
Delivered mail 61b00fc715dcb_61c75a509850@docker.nicepay.co.kr.mail (142.1ms)
=> #<Mail::Message:176220, Multipart: false, Headers: <Date: Wed, 08 Dec 2021 01:52:07 +0000>, 
<From: GitLab <gitlab@172.32.161.36>>, 
<Reply-To: GitLab <noreply@172.32.161.36>>, 
<To: hsyou@nicepay.co.kr>, 
<Message-ID: <61b00fc715dcb_61c75a509850@docker.nicepay.co.kr.mail>>, 
<Subject: test mail>, 
<Mime-Version: 1.0>, 
<Content-Type: text/html; charset=UTF-8>, 
<Content-Transfer-Encoding: 7bit>, 
<Auto-Submitted: auto-generated>, 
<X-Auto-Response-Suppress: All>>
irb(main):002:0> 

[Gitlab] 계정관리
root 계정을 통한 사용자 계정관리 방법을 안내합니다.


•	사용자 등록(root 사용자로만 가능)
•	등록 요청 사용자 허가
•	사용자 등록 시 확인 이메일 보내는 방법
•	사용자 조회
•	사용자 삭제
•	CUI 를 통한 패스워드 변경(및 초기화)
사용자 등록(root 사용자로만 가능)
Menu-Admin 이동
 
Admin Area-Overview-User 화면
 
New user 
 
필수정보 등록 및 create user
Name : gitlab 내에서 표시되는 이름
Username : 사용자 ID
 
등록확인
 
등록 요청 사용자 허가
Menu-Admin 이동
 
Admin Area-Overview-User 화면
 
Pending approval 탭 확인 및 대상자 Approve 선택
 
 
사용자 등록 시 확인 이메일 보내는 방법
Admin Area - Settings - General 메뉴 이동
Sign-up restrictions 확장
Send confirmation email on sign-up 를 체크하고 저장

 

사용자 조회
Admin Area-Overview-Users 화면
 

사용자 삭제
Admin Area-Overview-Users 화면
 
대상 사용자 선택 후 Delete User 수행
 
 

CUI 를 통한 패스워드 변경(및 초기화)

[docker@almt01 docker]$ docker exec -it gitlab /bin/bash 
root@docker:/# gitlab-rails console -e production 
-------------------------------------------------------------------------------- 
Ruby: ruby 2.7.4p191 (2021-07-07 revision a21a3b7d23) [x86_64-linux] 
GitLab: 14.5.1-ee (cd2049cb286) EE 
GitLab Shell: 13.22.1 
PostgreSQL: 12.7 
-------------------------------------------------------------------------------- 
Loading production environment (Rails 6.1.4.1) 
irb(main):001:0> user = User.where(id:1).first => #<User id:1 @root> 
irb(main):002:0> user.password='skdltm100%' => "skdltm100%" 
irb(main):003:0> user.password_confirmation='skdltm100%' => "skdltm100%" 
irb(main):004:0> user.save Enqueued ActionMailer::MailDeliveryJob (Job ID: b2589372-a30c-4fcb-ac4b-7f1a56c1dfac) to Sidekiq(mailers) 
with arguments: "DeviseMailer", "password_change", "deliver_now", {:args=>[#<GlobalID:0x00007f2c359e5288 @uri=#<URI::GID gid://gitlab/User/1>>]} => true 
irb(main):005:0>
Code Block 109 gitlab root password setup

[Gitlab] 사용자 가이드
•	[Gitlab] 계정 만들기
•	[Gitlab] Gitlab 에 ssh key 적용
•	[Gitlab] 그룹
•	[Gitlab] 프로젝트
[Gitlab] 계정 만들기
계정발급-개인생성

개인이 생성 요청 시 별도 이메일 등의 수단을 통한 계정 활성화 단계가 없습니다.

Register now 클릭
 
등록 사용자 정보 입력
 
관리자의 승인 대기
관리자 가 승인하지 않을 경우 아래와 같이 메시지가 발생합니다.
 
최초 정보 입력
로그인 후 최초 정보 등록(어떤 정보를 입력해도 상관없음)
 
계정 발급-관리자생성
계정관리-사용자 등록 참고
계정 활성화

업무망에서 gitlab 에 접근 불가하기 때문에 현재 계정 활성화 기능을 disable 했습니다.

이메일 확인 후 링크 클릭
 
[Gitlab] Gitlab 에 ssh key 적용

•	Gitlab 에 Eclipse 의 ssh key 적용
Gitlab 에 Eclipse 의 ssh key 적용
사용자명-Preferences 클릭, User Settings 메뉴의 SSH Keys 선택 (Eclipse 에서 ssh key 생성)
 

SSH Keys 내 Key 에 해당 키 입력 후 Title 설정
 

 
[Gitlab] 그룹
Gitlab 메뉴 중 Group 안내입니다.


•	Gitlab 의 그룹이란?
•	그룹 조회
•	그룹 참가
o	그룹 참가 요청
o	그룹 사용자 등록
o	그룹 참가 허용
•	그룹 생성
•	그룹 수정
•	그룹 삭제
Gitlab 의 그룹이란?
사용자들과 프로젝트를 관리하기 위한 기능
여러 프로젝트의 묶음이며 기본적으로 private 속성으로 생성
그룹 조회
Groups-Your groups 선택
 
조회할 대상 그룹선택
 
공개 (Public)또는 내부(Internal) 그룹은 검색되지만, 개인 그룹은 검색되지 않습니다.
그룹 참가
그룹 참가 요청
그룹 선택 후 Request Access 클릭
 

그룹 사용자 등록
그룹 내 Group information - Members 선택
 
Invite member 에서 사용자 검색 후 등록
역할과 기간을 지정해서 허용할 수 있음
 
그룹 참가 허용
그룹 내 Group information - Members 선택
 
Access requests 선택
역할과 기간을 지정해서 허용할 수 있음
 
그룹 생성
Groups-Create group 선택
 
그룹 이름 및 기타 정보 입력 후 Create group 등록
 
그룹 수정

그룹 메뉴 내에서 진행합니다.

Settings - General
 
그룹 이름/설명/아바타 및 노출 변경
 
그룹 권한 및 대용량 파일 push 를 위한 LFS 설정
100mb 이상 파일 push 시를 위해 LFS(Large File Storage) 를 사용해야 하며, 이를 위해 저장소 별 LFS 로 변경이 가능합니다.

 
그룹 삭제

그룹 메뉴 내에서 진행합니다.

Settings - General
 
Advanced - Expand
 
Remove group 의 Remove group 클릭하고 그룹 이름 입력
 
[Gitlab] 프로젝트
Gitlab 메뉴 중 Projects 안내입니다.


•	Gitlab 의 프로젝트란?
•	프로젝트 조회
•	프로젝트 생성 
•	프로젝트 수정
•	프로젝트 삭제
Gitlab 의 프로젝트란?
소스코드를 관리하는 기본적인 단위
프로젝트 조회
Projects -Your projects 선택
 
전체(All) 및 내 프로젝트(Personal) 조회
 
프로젝트 생성 
Projects -Create new projects 선택
 
프로젝트 생성 방법 선택
 
Create blank project - 빈 프로젝트 만들기
프로젝트 내용 구성
사용자 또는 그룹 선택
 
구성된 프로젝트 확인
 
Create from template - 템플릿을 이용한 프로젝트 만들기
Ruby on Rails, Spring 등 구성된 템플릿을 활용해서 프로젝트 생성 가능(Preview 는 외부 인터넷 연결되어야 확인 가능합니다.)
 
원하는 템플릿 선택 후 프로젝트 내용 구성
사용자 또는 그룹 선택
 
구성된 프로젝트 확인
 
Import project - 외부 프로젝트 가져오기
GitLab, Gitlab.com(클라우드) github, Bitbucket Cloud, Bitbucket Server, FogBugz, Gitea, URL 을 통한 공유, Manifest file 을 통한 가져오기, Phabricator Tasks 를 지원함
 
프로젝트 수정

프로젝트 메뉴 내에서 진행합니다.

Settings - General
 
프로젝트 위치(그룹→개인 또는 개인→그룹)  변경
Advanced - Expand 에서 Transfer project 의 namespace 변경
 
변경 후 confirm 수행
 
프로젝트 삭제

프로젝트 메뉴 내에서 진행합니다.

Settings - General
 
Advanced - Expand
 
Delete project 의 delete project 클릭하고 프로젝트 이름 입력
 
[Gitlab] 기타
[Gitlab] Eclipse 에서 git 다루기

•	[Eclipse] Git repositories Perspective 열기
•	[Eclipse] ssh key 생성
•	[Eclipse] 특정 프로젝트를 로컬 저장소(Git Local Repository) 에 생성하고 commit 하기
o	로컬 저장소(Git Local Repository) 만들기
o	로컬 저장소(Git Local Repository) 에 commit 하기
o	git Remote Repository 로 push 하기
•	[Eclipse] git Remote(Clone) 를 Eclipse Git repositories Perspective 에 등록하기
•	[Eclipse] 프로젝트 git disconnect (저장소 삭제하지 않음)
[Eclipse] Git repositories Perspective 열기
window - Perspective - Open Perspective - Other 선택하기
 
Git Perspective 선택
 
[Eclipse] ssh key 생성
Windows-Preferences-General-Network Connection-SSH2 메뉴 이동
Key Management 탭 선택
 
Generate RSA Key... 버튼 클릭
Save Private Key... 버튼 클릭
 
C:\Users\사용자명\.ssh 이동해서 id_rsa.pub 파일 열어 Key 복사
 
[Eclipse] 특정 프로젝트를 로컬 저장소(Git Local Repository) 에 생성하고 commit 하기
로컬 저장소(Git Local Repository) 만들기
프로젝트 오른클릭 후 Team-Share Project 선택
 
Share Project 를 Git 로 선택
 
Use or create repository in parent folder of project 선택
 

Create Repository 버튼 클릭하여 생성 및 종료
로컬 저장소(Git Local Repository) 에 commit 하기
프로젝트 오른클릭 후 Team-Commit 선택
 
Unstaged Changes 에서 commit 할 파일을 선택하여 add to index 또는 드래그 앤 드롭으로 Staged Changes 에 이동
 

commit 버튼 클릭(메시지 필수)
git Remote Repository 로 push 하기
프로젝트 오른클릭 후 Team-Remote-Push 선택
 

URI, Host, Repository path 등 등록
protocol (http) 선택 및 인증 정보 입력
 

필요 정보 입력 후 Add Spec 선택, Finish
 
완료 메시지 확인
 

Gitlab 에서 Commit 버전 확인
 
[Eclipse] git Remote(Clone) 를 Eclipse Git repositories Perspective 에 등록하기
Eclipse Git repositories  창에서 Clone a Git repository 선택
 
URI 에 정보 등록 및 git 사용자 계정 설정 (gitlab 에서 URL 정보 가져오기)
 
Branch 선택
 
Git Local Repository 선택 (로컬 저장소가 없을 경우 : Git Local Repository 만들기 )
 
프로젝트 import
 
Projects from Git 선택
 
Existing local reposutiry 로 로컬 저장소 선택
 
상황에 맞는 프로젝트 import 방법 선택 (테스트 프로젝트는 blank 프로젝트로 general project 로 구성)
 
정보 확인 후 종료 버튼 클릭
 
Eclipse 내에서 프로젝트 확인
 
[Eclipse] 프로젝트 git disconnect (저장소 삭제하지 않음)
프로젝트 오른클릭 후 Team-Disconnect 선택
 
[Gitlab] 기본적인 git 안내

•	git ?
•	git 의 기본 이해
o	Remote & Origin
o	Clone
o	Repository
•	git 기본 명령어
git ?
2005년 리누즈 토발즈가 만든 분산 버전 관리 시스템
리눅스 커널을 만들기 위해 분산 버전 관리 시스템인 BitKeeper 를 사용하고 있었는데, 유료화 되어 git 을 만들게 됨

git 의 기본 이해
Remote & Origin
Remote : 리모트 서버를 의미(github, gitlab, Bitbucket 등의 소스코드가 있는 서버)
내가 사용하는 리모트 서버를 부르는 말 : Origin
일반적으로 remote 와 origin 은 혼용해서 부르고는 함
Clone
소스코드를 복사해서 사용자의 컴퓨터로 받아오는 행위
받아온 소스코드를 리모트에 올리는 행위를 push, 서버의 소스를 내 컴퓨터로 받아오는  행위를 pull 또는 fetch 라고 부름
Repository
레파지토리(Repository, Repo, 저장소) 는 리모트 서버 내에서 구분되는 단위
일반적으로 하나의 프로젝트에 하나의 레파지토리를 두지만, 경우에 따라 여러개의 프로젝트를 구성하기 도 함
레파지토리를 clone 받을 때는 해당 레파지토리의 url 이 필요한데, 이때 맨 마지막에 .git 확장자를 붙여 구분함
git 기본 명령어
clone
pull & fetch
commit
push
[Gitlab] .gitignore
.gitignore
프로젝트 작업 시 로컬 환경의 정보나 빌드 정보 등 원격 저장소에 관리되지 말아야 하는 파일 들에 대해서 지정하여 원격 저장소에 push 되지 않도록 관리하는 파일
해당 파일에 대해서는 git track 되지 않음
로컬 환경에 종속적인 파일을 원격저장소에 올리지 않기 위해 작성
.gitignore 파일 정보
eclipse , java

# Created by https://www.toptal.com/developers/gitignore/api/eclipse,java
# Edit at https://www.toptal.com/developers/gitignore?templates=eclipse,java
 
### Eclipse ###
.metadata
bin/
tmp/
*.tmp
*.bak
*.swp
*~.nib
local.properties
.settings/
.loadpath
.recommenders
 
# External tool builders
.externalToolBuilders/
 
# Locally stored "Eclipse launch configurations"
*.launch
 
# PyDev specific (Python IDE for Eclipse)
*.pydevproject
 
# CDT-specific (C/C++ Development Tooling)
.cproject
 
# CDT- autotools
.autotools
 
# Java annotation processor (APT)
.factorypath
 
# PDT-specific (PHP Development Tools)
.buildpath
 
# sbteclipse plugin
.target
 
# Tern plugin
.tern-project
 
# TeXlipse plugin
.texlipse
 
# STS (Spring Tool Suite)
.springBeans
 
# Code Recommenders
.recommenders/
 
# Annotation Processing
.apt_generated/
.apt_generated_test/
 
# Scala IDE specific (Scala & Java development for Eclipse)
.cache-main
.scala_dependencies
.worksheet
 
# Uncomment this line if you wish to ignore the project description file.
# Typically, this file would be tracked if it contains build/dependency configurations:
#.project
 
### Eclipse Patch ###
# Spring Boot Tooling
.sts4-cache/
 
### Java ###
# Compiled class file
*.class
 
# Log file
*.log
 
# BlueJ files
*.ctxt
 
# Mobile Tools for Java (J2ME)
.mtj.tmp/
 
# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar
 
# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*
 
# End of https://www.toptal.com/developers/gitignore/api/eclipse,java
Code Block 110 .gitignore

_temp gitlab 학습하기
1.	gitlab을 위한 프로젝트 생성
2.	로컬 리파지토리 등록
3.	리모트에 리파지토리 생성
4.	파일 업로드
5.	티켓 만들기
6.	gitignore 구성
a.	다른 계정으로 프로젝트 remote
b.	수정 및 commit
7.	원래 계정에서 push

이클립스 / 프로젝트 - Team - Share Project
 
이클립스 / share project - Git 선택
 
로컬 저장소 생성
 
