---
layout: single                                
title: 폐쇄망 환경에서 grafana 설치하기
date: "2021-08-02 10:00:00 +0900"
toc : false
category: 오픈소스 사용기
tags: [VPN, opensource]
---

시작하면서
=============
오픈소스 메트릭 데이터 시각화 도구로, 메트릭 데이터에 대한 분석 및 대시보드 구성을 위해 사용되는 어플리케이션 입니다.
이전에 소개 드린 인플럭스 DB 와 연계성이 좋아 선택하게 되었습니다.

안내
=============
해당 가이드는 Red Hat Enterprise Linux Server release 7.8 (Maipo) 기준으로 작성되었습니다. 설치 및 실행은 root 계정에서 수행하였습니다.

다운로드
=============
설치경로 : [https://grafana.com/grafana/download](https://grafana.com/grafana/download) 또는 wget 활용하여 하단 명령어 실행(버전정보 입력 필요)

```bash
wget https://dl.grafana.com/oss/release/grafana-8.0.6-1.x86_64.rpm
```

프로그램 설치 및 최초 실행
=============
설치
------------

```bash
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
```

실행
-----------

```bash
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
```

|제목|화면|비고|
|---|----|----|
|최초화면|![image](https://user-images.githubusercontent.com/23024189/163523638-6ac603c4-6c75-40e0-b073-bd7da6895390.png)|http://<SERVER-IP>:3000/login 접속 및 최초정보 입력<br>최초 계정 : admin<br>초기 패스워드 : admin|
|초기 패스워드 설정|![image](https://user-images.githubusercontent.com/23024189/163523611-169b7259-5ae5-4a54-a85f-0e2e2c4c0595.png)|초기 계정의 패스워드를 변경|


프로그램 종료
------------

```bash
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
```


삭제(yum remove)
------------

grafana server 종료 후 수행해야 합니다.

```bash
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
```
