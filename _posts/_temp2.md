CI/CD 도구 안내
하위 페이지
•	GitLab
o	[Gitlab] 운영자 가이드
	[Gitlab] 설치/실행 안내
	[Gitlab] SMTP 설정
	[Gitlab] 계정관리
	[Gitlab] 최초 사용자 등록(root 비밀번호 초기화)
o	[Gitlab] 사용자 가이드
	[Gitlab] 계정 만들기
	[Gitlab] Gitlab 에 ssh key 적용
	[Gitlab] 그룹
	[Gitlab] 프로젝트
o	[Gitlab] 기타
	[Gitlab] Eclipse 에서 git 다루기
	[Gitlab] 기본적인 git 안내
	[Gitlab] .gitignore
	[Gitlab] git 설치파일
	[Gitlab] git 커밋 컨벤션
	[Gitlab] git command
	[Gitlab] 워크플로우 정의
	[Gitlab] git branch 전략
	[Gitlab] 사용 예시
•	Jenkins
o	[Jenkins] 운영자 가이드
	[Jenkins] 설치/실행 안내
	[Jenkins] Offline 플러그인 설치
	[Jenkins] Plugin 목록
	[Jenkins] Jenkins Offiline Plugin 설치
	[Jenkins] 사용자 생성
•	Nexus
o	[Nexus] Nexus Repository 3
	[Nexus] Nexus Repository 3 운영자 가이드
•	[Nexus] Maven Repository 생성방법
•	[Nexus] Nexus Repository 3 설치/실행 안내
•	[Nexus] Repository 라이브러리 수기 업로드 방법
•	[Nexus] 계정 권한 설정
•	[Nexus] 계정생성
	[Nexus] Nexus Repository 3 사용자 가이드
•	[Nexus] 메이븐에 Nexus Repository 미러링 설정 방법
o	[Nexus] 기타
	[Nexus] Nexus Repository 3 듀얼 구성 테스트
	[Nexus] 라이브러리 일괄 업로드 방법
•	[기타]
o	[Gitlab + Jenkins] Gitlab 과 Jenkins 연동
o	[Jenkins] Freestyle Project 설정을 통한 Gitlab 연동 (Pipeline X)
GitLab
GitLab 이란
 TBD 
GitLab vs. 다른 도구들
 TBD 
하위페이지
•	[Gitlab] 운영자 가이드
o	[Gitlab] 설치/실행 안내
o	[Gitlab] SMTP 설정
o	[Gitlab] 계정관리
o	[Gitlab] 최초 사용자 등록(root 비밀번호 초기화)
•	[Gitlab] 사용자 가이드
o	[Gitlab] 계정 만들기
o	[Gitlab] Gitlab 에 ssh key 적용
o	[Gitlab] 그룹
o	[Gitlab] 프로젝트
•	[Gitlab] 기타
o	[Gitlab] Eclipse 에서 git 다루기
o	[Gitlab] 기본적인 git 안내
o	[Gitlab] .gitignore
o	[Gitlab] git 설치파일
o	[Gitlab] git 커밋 컨벤션
o	[Gitlab] git command
o	[Gitlab] 워크플로우 정의
o	[Gitlab] git branch 전략
o	[Gitlab] 사용 예시
[Gitlab] 운영자 가이드
하위 페이지
•	[Gitlab] 설치/실행 안내
•	[Gitlab] SMTP 설정
•	[Gitlab] 계정관리
•	[Gitlab] 최초 사용자 등록(root 비밀번호 초기화)
[Gitlab] 설치/실행 안내
docker 를 이용한 Gitlab 설치
bastion host 다운로드 대상
docker image name	Docker Pull Command
gitlab enterprise edition	docker pull gitlab/gitlab-ee
gitlab community edition	docker pull gitlab/gitlab-ce
이미지 업로드
[root@almt01 docker]# docker images 
REPOSITORY       TAG    IMAGE ID     CREATED      SIZE 
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
[root@almt01 images]# docker images 
REPOSITORY       TAG    IMAGE ID     CREATED      SIZE 
gitlab/gitlab-ee latest 4062f34e61f6 42 hours ago 2.5GB 
[root@almt01 images]#
Code Block 1 gitlab docker load

docker 를 이용한 Gitlab 실행
방법1) docker run 활용
[root@almt01 docker]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS        PORTS                                             NAMES
2de33a1a5996   1c520775844c   "/sbin/tini -- /usr/…"   17 hours ago   Up 17 hours   0.0.0.0:8080->8080/tcp, 0.0.0.0:4000->50000/tcp   jenkins
[root@almt01 docker]# docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
jenkins/jenkins          latest         1c520775844c   4 days ago    442MB
gitlab/gitlab-ee         latest         4062f34e61f6   7 weeks ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   17d5117a2e37   2 years ago   1.76GB
[root@almt01 docker]# docker run --detach \
> --hostname docker.nicepay.co.kr \
> --publish 443:443 --publish 80:80 \
> --name gitlab \
> --volume /home/docker/gitlab/data:/var/opt/gitlab \
> --volume /home/docker/gitlab/logs:/var/log/gitlab \
> --volume /home/docker/gitlab/config:/etc/gitlab \
> 4062f34e61f6
033eb0f01bd3725540d10fa2ec4e82be4407480fc3efb0c7985a2d48606e79f1
[root@almt01 docker]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                             PORTS                                              NAMES
033eb0f01bd3   4062f34e61f6   "/assets/wrapper"        13 seconds ago   Up 12 seconds (health: starting)   0.0.0.0:80->80/tcp, 22/tcp, 0.0.0.0:443->443/tcp   gitlab
2de33a1a5996   1c520775844c   "/sbin/tini -- /usr/…"   17 hours ago     Up 17 hours                        0.0.0.0:8080->8080/tcp, 0.0.0.0:4000->50000/tcp    jenkins
[root@almt01 docker]# 
Code Block 2 gitlab docker run

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
      - '/home/docker/gitlab/data:/var/opt/gitlab'
      - '/home/docker/gitlab/logs:/var/log/gitlab'
      - '/home/docker/gitlab/config:/etc/gitlab'
Code Block 3 gitlab-ee docker-compose.yml

docker compose 실행
[docker@almt01 gitlab-ee]$ docker compose up -d 
[+] Running 1/1 ⠿ Container gitlab Started 0.4s 
[docker@almt01 gitlab-ee]$ docker ps
Code Block 4 gitlab docker compose up

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
Code Block 5 /etc/gitlab/gitlab.rb

gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "172.28.121.10"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "gitlab@nicepay.co.kr"
gitlab_rails['smtp_domain'] = "172.28.121.10"
gitlab_rails['smtp_tls'] = false
gitlab_rails['smtp_openssl_verify_mode'] = 'none'
gitlab_rails['smtp_enable_starttls_auto'] = false
gitlab_rails['smtp_ssl'] = false
gitlab_rails['smtp_force_ssl'] = false
 
gitlab_rails['gitlab_email_from'] = "gitlab@nicepay.co.kr"
gitlab_rails['gitlab_email_display_name'] = "Gitlab"
Code Block 6 nicepay gitlab.rb configure



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
Code Block 7 gitlab-ctl reconfigure

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
Code Block 8 gitlab root password setup

[Gitlab] 최초 사용자 등록(root 비밀번호 초기화)
gitlab-rails console 접속
docker 환경에서 사용자 정보 등록
[root@almt01 docker]# docker exec -it gitlab /bin/bash
root@docker:/# gitlab-rails console -e production
--------------------------------------------------------------------------------
 Ruby:         ruby 2.7.4p191 (2021-07-07 revision a21a3b7d23) [x86_64-linux]
 GitLab:       14.5.1-ee (cd2049cb286) EE
 GitLab Shell: 13.22.1
 PostgreSQL:   12.7
--------------------------------------------------------------------------------
Loading production environment (Rails 6.1.4.1)
irb(main):001:0> 
Code Block 9 docker exec gitlab

사용자 정보 등록 및 저장
gitlab-rails 사용자 정보 등록(id: 1 은 root 의미)
irb(main):001:0> user=User.where(id: 1).first
=> #<User id:1 @root>
irb(main):002:0> user.password='skdltm100%'
=> "skdltm100%"
irb(main):003:0> user.password_confirmation='skdltm100%'
=> "skdltm100%"
irb(main):004:0> user.save
Enqueued ActionMailer::MailDeliveryJob (Job ID: e584ffd5-4f83-45a0-a549-76216f8b9380) to Sidekiq(mailers) with arguments: 
"DeviseMailer", "password_change", "deliver_now", {:args=>[#<GlobalID:0x00007f57b3011f00 @uri=#<URI::GID gid://gitlab/User/1>>]}
=> true
irb(main):005:0> 
Code Block 10 gitlab-rails console

[Gitlab] 사용자 가이드
하위 페이지
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
하위 페이지
•	[Gitlab] Eclipse 에서 git 다루기
•	[Gitlab] 기본적인 git 안내
•	[Gitlab] .gitignore
•	[Gitlab] git 설치파일
•	[Gitlab] git 커밋 컨벤션
•	[Gitlab] git command
•	[Gitlab] 워크플로우 정의
•	[Gitlab] git branch 전략
•	[Gitlab] 사용 예시
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
Code Block 11 .gitignore

[Gitlab] git 설치파일
파일 : Git-2.34.1-64-bit.zip
[Gitlab] git 커밋 컨벤션
1. git 커밋 컨벤션
git 사용시 즉 커밋시 규칙을 정의 
2. git 커밋 메세지 구조 
커밋 메세지는 타입(typo), 제목(subject), 본문(body), 바닥글(footer)로 구분, 해당 영역은 아래 형식의 레이아웃으로 구성(서로 빈줄로 구분) 
type: subject
 
body 
 
footer

3. 타입(type)
타입은 타이틀 내에 포함되고, 커밋 타입은 아래 타입중 하나로 구성
•	feat : 새로운 기능 추가 , 화면 추가
•	fix : 버그 수정
•	docs : 문서 수정
•	style : 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우
•	refactor : 코드 리팩토링
•	test : 테스트 코드, 리팩토링 테스트 코드 추가
•	chore : 빌드 업무 수정, 패키지 매니저 수정
4. 제목(subject)
타입과 함께 타이틀 내에 포함되고, 아래 규칙으로 작성 
•	제목은 50자를 넘기지 않고, 마침표 X
•	제목에는 commit 타입을 함께 작성합니다.
•	과거 시제를 사용하지 않고 명령조로 작성합니다.
•	제목과 본문은 한 줄 띄워 분리
feat: 관리자페이지 거래 조회 기능 추가

5. 본문(Body)
커밋시 본문 내용은 선택사항이라 모든 커밋에 본문 내용을 작성할 필요는 없음, 추가적으로 정보를 전달할 경우 기입
•	어떻게 했는지가 아니라, 무엇을 왜 했는지 작성
•	최대 75자를 넘기지 않음
6. 바닥글(footer)
바닥글도 본문과 마찬가지로 선택사항 
•	이슈를 추적하기 위해 이슈 ID를 넣어주는 용도로 기입
7. 예시 포맷
feat: 관리자페이지 거래 조회 기능 추가
 
 
2022.01.19 xxx매니저님의 기능 추가 요청으로 인한, 거래 조회 기능 추가
- xxx.java 로직 변경
 
 
Resolves: NASR2201-03720

8. 이모지(Emoji)
만약에 사용한다면 참고
•	🎨 : 코드의 형식 / 구조를 개선 할 때
•	📰 : 새 파일을 만들 때
•	📝 : 사소한 코드 또는 언어를 변경 할 때
•	🐎 : 성능을 향상 시킬 때
•	📚 : 문서를 쓸 때
•	🐛 : 버그 reporting 할 때, @FIXME 주석 태그 삽입
•	🚑 : 버그를 고칠 때
•	🔥 : 코드 또는 파일을 제거 할 때, @CHANGED 주석 태그와 함께
•	🚜 : 파일 구조를 변경 할 때, 🎨과 함께 사용
•	🔨 : 코드를 리팩토링 할 때
•	☔️ : 테스트를 추가 할 때
•	🔬 : 코드 범위를 추가 할 때
•	💄 : UI / style 개선 시
•	♿️ : 접근성을 향상 시킬 때
•	🎉 : initial Commit
•	✨ : 새로운 기능을 소개 할 때
•	🤝 : 파일을 병합 할 때



Git 명령어(Git Command)
•	git checkout -b 브랜치 명 (생성)
•	git checkout -D 브랜치 명 (삭제)
•	git remote update (깃허브 브랜치 최신화)
•	git checkout -t origin/브랜치명 (깃허브에 다른사람이 만든 브랜치 가져오기)
•	git add . → 변경이 일어난 모든 파일 추적
•	git commit -m "커밋 메시지" -m "description 적는 곳" → 커밋을 추가하는 명령어
•	git push origin (브랜치명) → github저장소에 push
•	git branch -a → 모든 브랜치 목록 보기
•	git branch -D (브랜치명) → 로컬 브랜치 삭제
•	git push origin —delete (브랜치명) → 원격 브랜치 삭제 (—delete는 -D로 치환할 수 있다.)
•	git checkout -b 브랜치 명 (생성)
•	git checkout -D 브랜치 명 (삭제)
•	git remote update (깃허브 브랜치 최신화)
•	git checkout -t origin/브랜치명 (깃허브에 다른사람이 만든 브랜치 가져오기)
•	git add . → 변경이 일어난 모든 파일 추적
•	git commit -m "커밋 메시지" -m "description 적는 곳" → 커밋을 추가하는 명령어
•	git push origin (브랜치명) → github저장소에 push
•	git branch -a → 모든 브랜치 목록 보기
•	git branch -D (브랜치명) → 로컬 브랜치 삭제
•	git push origin —delete (브랜치명) → 원격 브랜치 삭제 (—delete는 -D로 치환할 수 있다.)
[Gitlab] 워크플로우 정의
1.팀을 구성하고 업무 배정
 
•	팀을 구성(Group, Member, Permission)하고 업무를 계획(Milestone)하고 업무를 세분화하여 팀원에게 배정(Issue)
 2.프로젝트 업무흐름
 
•	Group 등록
•	Member 등록 및 Permission 설정
•	Project 등록
•	Milestone 등록
•	Issue 등록 및 Assign
•	업무진행 및 Issue 종료
Group 등록
 
 
 
•	프로젝트를 수행하는 팀 단위로 Group을 만들며 유지보수 수행하는 팀이라면 운영시스템 단위로 Group을 생성
•	생성된 Group 확인 
Member 등록 및 Permission 설정
 
 
•	Permission은 Project Action과 Group Action에 대한 권한을 말함
권한 종류	설명
Owner	Group 등록한 팀원으로 모든 권한을 가짐
Maintainer	Group 수정/삭제와 Project 이동/삭제를 제외하고 Owner랑 같은 권한을 가짐 / 업무를 할당하고 소스코드에 대한 Merge Reqeust를 승인하는 팀원
Developer	프로젝트를 수행하는 팀원, 새로운 브랜치를 만들고 push가 가능하지만 protected 브랜치에는 push가 불가능함, master 브랜치가 protected 브랜치로 생성되는데 Developer는 master 브랜치로 push가 불가함
Reporter	Project 조회가 가능하고 Issue와 Label에 대한 관리가 가능 / QA이나 빌드배포 팀원이 해당
Guest	Issue등록과 comment를 남기는 것, Group & Project 조회가 가능
Project 생성
 
 
•	코드관리 단위로 Project를 생성
•	IDE에서 git을 통해 Project를 checkout해서 개발을 진행
[Gitlab] git branch 전략

•	git branch 전략
o	branch 란
o	merge 란?
o	master & main branch 란?
•	git-flow 전략
o	설명
o	장점
o	단점
o	branch 의 종류
o	branch 전략
•	github-flow 전략
o	설명
o	장점
o	단점
o	branch 의 종류
o	branch 전략
•	gitlab-flow 전략(Environment branchs with Gitlab flow)
o	설명
o	장점
o	단점
o	branch 의 종류
o	branch 전략
git branch 전략
branch 란
독립적으로 어떤 작업을 진행하기 위한 개념으로, 필요에 의해 만들어지는 각각의 branch 는 다른 branch 의 영향을 받지 않음
하나의 작업을 위해서 하나의 branch 를 생성하고 해당 branch 에서 작업을 하는 것이 일반적
merge 란?
branch 와 branch 와의 병합을 의미하는 것으로, 각각 branch 에서 작업한 내용을 하나의 branch 로 모으기 위한 것
master & main branch 란?
저장소를 처음 만들면 첫번째로 만들어지는 branch
일반적으로 master 로 부르나 BLM(Black Lives Matter) 운동에 의해 main 으로 바꿔 부르기로 함
git-flow 전략
설명
네덜란드 출신의 Vincent Driessen 이라는 파이썬 개발자가 공유한 Branch 전략(A successful Git branching model) 에서 안내한 방식으로, 많은 사이트에서 이용 중
장점
각 branch 간 명확한 역할 분배가 되어 있음
제품의 수명주기, 개발, 긴급패치 및 버전 관리에 용이
많은 버전관리 도구에서 기본적으로 제공함
단점
branch 가 많아 복잡하고 익히기 어려움
1개월 이상의 긴 호흡을 가지는 production 에 적합, 빠른 개발에는 부적합 함
branch 의 종류
master(main) : 라이브서버에 제품으로 출시되는 branch
develop : 다음 출시 버전을 대비하여 개발하는 branch
feature : 기능 개발 branch. develop branch 에 들어감
release : 다음 버전 출시를 준비하는 branch. develop branch 를 release branch 로 옮긴 후, QA, 테스트를 진행하고 master(main) branch 로 merge 한다.
hotfix : master(main) branch 에서 발생한 버그를 수정하는 branch
branch 전략
 
배포 가능한 상태만을 관리하는 master(main) branch 를 중심으로, 개발을 위한 develop branch 를 생성
github-flow 전략
설명
기본적인 git-flow 의 복잡성으로 인해 github 에 적용하기 어렵다는 Scott Chacon(GitHub Flow) 의 판단에 따라 만들어진 새로운 git 관리 방식
장점
release branch 가 명확하게 구분되어 있지 않은 시스템에서 사용이 유용함
수시로 release 되어야 할 필요가 있을 경우 github-flow 가 간단하고 효율이 좋음
단점
너무 단순하여 배포, 환경 구성, 릴리즈, 통합에 대한 이슈가 있음
branch 의 종류
master(main) : 항상 최신 상태로 유지되며, 새로운 branch 는 항상 master(main) 에서 생성. 해당 branch 는 항상 안정적(stable) 상태로 관리되어야 하며 product branch 임
feature : feature, develop branch 등은 master 의 branch 에서 분할하며, 브랜치 이름을 자세하게 적어 어떤 업무를 하는지 정의 함
branch 전략
 
항상 최신상태의 master branch 에서 개발을 위한 branch 를 생성
개발이 끝날때마다 바로 master branch 로 통합을 위해 pull request 를 생성
리뷰 후 master branch 에 merge. production 에 배포
gitlab-flow 전략(Environment branchs with Gitlab flow)
설명
 Git-flow 의 단순화 버전으로 Gitlab 에서 사용하기 위한 몇가지 전략(What is GitLab Flow?) 을 제시
대표적으로 Environment branchs with Gitlab flow 를 사용
장점
github-flow 의 단점을 개선하여 적용
단점
git-flow, github-flow 와 방향성이 다르게 진행되어 이질적이며, git-flow 의 모든 기능을 담지 못함
branch 의 종류
master(main) : 메인이 되는 branch 
pre-production : master(main) branch 에서 커밋한 내용을 일방적으로 deploy 하는 branch. 일반적으로 staging 영역에 해당함
production : pre-production 에서 QA, 테스트가 완료된 내용을 deploy 받아 prdoction 에 적용하는 branch
branch 전략
 
[Gitlab] 사용 예시
git flow에 맞춰서 사용 구성 및 예시  (git flow에서 몇개의 과정은 제외함)
•	과정 : 브랜치 구성 확인 → 이클립스 feature 브랜치 생성 → 커밋 / PUSH 이후  Merge Request 요청 (생성한 feature브랜치에서 develop 브랜치로 요청) → 리뷰 → Maintainer 권한이상 담당자 Merge 진행 
•	gitflow 참고 : [Gitlab] git branch 전략
•	git컨벤션 참고 : [Gitlab] git 커밋 컨벤션
•	gitlab 프로젝트 구성 / 사용자권한 참고 : [Gitlab] 워크플로우 정의
•	이클립스 git 사용법 참고 : [Gitlab] Eclipse 에서 git 다루기
브랜치 구성 확인 (프로젝트 구성 및 브랜치 추가)
 
 
•	원격 브랜치 구성은 develop → staging → main 
•	Default 브랜치는 main 브랜치로 설정되어 있으며 변경도 가능함 
브랜치 구성 확인 (Protected 브랜치 설정)
 
•	원격 브랜치인 develop / stating / main을 protected branch로 설정함 
•	protected branch로 설정이 되면 권한별로 브랜치 Merge 혹은 해당 브랜치로 Push를 설정할 수 있음
•	develop은 Maintainers 권한을 가진 계정만 merge 가능하게 하였고, 다이렉트로 Push는 Developers와 Maintainers 계정으로 설정함 (Push를 다이렉트로 한이유는 편의성?)
•	staging과 main 브랜치 같은경우 Maintainers 권한 계정만 핸들링 가능하도록 설정
이클립스 feature 브랜치 생성
 
 
•	프로젝트 우측 클릭 → Team → Switch To → New Branch 
•	Branch name을 feature/기능명칭 형식으로 구성하고 Finish (Check out new branch가 체크되어 있으면 생성브랜치로 Check out됨)
이클립스 커밋 / PUSH  
 
 
 
•	개발 이후 commit을 진행 
•	Commit Message는 git convention에 맞춰서 진행함 (위에 명시한 Git convention 페이지 참고)
GitLab Merge Request 요청
 
 
 
 
•	Merge Request → New Merge Request 통하여 Merge Request 진행
•	Change branches → Target Branch를 develop 브랜치로 변경 → Compare braches and continue → Create merge request 진행
리뷰 및 Merge 진행
 
 
 
 
 
•	Open인 상태인 Merge Request에서 개발된 내용 확인
•	코멘트를 통하여 리뷰 진행
•	확인 이후 Maintainers 권한의 담당자가 Merge 진행 (Merge가 진행되면 해당 원격 브랜치에 생성된 feature 브랜치가 삭제되고 develop 브랜치로 merge됨)
•	개발한 이클립스에서 생성한 feature 브랜치는 로컬브랜치라 삭제가 안되서 develop으로 checkout 이후 진행 →  develop 브랜치에서 merge 진행후 feature 브랜치 삭제   
Jenkins
하위페이지
•	[Jenkins] 운영자 가이드
o	[Jenkins] 설치/실행 안내
o	[Jenkins] Offline 플러그인 설치
o	[Jenkins] Plugin 목록
o	[Jenkins] Jenkins Offiline Plugin 설치
o	[Jenkins] 사용자 생성
[Jenkins] 운영자 가이드
하위 페이지
•	[Jenkins] 설치/실행 안내
•	[Jenkins] Offline 플러그인 설치
•	[Jenkins] Plugin 목록
•	[Jenkins] Jenkins Offiline Plugin 설치
•	[Jenkins] 사용자 생성
[Jenkins] 설치/실행 안내
docker 를 이용한 Jenkins 설치
bastion host 다운로드 대상
docker image name	Docker Pull Command	version
jenkins LTS version	docker pull jenkins/jenkins	2.331(2022. 1. 26  기준)
이미지 추출(bastion host)
[root@openwebt01 jenkins]# docker pull jenkins/jenkins
Using default tag: latest
latest: Pulling from jenkins/jenkins
0e29546d541c: Downloading [=======>                                           ]  8.096MB/54.92MB
a881d3e39b57: Downloading [=====>                                             ]  5.376MB/52.75MB
d424caad5b90: Download complete 
469ee726cc8f: Download complete 
f5eff683d188: Waiting 
955c78102a93: Waiting 
1e670fe34dae: Waiting 
30a5b207ad53: Waiting 
3c421004e233: Waiting 
e2729810a28a: Waiting 
4c14906574b5: Waiting 
8d6f1717fa64: Waiting 
a43947c0b965: Waiting 
0dfe4ad317f0: Waiting 
51f8f56f3e20: Waiting 
3944cb7b63c3: Waiting 
f3ebba26875d: Waiting 
Digest: sha256:0c31a58707a69449d2db06a31dc76b6bdf7f690d2664406104185eac27d0d54b
Status: Downloaded newer image for jenkins/jenkins:latest
docker.io/jenkins/jenkins:latest
 
[root@openwebt01 jenkins]# docker save -o jenkins.tar jenkins/jenkins:latest
[root@openwebt01 jenkins]# ls -al | grep *.tar
-rw-------. 1 root root  451500032  1월 25 09:13 jenkins.tar
[root@openwebt01 jenkins]# chown jenkins.tar pg:pg
[root@openwebt01 jenkins]# chown pg:mas_g jenkins.tar 
[root@openwebt01 jenkins]# ls -al | grep *.tar
-rw-------. 1 pg   mas_g 451500032  1월 25 09:13 jenkins.tar
[root@openwebt01 jenkins]# 
Code Block 12 jenkins docker save

이미지 업로드
[root@almt01 images]# docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
gitlab/gitlab-ee         latest         4062f34e61f6   7 weeks ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   17d5117a2e37   2 years ago   1.76GB
[root@almt01 images]# docker load < jenkins.tar 
11936051f93b: Loading layer [==================================================>]  129.1MB/129.1MB
8b1d425bc3cc: Loading layer [==================================================>]  129.7MB/129.7MB
ea041837b884: Loading layer [==================================================>]  65.02kB/65.02kB
26d94d80b16c: Loading layer [==================================================>]  10.37MB/10.37MB
1b9c4d263b95: Loading layer [==================================================>]  338.9kB/338.9kB
b81f1f079f3a: Loading layer [==================================================>]  3.584kB/3.584kB
99088ba6bff9: Loading layer [==================================================>]  9.728kB/9.728kB
5fda55cbd6e9: Loading layer [==================================================>]    874kB/874kB
5dbee000bfea: Loading layer [==================================================>]  73.77MB/73.77MB
9ba6cc0a10ed: Loading layer [==================================================>]  12.29kB/12.29kB
a8cae674152a: Loading layer [==================================================>]  6.263MB/6.263MB
43c65400a8f6: Loading layer [==================================================>]  100.9MB/100.9MB
60b7dbfc07f6: Loading layer [==================================================>]  9.728kB/9.728kB
c0eccc79daf0: Loading layer [==================================================>]  5.632kB/5.632kB
2f0f35708125: Loading layer [==================================================>]  3.072kB/3.072kB
d7063cee3652: Loading layer [==================================================>]   2.56kB/2.56kB
cb51e1456cd5: Loading layer [==================================================>]  13.82kB/13.82kB
Loaded image: jenkins/jenkins:latest
[root@almt01 images]# docker images
REPOSITORY               TAG            IMAGE ID       CREATED       SIZE
jenkins/jenkins          latest         1c520775844c   3 days ago    442MB
gitlab/gitlab-ee         latest         4062f34e61f6   7 weeks ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   17d5117a2e37   2 years ago   1.76GB
[root@almt01 images]# 
Code Block 13 jenkins docker load

docker 를 이용한 Jenkins 실행
방법1) docker run 활용
jenkins docker run
[root@almt01 images]# docker images --digests
REPOSITORY               TAG            DIGEST    IMAGE ID       CREATED       SIZE
jenkins/jenkins          latest         <none>    1c520775844c   3 days ago    442MB
gitlab/gitlab-ee         latest         <none>    4062f34e61f6   7 weeks ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   <none>    17d5117a2e37   2 years ago   1.76GB
[root@almt01 images]# docker run --detach \
> --publish 4000:50000 \
> --publish 8080:8080 \
> --name jenkins \
> --volume jenkins-data:/var/jenkins_home  \
> --volume jenkins-docker-certs:/certs/client:ro \
> 1c520775844c
f3f18b1ec34ed8aba28130b733bd95ce5d7e68f347edd69a9cf282797b79355d
[root@almt01 images]# docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS                 PORTS                                              NAMES
f3f18b1ec34e   1c520775844c   "/sbin/tini -- /usr/…"   4 seconds ago   Up 3 seconds           0.0.0.0:8080->8080/tcp, 0.0.0.0:4000->50000/tcp    jenkins
5db4ce88dab3   4062f34e61f6   "/assets/wrapper"        7 weeks ago     Up 7 weeks (healthy)   0.0.0.0:80->80/tcp, 22/tcp, 0.0.0.0:443->443/tcp   gitlab
Code Block 14 jenkins docker run

2) docker compose 활용
프로젝트 디렉토리 생성 후 docker-compose.yml 파일 생성방법
jenkins docker-compose.yml
version: '3.0'
services:
  jenkins:
    image: '1c520775844c'
    #restart: always
    hostname: 'jenkins.nicepay.co.kr'
    container_name : 'jenkins'
    environment:
      TZ : "Asia/Seoul"
    ports:
      - '4000:50000'
      - '8080:8080'
    volumes:
      - '/home/docker/jenkins/data:/var/jenkins_home'
      - '/home/docker/jenkins/certs:/certs/client:ro'
Code Block 15 jenkins docker-compose.yml

docker volumes 대상 디렉토리 owner 변경
chown (-R) 1000
[root@almt01 docker]# chown -R 1000 jenkins/
[root@almt01 docker]# ls -al | grep jenkins
drwxr-xr-x  4   1000 docker       31  1월 25 16:13 jenkins
[root@almt01 docker]# 
Code Block 16 jenkins volumes chwon

docker compose 실행
jenkins docker compose up
[root@almt01 jenkins]# docker compose up -d
[+] Running 2/2
 ⠿ Network jenkins_default  Created                                                                                                                                                                                                                                                                                   0.1s
 ⠿ Container jenkins        Started                                                                                                                                                                                                                                                                                   0.4s
[root@almt01 jenkins]# 
Code Block 17 jenkins docker compose up

Jenkins 실행 및 최초 설치
jenkins 사이트 접속(지정포트 : 8080, docker 설정한 port 로 접속)
http://172.32.161.36:8080
 
Unlock Jenkins 페이지에서 최초 admin Password 확인 후 등록
docker logs 에서 확인
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by org.codehaus.groovy.reflection.CachedClass (file:/var/jenkins_home/war/WEB-INF/lib/groovy-all-2.4.21.jar) to method java.lang.Object.finalize()
WARNING: Please consider reporting this to the maintainers of org.codehaus.groovy.reflection.CachedClass
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
2022-01-25 08:43:31.880+0000 [id=30]    INFO    jenkins.install.SetupWizard#init: 
 
*************************************************************
*************************************************************
*************************************************************
 
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:
 
67f3df57e4a04c9fb415427e2f802611
 
This may also be found at: /var/jenkins_home/secrets/initialAdminPassword
 
*************************************************************
*************************************************************
*************************************************************
Code Block 18 docker logs -f --tail 300 jenkins

data 영역 해당 파일에서 확인
[root@almt01 secrets]# pwd
/home/docker/jenkins/data/secrets
[root@almt01 secrets]# cat initialAdminPassword 
67f3df57e4a04c9fb415427e2f802611
[root@almt01 secrets]#
Code Block 19 jenkins initialAdminPassword

인터넷 연결이 되지 않은 상태이므로 offline 모드로 설치, Skip Plugin Installations 클릭
 
Admin User 정보 등록

 
Jenkins 접속 URL 설정(최초 설정한 8080 으로 그대로 수행)
 
설치완료
 
온라인의 경우 추천 플러그인 설치 가능
 
[Jenkins] Offline 플러그인 설치
Jenkins 필요 플러그인 검색
https://jenkins.io/ 의 plugins 메뉴 클릭하거나
 
https://plugins.jenkins.io/ 에서 plugin 파일을 검색
 
원하는 플러그인 이름 입력 후 검색
 
검색된 플러그인을 Releases 에서 버전 숫자 클릭하여 다운로드 후 hpi 파일을 설치
 
만일 의존성 패키지가 있다면 Dependencies 내 Required 를 모두 설치, Optional 과 Implied 는 선택사항
 
만일 패키지 명을 알고 있다면 아래 주소로 들어가서 직접 다운로드 가능
https://updates.jenkins-ci.org/download/plugins
 
Jenkins 플러그인 설치
Jenkins 관리 - 플러그인 관리 에서 고급으로 이동
 
Deploy Plugin 메뉴에서 파일 선택 클릭, Deploy 버튼 클릭
 
[Jenkins] Plugin 목록
Jenkins Plugin 설치 정보
Ant
Plugin 이름	파일명	version	Dependencies
Ant	ant.hpi	1.13	
	Structs Plugin	structs.hpi	308.v852b473a2b8c	Required
	SSH server	sshd.hpi	3.1.0	Implied
	JavaBeans Activation Framework (JAF) API	javax-activation-api.hpi	1.20-2	Implied
	JavaMail API	javax-mail-api.hpi	1.6.2-5	Implied
Maven
Plugin 이름	파일명	version	Dependencies
Maven Ingegration	maven-plugin.hpi	3.16	
	Apache HttpComponents Client 4.x API Plugin	apache-httpcomponents-client-4-api.hpi	4.5.13-1.0	Required
	Javadoc	javadoc.hpi	1.6	Required
	JSch dependency plugin	jsch.hpi	0.1.55.2	Required
		SSH Credentials Plugin	ssh-credentials.hpi	1.19	Required
		•	Credentials Plugin	credentials.hpi	2.6.2	Required
		•	Trilead API Plugin	trilead-api.hpi	1.0.13	Required
	JUnit Plugin	junit.hpi	1.53	Required
	
	Checks API plugin	checks-api.hpi	1.7.2	Required
		•	Display URL API	display-url-api.hpi	2.3.5	Required
		•	Plugin Utilities API Plugin	plugin-util-api.hpi	2.13.0	Required
		•	Pipeline: Supporting APIs	workflow-support.hpi	813.vb_d7c3d2984a_0	Required
		•	SCM API Plugin	scm-api.hpi	2.6.5	Required
		•	Pipeline: Step API	workflow-step-api.hpi	622.vb_8e7c15b_c95a_	Required
	
	Script Security Plugin	script-security.hpi	1131.v8b_b_5eda_c328e	Required
		•	Caffeine API	caffeine-api.hpi	2.9.2-29.v717aac953ff3	Required
	
	Bootstrap 4 API Plugin	bootstrap4-api.hpi	4.6.0.3	Required
		•	Font Awesome API Plugin	font-awesome-api.hpi	5.15.4-5	Required
		•	JQuery3 API Plugin	jquery3-api.hpi	3.6.0-2	Required
		•	Popper.js API Plugin	1.16.1-2	popper-api.hpi	Required
	
	ECharts API Plugin	echarts-api.hpi	5.2.2-2	Required
		•	Bootstrap 5 API Plugin	bootstrap5-api.hpi	5.1.3-4	Required
		•	Popper.js 2 API Plugin	popper2-api.hpi	2.11.2-1	Required
	
	•	Jackson 2 API Plugin	jackson2-api.hpi	2.13.1-246.va8a9f3eaf46a	Required
	
	•	Snakeyaml API Plugin	1.29.1	snakeyaml-api.hpi	Required
	
	Pipeline: API	workflow-api.hpi	1136.v7f5f1759dc16	Required
	
	Pipeline: Step API	workflow-step-api.hpi	622.vb_8e7c15b_c95a_	Required
	Mailer Plugin	mailer.hpi	408.vd726a_1130320	Required
	Token Macro Plugin	token-macro.hpi	267.vcdaea6462991	Optional
	JavaBeans Activation Framework (JAF) API	javax-activation-api.hpi	1.20-2	Implied
	JavaMail API	javax-mail-api.hpi	1.6.2-5	Implied
Git
Plugin 이름	파일명	version	Dependencies
Git plugin	git.hpi	4.10.3	
	Pipeline: SCM Step	workflow-scm-step.hpi	2.13	Required
	Pipeline: Step API	workflow-step-api.hpi	622.vb_8e7c15b_c95a_	Required
	Credentials Binding Plugin	credentials-binding.hpi	1.27.1	Required
		Plain Credentials	plain-credentials.hpi	1.8	Optional
	Credentials Plugin	credentials.hpi	2.6.2	Required
	Git client plugin	git-client.hpi	3.11.0	Required
	Mailer Plugin	mailer.hpi	408.vd726a_1130320	Required
	SCM API Plugin	scm-api.hpi	2.6.5	Required
	Script Security Plugin	script-security.hpi	1131.v8b_b_5eda_c328e	Required
	SSH Credentials Plugin	ssh-credentials.hpi	1.19	Required
	Structs Plugin	structs.hpi	308.v852b473a2b8c	Required
	Configuration as Code ≥ 1.55			Optional
	Matrix Project Plugin	matrix-project.hpi	1.2	Optional
	Parameterized Trigger ≥ 2.39			Optional
	promoted builds ≥ 3.9.1			Optional
	Token Macro Plugin	token-macro.hpi	267.vcdaea6462991	Optional
	JavaBeans Activation Framework (JAF) API	javax-activation-api.hpi	1.20-2	Implied
	JavaMail API	javax-mail-api.hpi	1.6.2-5	Implied
Gitlab
Plugin 이름	파일명	version	Dependencies
GitLab Plugin	gitlab-plugin.hpi	1.5.27	
	Caffeine API	caffeine-api.hpi	2.9.2-29.v717aac953ff3	Required
	Jersey 2 API	jersey2-api.hpi	2.35-3	Required
	Pipeline: API	workflow-api.hpi	1136.v7f5f1759dc16	Required
	Pipeline: Shared Groovy Libraries	workflow-cps-global-lib.hpi	552.vd9cc05b8a2e1	Required
		GIT server Plugin	git-server.hpi	1.1	Required
		Folders Plugin	cloudbees-folder.hpi	6.17	Required
		Pipeline: Groovy	workflow-cps.hpi	2.94	Required
		JavaScript GUI Lib: ACE Editor bundle	ace-editor.hpi	1.1	Required
	Pipeline: Nodes and Processes	workflow-durable-task-step.hpi	1121.va_65b_d2701486	Required
		Durable Task Plugin	durable-task.hpi	493.v195aefbb0ff2	Required
	Pipeline: Job	workflow-job.hpi	1167.v8fe861b_09ef9	Required
	Pipeline: SCM Step	workflow-scm-step.hpi	2.13	Required
	Pipeline: Step API	workflow-step-api.hpi	622.vb_8e7c15b_c95a_	Required
	Pipeline: Supporting APIs	workflow-support.hpi	813.vb_d7c3d2984a_0	Required
	Apache HttpComponents Client 4.x API	apache-httpcomponents-client-4-api.hpi	4.5.13-1.0	Required
	Credentials Plugin	credentials.hpi	2.6.2	Required
	Display URL API	display-url-api.hpi	2.3.5	Required
	Git client plugin	git-client.hpi	3.11.0	Required
	Git plugin	git.hpi	4.10.3	Required
		Git 플러그인 의존성 정보 참고			
	Jackson 2 API Plugin	jackson2-api.hpi	2.13.1-246.va8a9f3eaf46a	Required
	JUnit Plugin	junit.hpi	1.53	Required
	Matrix Project Plugin	matrix-project.hpi	1.2	Required
	SCM API Plugin	scm-api.hpi	2.6.5	Required
	Script Security Plugin	script-security.hpi	1131.v8b_b_5eda_c328e	Required
	Structs Plugin	structs.hpi	308.v852b473a2b8c	Required
	Plain Credentials	plain-credentials.hpi	1.8	Optional
	SSH Credentials Plugin	ssh-credentials.hpi	1.19	Optional
	JavaBeans Activation Framework (JAF) API	javax-activation-api.hpi	1.20-2	Implied
	JavaMail API	javax-mail-api.hpi	1.6.2-5	Implied
Pipeline
Plugin 이름	파일명	version	Dependencies
Pipeline	workflow-aggregator.hpi	2.6	
	Lockable Resources	lockable-resources.hpi	2.13	Required
	Pipeline: Stage View	pipeline-stage-view.hpi	2.21	Required
		JavaScript GUI Lib: Moment.js bundle plugin	momentjs.hpi	1.1.1	Required
		JavaScript GUI Lib: Handlebars bundle plugin	handlebars.hpi	3.0.8	Required
		Pipeline: REST API Plugin	pipeline-rest-api.hpi	2.21	Required
	Pipeline: API	workflow-api.hpi	1136.v7f5f1759dc16	Required
	Pipeline: Basic Steps	workflow-basic-steps.hpi	2.24	Required
	Pipeline: Shared Groovy Libraries	workflow-cps-global-lib.hpi	552.vd9cc05b8a2e1	Required
	Pipeline: Groovy	workflow-cps.hpi	2.94	Required
	Pipeline: Nodes and Processes	workflow-durable-task-step.hpi	1121.va_65b_d2701486	Required
	Pipeline: Job	workflow-job.hpi	1167.v8fe861b_09ef9	Required
	Pipeline: Multibranch	workflow-multibranch.hpi	2.26	Required
	Pipeline: SCM Step	Step workflow-scm-step.hpi	2.13	Required
	Pipeline: Step API	workflow-step-api.hpi	622.vb_8e7c15b_c95a_	Required
	Pipeline: Supporting APIs	workflow-support.hpi	813.vb_d7c3d2984a_0	Required
	Folders Plugin	cloudbees-folder.hpi	6.17	Required
	Credentials Plugin	credentials.hpi	2.6.2	Required
	Git client plugin	git-client.hpi	3.11.0	Required
	Jackson 2 API Plugin	jackson2-api.hpi	2.13.1-246.va8a9f3eaf46a	Required
	Pipeline: Build Step	pipeline-build-step.hpi	2.15	Required
	Pipeline: Input Step	pipeline-input-step.hpi	446.vf27b_0b_83500e	Required
	Pipeline: Milestone Step	pipeline-milestone-step.hpi	1.3.2	Required
	Pipeline: Stage Step	pipeline-stage-step.hpi	291.vf0a8a7aeeb50	Required
	SCM API	scm-api.hpi	2.6.5	Required
	Structs Plugin	structs.hpi	308.v852b473a2b8c	Required
	Pipeline: Declarative	pipeline-model-definition.hpi	1.9.3	Required
	JAXB			Implied
	Trilead API Plugin	trilead-api.hpi	1.0.13	Implied
	SSH server	sshd.hpi	3.1.0	Implied
	JavaBeans Activation			Implied
	JavaBeans Activation Framework (JAF) API	javax-activation-api.hpi	1.20-2	Implied
	JavaMail API	javax-mail-api.hpi	1.6.2-5	Implied
Post Build Task

Plugin 이름	파일명	version	Dependencies
Post build task	postbuild-task.hpi	1.9	

Blue Ocean
Plugin 이름	파일명	version	Dependencies
Blue Ocean	blueocean.hpi	1.25.2	
	Bitbucket Pipeline for Blue Ocean	blueocean-bitbucket-pipeline.hpi	1.25.2	Required
	Common API for Blue Ocean	blueocean-commons.hpi	1.25.2	Required
	Config API for Blue Ocean	blueocean-config.hpi	1.25.2	Required
	Blue Ocean Core JS	blueocean-core-js.hpi	1.25.2	Required
	Dashboard for Blue Ocean	blueocean-dashboard.hpi	1.25.2	Required
	Events API for Blue Ocean	blueocean-events.hpi	1.25.2	Required
	Git Pipeline for Blue Ocean	blueocean-git-pipeline.hpi	1.25.2	Required
	GitHub Pipeline for Blue Ocean	blueocean-github-pipeline.hpi	1.25.2	Required
		GitHub plugin	github.hpi	1.34.1	Required
		GitHub API Plugin	github-api.hpi	1.301-378.v9807bd746da5	Required
		GitHub Branch Source Plugin	github-branch-source.hpi	2.114	Required
		Pub-Sub "light" Bus	pubsub-light.hpi	1.16	Required
	i18n for Blue Ocean	blueocean-i18n.hpi	1.25.2	Required
	JWT for Blue Ocean	blueocean-jwt.hpi	1.25.2	Required
	Personalization for Blue Ocean	blueocean-personalization.hpi	1.25.2	Required
	Pipeline implementation for Blue Ocean	blueocean-pipeline-api-impl.hpi	1.25.2	Required
	Blue Ocean Pipeline Editor	blueocean-pipeline-editor.hpi	1.25.2	Required
	REST Implementation for Blue Ocean	blueocean-rest-impl.hpi	1.25.2	Required
	REST API for Blue Ocean	blueocean-rest.hpi	1.25.2	Required
	Web for Blue Ocean	blueocean-web.hpi	1.25.2	Required
	Design Language	jenkins-design-language.hpi	1.25.2	Required
	Autofavorite for Blue Ocean	blueocean-autofavorite.hpi	1.2.4	Required
	Display URL for Blue Ocean	blueocean-display-url.hpi	2.4.1	Required
	Pipeline: Build Step	pipeline-build-step.hpi	2.15	Required
	Pipeline: Milestone Step	pipeline-milestone-step.hpi	1.3.2	Required
	Blue Ocean Executor Info	blueocean-executor-info.hpi	1.25.2	Optional(DEPRECATED )
	JIRA Integration for Blue Ocean	blueocean-jira.hpi	1.25.2	Optional
		Jira plugin	jira.hpi	3.6	Required
	SSH server	sshd.hpi	3.1.0	Implied
	JavaBeans Activation Framework (JAF) API	javax-activation-api.hpi	1.20-2	Implied
	JavaMail API	javax-mail-api.hpi	1.6.2-5	Implied
Jenkins PlugIn 이름 및 다운로드 URL

이름	download URL	download date	version	파일명
Ant	https://updates.jenkins-ci.org/download/plugins/ant/
2022. 1. 28	1.13	ant.hpi
Apache HttpComponents Client 4.x API Plugin	https://updates.jenkins-ci.org/download/plugins/apache-httpcomponents-client-4-api/
2022. 1. 27 	4.5.13-1.0	apache-httpcomponents-client-4-api.hpi
Authentication Tokens API	https://updates.jenkins-ci.org/download/plugins/authentication-tokens/
2022. 1. 28	1.4	authentication-tokens.hpi
Autofavorite for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-autofavorite/
2022. 1. 27 	1.2.4	blueocean-autofavorite.hpi
Bitbucket Branch Source Plugin	https://updates.jenkins-ci.org/download/plugins/cloudbees-bitbucket-branch-source/
2022. 1. 28	751.vda_24678a_f781	cloudbees-bitbucket-branch-source.hpi
Bitbucket Pipeline for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-bitbucket-pipeline/
2022. 1. 27	1.25.2	blueocean-bitbucket-pipeline.hpi
Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean/
2022. 1. 27	1.25.2	blueocean.hpi
Blue Ocean Core JS	https://updates.jenkins-ci.org/download/plugins/blueocean-core-js/
2022. 1. 27	1.25.2	blueocean-core-js.hpi
Blue Ocean Executor Info	https://updates.jenkins-ci.org/download/plugins/blueocean-executor-info/
2022. 1. 27	1.25.2	blueocean-executor-info.hpi
Blue Ocean Pipeline Editor	https://updates.jenkins-ci.org/download/plugins/blueocean-pipeline-editor/
2022. 1. 27	1.25.2	blueocean-pipeline-editor.hpi
Bootstrap 4 API Plugin	https://updates.jenkins-ci.org/download/plugins/bootstrap4-api/
2022. 1. 27	4.6.0.3	bootstrap4-api.hpi
Bootstrap 5 API Plugin	https://updates.jenkins-ci.org/download/plugins/bootstrap5-api/
2022. 1. 27	5.1.3-4	bootstrap5-api.hpi
Branch API Plugin	https://updates.jenkins-ci.org/download/plugins/branch-api/
2022. 1. 27	2.7.0	branch-api.hpi
Caffeine API	https://updates.jenkins-ci.org/download/plugins/caffeine-api/
2022. 1. 27 	2.9.2-29.v717aac953ff3	caffeine-api.hpi
Checks API plugin	https://updates.jenkins-ci.org/download/plugins/checks-api/
2022. 1. 27	1.7.2	checks-api.hpi
Common API for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-commons/
2022. 1. 27	1.25.2	blueocean-commons.hpi
Config API for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-config/
2022. 1. 27	1.25.2	blueocean-config.hpi
Credentials Binding Plugin	https://updates.jenkins-ci.org/download/plugins/credentials-binding/
2022. 1. 27	1.27.1	credentials-binding.hpi
Credentials Plugin	https://updates.jenkins-ci.org/download/plugins/credentials/
2022. 1. 27 	2.6.2	credentials.hpi
Dashboard for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-dashboard/
2022. 1. 27	1.25.2	blueocean-dashboard.hpi
Design Language	https://updates.jenkins-ci.org/download/plugins/jenkins-design-language/
2022. 1. 27	1.25.2	jenkins-design-language.hpi
Display URL API	https://updates.jenkins-ci.org/download/plugins/display-url-api/
2022. 1. 27 	2.3.5	display-url-api.hpi
Display URL for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-display-url/
2022. 1. 27	2.4.1	blueocean-display-url.hpi
Durable Task Plugin	https://updates.jenkins-ci.org/download/plugins/durable-task/
2022. 1. 27	493.v195aefbb0ff2	durable-task.hpi
ECharts API Plugin	https://updates.jenkins-ci.org/download/plugins/echarts-api/
2022. 1. 27	5.2.2-2	echarts-api.hpi
Events API for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-events/
2022. 1. 27	1.25.2	blueocean-events.hpi
Favorite	https://updates.jenkins-ci.org/download/plugins/favorite/
2022. 1. 27	2.3.3	favorite.hpi
Folders Plugin	https://updates.jenkins-ci.org/download/plugins/cloudbees-folder/
2022. 1. 27 	6.17	cloudbees-folder.hpi
Font Awesome API Plugin	https://updates.jenkins-ci.org/download/plugins/font-awesome-api/
2022. 1. 27	5.15.4-5	font-awesome-api.hpi
Git client plugin	https://updates.jenkins-ci.org/download/plugins/git-client/
2022. 1. 27	3.11.0	git-client.hpi
Git Pipeline for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-git-pipeline/
2022. 1. 27	1.25.2	blueocean-git-pipeline.hpi
Git plugin	https://updates.jenkins-ci.org/download/plugins/git/
2022. 1. 27 	4.10.3	git.hpi
GIT server Plugin	https://updates.jenkins-ci.org/download/plugins/git-server/
2022. 1. 27	1.1	git-server.hpi
GitHub API Plugin	https://updates.jenkins-ci.org/download/plugins/github-api/
2022. 1. 28	1.301-378.v9807bd746da5	github-api.hpi
GitHub Branch Source Plugin	https://updates.jenkins-ci.org/download/plugins/github-branch-source/
2022. 1. 28	2.114	github-branch-source.hpi
GitHub Pipeline for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-github-pipeline/
2022. 1. 27	1.25.2	blueocean-github-pipeline.hpi
GitHub plugin	https://updates.jenkins-ci.org/download/plugins/github/
2022. 1. 28	1.34.1	github.hpi
GitLab Plugin	https://updates.jenkins-ci.org/download/plugins/gitlab-plugin/
2022. 1. 27	1.5.27	gitlab-plugin.hpi
Handy Uri Templates 2.x API	https://updates.jenkins-ci.org/download/plugins/handy-uri-templates-2-api/
2022. 1. 28	2.1.8-1.0	handy-uri-templates-2-api.hpi
HTML Publisher	https://updates.jenkins-ci.org/download/plugins/htmlpublisher/
2022. 1. 28	1.28	htmlpublisher.hpi
i18n for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-i18n/
2022. 1. 27	1.25.2	blueocean-i18n.hpi
Jackson 2 API Plugin	https://updates.jenkins-ci.org/download/plugins/jackson2-api/
2022. 1. 27	2.13.1-246.va8a9f3eaf46a	jackson2-api.hpi
Java JSON Web Token (JJWT) Plugin	https://updates.jenkins-ci.org/download/plugins/jjwt-api/
2022. 1. 28	0.11.2-9.c8b45b8bb173	jjwt-api.hpi
JavaBeans Activation Framework (JAF) API	https://updates.jenkins-ci.org/download/plugins/javax-activation-api/
2022. 1. 27 	1.20-2	javax-activation-api.hpi
Javadoc	https://updates.jenkins-ci.org/download/plugins/javadoc/
2022. 1. 28	1.6	javadoc.hpi
JavaMail API	https://updates.jenkins-ci.org/download/plugins/javax-mail-api/
2022. 1. 27	1.6.2-5	javax-mail-api.hpi
JavaScript GUI Lib: ACE Editor bundle	https://updates.jenkins-ci.org/download/plugins/ace-editor/
2022. 1. 27	1.1	ace-editor.hpi
Jersey 2 API	https://updates.jenkins-ci.org/download/plugins/jersey2-api/
2022. 1. 27	2.35-3	jersey2-api.hpi
JIRA Integration for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-jira/
2022. 1. 27	1.25.2	blueocean-jira.hpi
Jira plugin	https://updates.jenkins-ci.org/download/plugins/jira/
2022. 1. 27	3.6	jira.hpi
JQuery3 API Plugin	https://updates.jenkins-ci.org/download/plugins/jquery3-api/
2022. 1. 27	3.6.0-2	jquery3-api.hpi
JSch dependency plugin	https://updates.jenkins-ci.org/download/plugins/jsch/
2022. 1. 27 	0.1.55.2	jsch.hpi
JUnit Plugin	https://updates.jenkins-ci.org/download/plugins/junit/
2022. 1. 27	1.53	junit.hpi
JWT for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-jwt/
2022. 1. 27	1.25.2	blueocean-jwt.hpi
Mailer Plugin	https://updates.jenkins-ci.org/download/plugins/mailer/
2022. 1. 27 	408.vd726a_1130320	mailer.hpi
Matrix Project Plugin	https://updates.jenkins-ci.org/download/plugins/matrix-project/
2022. 1. 27	1.2	matrix-project.hpi
Maven Ingegration	https://updates.jenkins-ci.org/download/plugins/maven-plugin/
2022. 1. 28	3.16	maven-plugin.hpi
OkHttp Plugin	https://updates.jenkins-ci.org/download/plugins/okhttp-api/
2022. 1. 28	4.9.3-105.vb96869f8ac3a	okhttp-api.hpi
Personalization for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-personalization/
2022. 1. 27	1.25.2	blueocean-personalization.hpi
Pipeline Graph Analysis Plugin	https://updates.jenkins-ci.org/download/plugins/pipeline-graph-analysis/
2022. 1. 28 	1.12	pipeline-graph-analysis.hpi
Pipeline implementation for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-pipeline-api-impl/
2022. 1. 27	1.25.2	blueocean-pipeline-api-impl.hpi
Pipeline SCM API for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-pipeline-scm-api/
2022. 1. 27	1.25.2	blueocean-pipeline-scm-api.hpi
Pipeline: API	https://updates.jenkins-ci.org/download/plugins/workflow-api/
2022. 1. 27	1136.v7f5f1759dc16	workflow-api.hpi
Pipeline: Basic Steps 	https://updates.jenkins-ci.org/download/plugins/workflow-basic-steps/
2022. 1. 28	2.24	workflow-basic-steps.hpi
Pipeline: Build Step	https://updates.jenkins-ci.org/download/plugins/pipeline-build-step/
2022. 1. 28	2.15	pipeline-build-step.hpi
Pipeline: Declarative	https://updates.jenkins-ci.org/download/plugins/pipeline-model-definition/
2022. 1. 28	1.9.3	pipeline-model-definition.hpi
Pipeline: Declarative Extension Points API	https://updates.jenkins-ci.org/download/plugins/pipeline-model-extensions/
2022. 1. 28	1.9.3	pipeline-model-extensions.hpi
Pipeline: Groovy	https://updates.jenkins-ci.org/download/plugins/workflow-cps/
2022. 1. 27 	2.94	workflow-cps.hpi
Pipeline: Input Step	https://updates.jenkins-ci.org/download/plugins/pipeline-input-step/
2022. 1. 28	446.vf27b_0b_83500e	pipeline-input-step.hpi
Pipeline: Job	https://updates.jenkins-ci.org/download/plugins/workflow-job/
2022. 1. 27	1167.v8fe861b_09ef9	workflow-job.hpi
Pipeline: Milestone Step	https://updates.jenkins-ci.org/download/plugins/pipeline-milestone-step/
2022. 1. 28	1.3.2	pipeline-milestone-step.hpi
Pipeline: Model API	https://updates.jenkins-ci.org/download/plugins/pipeline-model-api/
2022. 1. 28	1.9.3	pipeline-model-api.hpi
Pipeline: Multibranch	https://updates.jenkins-ci.org/download/plugins/workflow-multibranch/
2022. 1. 27	2.26	workflow-multibranch.hpi
Pipeline: Nodes and Processes	https://updates.jenkins-ci.org/download/plugins/workflow-durable-task-step/
2022. 1. 27	1121.va_65b_d2701486	workflow-durable-task-step.hpi
Pipeline: SCM Step	https://updates.jenkins-ci.org/download/plugins/workflow-scm-step/
2022. 1. 27	2.13	workflow-scm-step.hpi
Pipeline: Shared Groovy Libraries	https://updates.jenkins-ci.org/download/plugins/workflow-cps-global-lib/
2022. 1. 27	552.vd9cc05b8a2e1	workflow-cps-global-lib.hpi
Pipeline: Stage Step	https://updates.jenkins-ci.org/download/plugins/pipeline-stage-step/
2022. 1. 28	291.vf0a8a7aeeb50	pipeline-stage-step.hpi
Pipeline: Stage Tags Metadata	https://updates.jenkins-ci.org/download/plugins/pipeline-stage-tags-metadata/
2022. 1. 28 	1.9.3	pipeline-stage-tags-metadata.hpi
Pipeline: Step API	https://updates.jenkins-ci.org/download/plugins/workflow-step-api/
2022. 1. 27	622.vb_8e7c15b_c95a_	workflow-step-api.hpi
Pipeline: Supporting APIs	https://updates.jenkins-ci.org/download/plugins/workflow-support/
2022. 1. 27	813.vb_d7c3d2984a_0	workflow-support.hpi
Plain Credentials	https://updates.jenkins-ci.org/download/plugins/plain-credentials/
2022. 1. 27 	1.8	plain-credentials.hpi
Plugin Utilities API Plugin	https://updates.jenkins-ci.org/download/plugins/plugin-util-api/
2022. 1. 27	2.13.0	plugin-util-api.hpi
Popper.js 2 API Plugin	https://updates.jenkins-ci.org/download/plugins/popper2-api/
2022. 1. 28 	2.11.2-1	popper2-api.hpi
Popper.js API Plugin	https://updates.jenkins-ci.org/download/plugins/popper-api/
2022. 1. 27 	1.16.1-2	popper-api.hpi
Pub-Sub "light" Bus	https://updates.jenkins-ci.org/download/plugins/pubsub-light/
2022. 1. 27	1.16	pubsub-light.hpi
REST API for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-rest/
2022. 1. 27	1.25.2	blueocean-rest.hpi
REST Implementation for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-rest-impl/
2022. 1. 27	1.25.2	blueocean-rest-impl.hpi
SCM API Plugin	https://updates.jenkins-ci.org/download/plugins/scm-api/
2022. 1. 27 	2.6.5	scm-api.hpi
Script Security Plugin	https://updates.jenkins-ci.org/download/plugins/script-security/
2022. 1. 27 	1131.v8b_b_5eda_c328e	script-security.hpi
Server Sent Events (SSE) Gateway Plugin	https://updates.jenkins-ci.org/download/plugins/sse-gateway/
2022. 1. 28	1.25	sse-gateway.hpi
Snakeyaml API Plugin	https://updates.jenkins-ci.org/download/plugins/snakeyaml-api/
2022. 1. 27	1.29.1	snakeyaml-api.hpi
SSH Credentials Plugin	https://updates.jenkins-ci.org/download/plugins/ssh-credentials/
2022. 1. 27 	1.19	ssh-credentials.hpi
SSH server	https://updates.jenkins-ci.org/download/plugins/sshd/
2022. 1. 27 	3.1.0	sshd.hpi
Structs Plugin	https://updates.jenkins-ci.org/download/plugins/structs/
2022. 1. 27 	308.v852b473a2b8c	structs.hpi
Token Macro Plugin	https://updates.jenkins-ci.org/download/plugins/token-macro/
2022. 1. 27 	267.vcdaea6462991	token-macro.hpi
Trilead API Plugin	https://updates.jenkins-ci.org/download/plugins/trilead-api/
2022. 1. 27 	1.0.13	trilead-api.hpi
Variant Plugin	https://updates.jenkins-ci.org/download/plugins/variant/
2022. 1. 27 	1.4	variant.hpi
Web for Blue Ocean	https://updates.jenkins-ci.org/download/plugins/blueocean-web/
2022. 1. 27	1.25.2	blueocean-web.hpi
Lockable Resources plugin	https://updates.jenkins-ci.org/download/plugins/lockable-resources/
2022. 2. 04	2.13	lockable-resources.hpi
Pipeline	https://updates.jenkins-ci.org/download/plugins/workflow-aggregator/
2022. 2. 04	2.6	workflow-aggregator.hpi
Pipeline: Stage View	https://updates.jenkins-ci.org/download/plugins/pipeline-stage-view/
2022. 2. 04	2.21	pipeline-stage-view.hpi
JavaScript GUI Lib: Moment.js bundle plugin	https://updates.jenkins-ci.org/download/plugins/momentjs/
2022. 2. 04	1.1.1	momentjs.hpi
JavaScript GUI Lib: Handlebars bundle plugin	https://updates.jenkins-ci.org/download/plugins/handlebars/
2022. 2. 04	3.0.8	handlebars.hpi
Pipeline: REST API Plugin	https://updates.jenkins-ci.org/download/plugins/pipeline-rest-api/
2022. 2. 04	2.21	pipeline-rest-api.hpi
Post build task	https://updates.jenkins.io/download/plugins/postbuild-task/
2022. 2. 08	1.9	postbuild-task.hpi
Jenkins Plugin 파일 목록

파일	변경됨
파일 ace-editor.hpi
2022-01-27 by IT기획팀

파일 ant.hpi
2022-01-28 by IT기획팀

파일 apache-httpcomponents-client-4-api.hpi
2022-01-27 by IT기획팀

파일 authentication-tokens.hpi
2022-01-28 by IT기획팀

파일 blueocean.hpi
2022-01-27 by IT기획팀

파일 blueocean-autofavorite.hpi
2022-01-27 by IT기획팀

파일 blueocean-bitbucket-pipeline.hpi
2022-01-27 by IT기획팀

파일 blueocean-commons.hpi
2022-01-27 by IT기획팀

파일 blueocean-config.hpi
2022-01-27 by IT기획팀

파일 blueocean-core-js.hpi
2022-01-27 by IT기획팀

파일 blueocean-dashboard.hpi
2022-01-27 by IT기획팀

파일 blueocean-display-url.hpi
2022-01-27 by IT기획팀

파일 blueocean-events.hpi
2022-01-27 by IT기획팀

파일 blueocean-executor-info.hpi
2022-01-27 by IT기획팀

파일 blueocean-github-pipeline.hpi
2022-01-27 by IT기획팀

파일 blueocean-git-pipeline.hpi
2022-01-27 by IT기획팀

파일 blueocean-i18n.hpi
2022-01-27 by IT기획팀

파일 blueocean-jira.hpi
2022-01-27 by IT기획팀

파일 blueocean-jwt.hpi
2022-01-27 by IT기획팀

파일 blueocean-personalization.hpi
2022-01-27 by IT기획팀

파일 blueocean-pipeline-api-impl.hpi
2022-01-27 by IT기획팀

파일 blueocean-pipeline-editor.hpi
2022-01-27 by IT기획팀

파일 blueocean-pipeline-scm-api.hpi
2022-01-27 by IT기획팀

파일 blueocean-rest.hpi
2022-01-27 by IT기획팀

파일 blueocean-rest-impl.hpi
2022-01-27 by IT기획팀

파일 blueocean-web.hpi
2022-01-27 by IT기획팀

파일 bootstrap4-api.hpi
2022-01-27 by IT기획팀

파일 bootstrap5-api.hpi
2022-01-27 by IT기획팀

파일 branch-api.hpi
2022-01-27 by IT기획팀

파일 caffeine-api.hpi
2022-01-27 by IT기획팀

파일 checks-api.hpi
2022-01-27 by IT기획팀

파일 cloudbees-bitbucket-branch-source.hpi
2022-01-28 by IT기획팀

파일 cloudbees-folder.hpi
2022-01-27 by IT기획팀

파일 credentials.hpi
2022-01-27 by IT기획팀

파일 credentials-binding.hpi
2022-01-27 by IT기획팀

파일 display-url-api.hpi
2022-01-27 by IT기획팀

파일 durable-task.hpi
2022-01-27 by IT기획팀

파일 echarts-api.hpi
2022-01-27 by IT기획팀

파일 favorite.hpi
2022-01-27 by IT기획팀

파일 font-awesome-api.hpi
2022-01-27 by IT기획팀

파일 git.hpi
2022-01-28 by IT기획팀

파일 git-client.hpi
2022-01-27 by IT기획팀

파일 github.hpi
2022-01-28 by IT기획팀

파일 github-api.hpi
2022-01-28 by IT기획팀

파일 github-branch-source.hpi
2022-01-28 by IT기획팀

파일 gitlab-plugin.hpi
2022-01-28 by IT기획팀

파일 git-server.hpi
2022-01-27 by IT기획팀

파일 handlebars.hpi
2022-02-04 by IT기획팀

파일 handy-uri-templates-2-api.hpi
2022-01-28 by IT기획팀

파일 htmlpublisher.hpi
2022-01-28 by IT기획팀

파일 jackson2-api.hpi
2022-01-27 by IT기획팀

파일 javadoc.hpi
2022-01-28 by IT기획팀

파일 javax-activation-api.hpi
2022-01-27 by IT기획팀

파일 javax-mail-api.hpi
2022-01-27 by IT기획팀

파일 jenkins-design-language.hpi
2022-01-27 by IT기획팀

파일 jersey2-api.hpi
2022-01-27 by IT기획팀

파일 jira.hpi
2022-01-27 by IT기획팀

파일 jjwt-api.hpi
2022-01-28 by IT기획팀

파일 jquery3-api.hpi
2022-01-27 by IT기획팀

파일 jsch.hpi
2022-01-27 by IT기획팀

파일 junit.hpi
2022-01-27 by IT기획팀

파일 lockable-resources.hpi
2022-02-04 by IT기획팀

파일 mailer.hpi
2022-01-27 by IT기획팀

파일 matrix-project.hpi
2022-01-27 by IT기획팀

파일 maven-plugin.hpi
2022-01-28 by IT기획팀

파일 momentjs.hpi
2022-02-04 by IT기획팀

파일 okhttp-api.hpi
2022-01-28 by IT기획팀

파일 pipeline-build-step.hpi
2022-01-28 by IT기획팀

파일 pipeline-graph-analysis.hpi
2022-01-28 by IT기획팀

파일 pipeline-input-step.hpi
2022-01-28 by IT기획팀

파일 pipeline-milestone-step.hpi
2022-01-28 by IT기획팀

파일 pipeline-model-api.hpi
2022-01-28 by IT기획팀

파일 pipeline-model-definition.hpi
2022-01-28 by IT기획팀

파일 pipeline-model-extensions.hpi
2022-01-28 by IT기획팀

파일 pipeline-rest-api.hpi
2022-02-04 by IT기획팀

파일 pipeline-stage-step.hpi
2022-01-28 by IT기획팀

파일 pipeline-stage-tags-metadata.hpi
2022-01-28 by IT기획팀

파일 pipeline-stage-view.hpi
2022-02-04 by IT기획팀

파일 plain-credentials.hpi
2022-01-27 by IT기획팀

파일 plugin-util-api.hpi
2022-01-27 by IT기획팀

파일 popper2-api.hpi
2022-01-28 by IT기획팀

파일 popper-api.hpi
2022-01-27 by IT기획팀

파일 postbuild-task.hpi
2022-02-08 by IT기획팀

파일 pubsub-light.hpi
2022-01-27 by IT기획팀

파일 scm-api.hpi
2022-01-27 by IT기획팀

파일 script-security.hpi
2022-01-27 by IT기획팀

파일 snakeyaml-api.hpi
2022-01-27 by IT기획팀

파일 sse-gateway.hpi
2022-01-28 by IT기획팀

파일 ssh-credentials.hpi
2022-01-27 by IT기획팀

파일 sshd.hpi
2022-01-27 by IT기획팀

파일 structs.hpi
2022-01-27 by IT기획팀

파일 token-macro.hpi
2022-01-27 by IT기획팀

파일 trilead-api.hpi
2022-01-27 by IT기획팀

파일 variant.hpi
2022-01-27 by IT기획팀

파일 workflow-aggregator.hpi
2022-02-04 by IT기획팀

파일 workflow-api.hpi
2022-01-27 by IT기획팀

파일 workflow-basic-steps.hpi
2022-01-28 by IT기획팀

파일 workflow-cps.hpi
2022-01-27 by IT기획팀

파일 workflow-cps-global-lib.hpi
2022-01-27 by IT기획팀

파일 workflow-durable-task-step.hpi
2022-01-27 by IT기획팀

파일 workflow-job.hpi
2022-01-27 by IT기획팀

파일 workflow-multibranch.hpi
2022-01-27 by IT기획팀

파일 workflow-scm-step.hpi
2022-01-27 by IT기획팀

파일 workflow-step-api.hpi
2022-01-27 by IT기획팀

파일 workflow-support.hpi
2022-01-27 by IT기획팀


Pipeline: API
플러그인 등록
Jenkins 관리 - 플러그인 관리 메뉴 접근
 
고급 - Deploy Plugin 에서 *.hpi 파일 등록 후 Deploy 수행
 
또는 plugin 디렉토리에 hpi 파일 업로드
[root@almt01 plugins]# pwd
/home/docker/jenkins/data/plugins
[root@almt01 plugins]# ls -al | grep .hpi
-rw-r--r--  1 root root     60849  1월 27 10:52 blueocean-autofavorite.hpi
-rw-r--r--  1 root root     90864  1월 27 10:52 blueocean-bitbucket-pipeline.hpi
-rw-r--r--  1 root root    628997  1월 27 10:52 blueocean-commons.hpi
-rw-r--r--  1 root root     61356  1월 27 10:52 blueocean-config.hpi
-rw-r--r--  1 root root   1076075  1월 27 10:52 blueocean-core-js.hpi
-rw-r--r--  1 root root   2745160  1월 27 10:52 blueocean-dashboard.hpi
-rw-r--r--  1 root root    596777  1월 27 10:52 blueocean-display-url.hpi
-rw-r--r--  1 root root     23995  1월 27 10:52 blueocean-events.hpi
-rw-r--r--  1 root root      6242  1월 27 10:52 blueocean-executor-info.hpi
-rw-r--r--  1 root root     51994  1월 27 10:52 blueocean-git-pipeline.hpi
-rw-r--r--  1 root root     66293  1월 27 10:52 blueocean-github-pipeline.hpi
-rw-r--r--  1 root root     15282  1월 27 10:52 blueocean-i18n.hpi
-rw-r--r--  1 root root     14187  1월 27 10:52 blueocean-jira.hpi
-rw-r--r--  1 root root    277928  1월 27 10:52 blueocean-jwt.hpi
-rw-r--r--  1 root root    703631  1월 27 10:52 blueocean-personalization.hpi
-rw-r--r--  1 root root    191468  1월 27 10:52 blueocean-pipeline-api-impl.hpi
-rw-r--r--  1 root root   1057575  1월 27 10:52 blueocean-pipeline-editor.hpi
-rw-r--r--  1 root root     34451  1월 27 10:52 blueocean-pipeline-scm-api.hpi
-rw-r--r--  1 root root    966458  1월 27 10:52 blueocean-rest-impl.hpi
-rw-r--r--  1 root root    103015  1월 27 10:52 blueocean-rest.hpi
-rw-r--r--  1 root root   1413910  1월 27 10:52 blueocean-web.hpi
-rw-r--r--  1 root root      7973  1월 27 10:52 blueocean.hpi
[root@almt01 plugins]# 
Code Block 20 jenkins hpi plugin upload

Jenkins 재기동
 
[Jenkins] 사용자 생성
Jenkins 관리 → Manage Users → 사용자 생성 → Create User 진행
	진행화면
1	 
2	 
3	 
4	 
Nexus
하위페이지
•	[Nexus] Nexus Repository 3
o	[Nexus] Nexus Repository 3 운영자 가이드
	[Nexus] Maven Repository 생성방법
	[Nexus] Nexus Repository 3 설치/실행 안내
	[Nexus] Repository 라이브러리 수기 업로드 방법
	[Nexus] 계정 권한 설정
	[Nexus] 계정생성
o	[Nexus] Nexus Repository 3 사용자 가이드
	[Nexus] 메이븐에 Nexus Repository 미러링 설정 방법
•	[Nexus] 기타
o	[Nexus] Nexus Repository 3 듀얼 구성 테스트
o	[Nexus] 라이브러리 일괄 업로드 방법
[Nexus] Nexus Repository 3
[Nexus] Nexus Repository 3 운영자 가이드
Maven Repository 생성
 
•	Repository → Repositories → Create Repository 진행
 
•	mavne2 (hosted)로 선택을 함 (Proxy 같은 경우 외부 Repository에 대하여  proxy 역할을 하는 Repository임 / 외부랑 연결이 안되서 Hosted로 테스트 진행)
 
•	Name 설정 기입하고 정책을 용도에 맞게 지정해서 생성 진행
[Nexus] Nexus Repository 3 설치/실행 안내
docker 를 이용한 Nexus Repository 3 설치
bastion host 다운로드 대상
docker image name	Docker Pull Command	version
nexus3 latest version	docker pull sonatype/nexus3	3.373(2022. 2. 15  기준)
또는 wget https://download.sonatype.com/nexus/3/nexus-3.37.3-02-unix.tar.gz 에서 다운로드(tar 버전)
이미지 추출(bastion host)
[root@openwebt01 ~]# docker pull sonatype/nexus3
Using default tag: latest
latest: Pulling from sonatype/nexus3
26f1167feaf7: Pull complete 
adffa6963146: Pull complete 
e88dfbe0ef6a: Pull complete 
0d43c5e95446: Downloading [===========================================>       ]  180.5MB/208.6MB
8ff7b45a7e29: Download complete 
Digest: sha256:eff4fb12346ceb5cd424732ee9f2765c0db0f8d5032cdb2f7f7e17acc349f651
Status: Downloaded newer image for sonatype/nexus3:latest
docker.io/sonatype/nexus3:latest
[root@openwebt01 jenkins]# docker save -o nexus3.tar sonatype/nexus3:latest
[root@openwebt01 pg]# chown pg:mas_g nexus3.tar 
[root@openwebt01 pg]# ls -al | grep nexus
-rw-------. 1 root root   675463168  2월 15 08:43 nexus3.tar
[root@openwebt01 pg]# 
Code Block 21 nexus3 docker save

이미지 업로드
[root@almt01 nexus3]# docker images
REPOSITORY               TAG            IMAGE ID       CREATED        SIZE
jenkins/jenkins          latest         1c520775844c   3 weeks ago    442MB
gitlab/gitlab-ee         latest         4062f34e61f6   2 months ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   17d5117a2e37   2 years ago    1.76GB
[root@almt01 nexus3]# docker load < nexus3.tar 
352ba846236b: Loading layer [==================================================>]  234.7MB/234.7MB
3ba8c926eef9: Loading layer [==================================================>]  20.48kB/20.48kB
fb1fa13dcf2f: Loading layer [==================================================>]   5.12kB/5.12kB
bd0533a191cf: Loading layer [==================================================>]    260MB/260MB
4c2a55dcb2bc: Loading layer [==================================================>]  180.6MB/180.6MB
Loaded image: sonatype/nexus3:latest
[root@almt01 nexus3]# docker images
REPOSITORY               TAG            IMAGE ID       CREATED        SIZE
jenkins/jenkins          latest         1c520775844c   3 weeks ago    442MB
sonatype/nexus3          latest         589f7296a4a2   6 weeks ago    655MB
gitlab/gitlab-ee         latest         4062f34e61f6   2 months ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   17d5117a2e37   2 years ago    1.76GB
[root@almt01 nexus3]# 
Code Block 22 nexus3 docker load

docker 를 이용한 Nexus Repository 3 실행
방법1) docker run 활용
nexus3 docker run
[root@almt01 nexus3]# docker images --digests
REPOSITORY               TAG            DIGEST    IMAGE ID       CREATED        SIZE
jenkins/jenkins          latest         <none>    1c520775844c   3 weeks ago    442MB
sonatype/nexus3          latest         <none>    589f7296a4a2   6 weeks ago    655MB
gitlab/gitlab-ee         latest         <none>    4062f34e61f6   2 months ago   2.5GB
store/gitlab/gitlab-ce   11.10.4-ce.0   <none>    17d5117a2e37   2 years ago    1.76GB
[root@almt01 nexus3]# docker run -d -p 8081:8081 -v /home/docker/nexus3/data:/nexus-data -v /home/docker/nexus3/data:/sonatype-work --name nexus sonatype/nexus3
6d3de97fa447773f228a8a947f5e646c78c453e7db11bc6b0d8c38532c8cca02
[root@almt01 nexus3]# docker ps
CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS                 PORTS                                              NAMES
6d3de97fa447   sonatype/nexus3   "sh -c ${SONATYPE_DI…"   About a minute ago   Up About a minute      0.0.0.0:8081->8081/tcp                        nexus
b284f4e20fe3   4062f34e61f6      "/assets/wrapper"        2 weeks ago      Up 2 weeks (healthy)   0.0.0.0:80->80/tcp, 22/tcp, 0.0.0.0:443->443/tcp   gitlab
2de33a1a5996   1c520775844c      "/sbin/tini -- /usr/…"   2 weeks ago      Up 2 weeks             0.0.0.0:8080->8080/tcp, 0.0.0.0:4000->50000/tcp   jenkins
Code Block 23 nexus3 docker run

2) docker compose 활용
프로젝트 디렉토리 생성 후 docker-compose.yml 파일 생성방법
nexus3 docker-compose.yml
version: '3.0'
services:
  nexus3:
    privileged : true
    build: .
    image: '589f7296a4a2'
    #restart: always
    hostname: 'nexus.nicepay.co.kr'
    container_name : 'nexus3'
    environment:
      TZ : "Asia/Seoul"
    ports:
      - '8081:8081'
    volumes:
      - '/home/docker/nexus3/data:/nexus-data'
      - '/home/docker/nexus3/data:/sonatype-work'
Code Block 24 nexus3 docker-compose.yml

docker volumes 대상 디렉토리 owner 변경
chown (-R) 200
[root@almt01 docker]# chown -R 200:docker nexus3
[root@almt01 docker]# ls -al
[root@almt01 docker]# ls -al | grep nexus3
drwxrwxr-x   3    200 docker       18  2월 15 10:17 nexus3
[root@almt01 docker]# 
Code Block 25 nexus3 volumes chwon

docker compose 실행
nexus3 docker compose up
[root@almt01 nexus3]# docker compose up -d
[+] Running 2/2
 ⠿ Network nexus3_default  Created                                                                                                                   0.1s
 ⠿ Container nexus3        Started                                                                                                                   0.4s
[root@almt01 nexus3]# 
Code Block 26 nexus3 docker compose up

Nexus Repository 3 실행 및 최초 설치
nexus3 사이트 접속(지정포트 : 8081, docker 설정한 port 로 접속)
http://172.32.161.36:8081/
 
[Nexus] Repository 라이브러리 수기 업로드 방법
업로드 진행
 
•	박스 모양 클릭 → Upload → 업로드 대상 Repository 클릭
•	Browse 버튼을 통하여 해당 jar파일 라이브러리를 업로드함 
•	Component coordinate에 필요한 정보를 기입후 Upload 진행 
업로드 라이브러리 확인
 
•	업로드된 라이브러리는 Browse 탭에서 확인이 가능함
•	명시된 버젼과 정보 리스트
계정 Role 생성 방법
 
•	Roles 탭에서 권한 종류 확인이 가능함
•	Create Role을  클릭하여 권한 추가를 진행함
 
•	Available 필터안에 해당 Repository 네임에 관련 키워드를 입력하여 권한을 줌
•	read / edit / delete / browse 등이 존재함 
•	해당 Role을 만들고 Role을 User에 할당 진행하면 Repository에 대한 권한이 부여됨
[Nexus] 계정생성
Server Configuration → Users → Create Local User

화면 순서 진행	
 	•	계정관리 페이지 접근
•	Create Local User 버튼클릭

 	•	계정 필요사항 기입
•	권한 설정 후 생성
[Nexus] Nexus Repository 3 사용자 가이드
[Nexus] 메이븐에 Nexus Repository 미러링 설정 방법
선행 확인 
 
•	메이븐이 사전 설치가 되어야 함 (설치방법은 생략)
•	이클립스 → Windows → Preferences → Maven → User Settings 접근하여 설치된 메이븐 settings.xml로 되어있는 지 확인필요 
•	Apply and Close로 세팅 확인 
Nexus  Repository 미러링 설정 진행 및 확인
 
•	Nexus에 로그인
•	Browse 탭 클릭 → 사용할 Repository 주소 URL탭의 Copy버튼으로 복사
 
•	server에 Repository 주소에 접근가능한 계정 아이디와 비밀번호를 기입함
•	mirrors에 미러링해서 사용하는 복사한 Repository 주소를 기입
•	해당 settings.xml을 저장함 (settings.xml을 통하여 미러링 주소가 설정이 됨)
 
•	메이븐 빌드 진행시 설정된 settings.xml에 계정이 지정한 Repository에 접근할 권한이 없는경우 위의 이미지처럼 다운로드가 실패됨
 
•	정상적으로 접근권한이 있으면 로컬 Repository에 pom.xml에 설정한 해당 디펜던시가 없는 경우 위의 이미지처럼 설정한 원격지에 다운로드가 진행되고 빌드가 성공
 
•	Local에 디펜던시가 다운받은 것을 확인할 수 있음
[Nexus] 기타
[Nexus] Nexus Repository 3 듀얼 구성 테스트
네이버 클라우드를 통하여 테스트 진행
작업환경
네이버클라우드 서버정보	사양
ncloud001 (115.85.180.83)	Standard (4core 8GB Memory)
ncloud002 (118.67.128.129)	Standard (4core 8GB Memory)

요약 및 구성도
설치 항목	비고
Nexus OSS 3.37	넥서스 레포지토리
Maven 3.6.3	메이븐 (스크립트 테스트용도)
 

넥서스 설정
 
 
•	ncloud001에 설치된 넥서스 레포지토리는 메이븐 레포를 바라보게 설정
•	ncloud002에 설치된 넥서스 레포지토리에는 ncloud001에 생성한 레포를 바라보게 설정
•	ncloud001에 설치된 넥서스 접근 권한은 annoymous로 설정해야함
메이븐 설정 
<project>
<modelVersion>4.0.0</modelVersion> 
<groupId>kr.co.nicepay</groupId> 
<artifactId>nexus-proxy</artifactId> 
<version>1.0-SNAPSHOT</version> 
 
<dependencies> 
<dependency> 
  <groupId>junit</groupId> 
  <artifactId>junit</artifactId> 
  <version>4.10</version> 
</dependency>
</dependencies> 
</project>
Code Block 27  ncloud002 (메이븐 pom.xml 설정)

<?xml version="1.0" encoding="UTF-8"?>
 
<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at
 
    http://www.apache.org/licenses/LICENSE-2.0
 
Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->
 
<!--
 | This is the configuration file for Maven. It can be specified at two levels:
 |
 |  1. User Level. This settings.xml file provides configuration for a single user,
 |                 and is normally provided in ${user.home}/.m2/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -s /path/to/user/settings.xml
 |
 |  2. Global Level. This settings.xml file provides configuration for all Maven
 |                 users on a machine (assuming they're all using the same Maven
 |                 installation). It's normally provided in
 |                 ${maven.conf}/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -gs /path/to/global/settings.xml
 |
 | The sections in this sample file are intended to give you a running start at
 | getting the most out of your Maven installation. Where appropriate, the default
 | values (values used when the setting is not specified) are provided.
 |
 |-->
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository-->
  <localRepository>/home/nexus/apache-maven-3.6.3/repository</localRepository>
  
 
  <!-- interactiveMode
   | This will determine whether maven prompts you when it needs input. If set to false,
   | maven will use a sensible default value, perhaps based on some other setting, for
   | the parameter in question.
   |
   | Default: true
  <interactiveMode>true</interactiveMode>
  -->
 
  <!-- offline
   | Determines whether maven should attempt to connect to the network when executing a build.
   | This will have an effect on artifact downloads, artifact deployment, and others.
   |
   | Default: false
  <offline>false</offline>
  -->
 
  <!-- pluginGroups
   | This is a list of additional group identifiers that will be searched when resolving plugins by their prefix, i.e.
   | when invoking a command line like "mvn prefix:goal". Maven will automatically add the group identifiers
   | "org.apache.maven.plugins" and "org.codehaus.mojo" if these are not already contained in the list.
   |-->
  <pluginGroups>
    <!-- pluginGroup
     | Specifies a further group identifier to use for plugin lookup.
    <pluginGroup>com.your.plugins</pluginGroup>
    -->
  </pluginGroups>
 
  <!-- proxies
   | This is a list of proxies which can be used on this machine to connect to the network.
   | Unless otherwise specified (by system property or command-line switch), the first proxy
   | specification in this list marked as active will be used.
   |-->
  <proxies>
    <!-- proxy
     | Specification for one proxy, to be used in connecting to the network.
     |
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    -->
  </proxies>
 
  <!-- servers
   | This is a list of authentication profiles, keyed by the server-id used within the system.
   | Authentication profiles can be used whenever maven must make a connection to a remote server.
   |-->
  <servers>
    <!-- server
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     |
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are
     |       used together.
     |-->
    <server>
      <id>nexus</id>
      <username>admin</username>
      <password>skdltm100%</password>
    </server>
    
 
    <!-- Another sample, using keys to authenticate.
    <server>
      <id>siteServer</id>
      <privateKey>/path/to/private/key</privateKey>
      <passphrase>optional; leave empty if not used.</passphrase>
    </server>
    -->
  </servers>
 
  <!-- mirrors
   | This is a list of mirrors to be used in downloading artifacts from remote repositories.
   |
   | It works like this: a POM may declare a repository to use in resolving certain artifacts.
   | However, this repository may have problems with heavy traffic at times, so people have mirrored
   | it to several places.
   |
   | That repository definition will have a unique id, so we can create a mirror reference for that
   | repository, to be used as an alternate download site. The mirror site will be the preferred
   | server for that repository.
   |-->
  <mirrors>
    <!-- mirror
     | Specifies a repository mirror site to use instead of a given repository. The repository that
     | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
     | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
     |-->
    <mirror>
      <id>nexus</id>
      <mirrorOf>*</mirrorOf>
      <url>http://localhost:8081/repository/maven-proxy/</url>
    </mirror>
  </mirrors>
 
  <!-- profiles
   | This is a list of profiles which can be activated in a variety of ways, and which can modify
   | the build process. Profiles provided in the settings.xml are intended to provide local machine-
   | specific paths and repository locations which allow the build to work in the local environment.
   |
   | For example, if you have an integration testing plugin - like cactus - that needs to know where
   | your Tomcat instance is installed, you can provide a variable here such that the variable is
   | dereferenced during the build process to configure the cactus plugin.
   |
   | As noted above, profiles can be activated in a variety of ways. One way - the activeProfiles
   | section of this document (settings.xml) - will be discussed later. Another way essentially
   | relies on the detection of a system property, either matching a particular value for the property,
   | or merely testing its existence. Profiles can also be activated by JDK version prefix, where a
   | value of '1.4' might activate a profile when the build is executed on a JDK version of '1.4.2_07'.
   | Finally, the list of active profiles can be specified directly from the command line.
   |
   | NOTE: For profiles defined in the settings.xml, you are restricted to specifying only artifact
   |       repositories, plugin repositories, and free-form properties to be used as configuration
   |       variables for plugins in the POM.
   |
   |-->
  <profiles>
    <!-- profile
     | Specifies a set of introductions to the build process, to be activated using one or more of the
     | mechanisms described above. For inheritance purposes, and to activate profiles via <activatedProfiles/>
     | or the command line, profiles have to have an ID that is unique.
     |
     | An encouraged best practice for profile identification is to use a consistent naming convention
     | for profiles, such as 'env-dev', 'env-test', 'env-production', 'user-jdcasey', 'user-brett', etc.
     | This will make it more intuitive to understand what the set of introduced profiles is attempting
     | to accomplish, particularly when you only have a list of profile id's for debug.
     |
     | This profile example uses the JDK version to trigger activation, and provides a JDK-specific repo.
    <profile>
      <id>jdk-1.4</id>
 
      <activation>
        <jdk>1.4</jdk>
      </activation>
 
      <repositories>
        <repository>
          <id>jdk14</id>
          <name>Repository for JDK 1.4 builds</name>
          <url>http://www.myhost.com/maven/jdk14</url>
          <layout>default</layout>
          <snapshotPolicy>always</snapshotPolicy>
        </repository>
      </repositories>
    </profile>
    -->
 
    <!--
     | Here is another profile, activated by the system property 'target-env' with a value of 'dev',
     | which provides a specific path to the Tomcat instance. To use this, your plugin configuration
     | might hypothetically look like:
     |
     | ...
     | <plugin>
     |   <groupId>org.myco.myplugins</groupId>
     |   <artifactId>myplugin</artifactId>
     |
     |   <configuration>
     |     <tomcatLocation>${tomcatPath}</tomcatLocation>
     |   </configuration>
     | </plugin>
     | ...
     |
     | NOTE: If you just wanted to inject this configuration whenever someone set 'target-env' to
     |       anything, you could just leave off the <value/> inside the activation-property.
     |
    <profile>
      <id>env-dev</id>
 
      <activation>
        <property>
          <name>target-env</name>
          <value>dev</value>
        </property>
      </activation>
 
      <properties>
        <tomcatPath>/path/to/tomcat/instance</tomcatPath>
      </properties>
    </profile>
    -->
  </profiles>
 
  <!-- activeProfiles
   | List of profiles that are active for all builds.
   |
  <activeProfiles>
    <activeProfile>alwaysActiveProfile</activeProfile>
    <activeProfile>anotherAlwaysActiveProfile</activeProfile>
  </activeProfiles>
  -->
</settings>
Code Block 28 ncloud002 (메이븐 setting.xml 설정


테스트 확인
 
•	bin 경로에 있는 pom.xml 스크립트를 실행
•	./mvn package (디펜던시가 정상적으로 빌드해서 다운받아지면 BUILD SUCCESS가 됨)
테스트 시나리오
시나리오 구성 정보	확인체크
1.	ncloud001에 설치된 넥서스, 프록시 레포지토리(메이븐 레포지토리에 연결된 레포지토리) 구성
2.	ncloud001에 설치된 메이븐에 setting.xml에 수정하여 프록시 레포지토리에 접근하도록 구성 설정
3.	ncloud001에 설치된 메이븐에서 pom.xml에 정의한 스크립트 기반으로 디펜던시를 프록시 레포지토리를 통해 정상적으로 패키지하여 다운로드하는지 확인	 	 
1.	ncloud002에 설치된 넥서스에서 ncloud001의 프록시 레포지토리를 바라보는 프록시 레포지토리를 구성함
2.	ncloud002의 프록시 레포지토리는 특정계정의 권한이 있어야만 접근 가능하게 설정 구성
3.	ncloud002에 설치된 메이븐에서 pom.xml 정의한 스크립트 기반으로 디펜던시를 정상적으로 패키지하여 다운로드하는지 확인	 	 
1.	메이븐 pom.xml을 통하여 디펜던시를 다운받는 경우, 넥서스에서 해당 라이브러리 관련 로그를 남기는지 확인	 	 

기타
요약	비고
넥서스 디펜던시
다운로드 로그 확인 경로	 
 
•	audit.log에 디펜던시가 다운될 경우 해당 로그가 생김
[Nexus] 라이브러리 일괄 업로드 방법
선행 확인
•	bash shell을 실행할 수 있는 환경에서 업로드 진행
•	window의 경우 로컬에 git 설치시 shell 사용 가능
         (intellij 사용자의 경우 git을 설치해야 gitlab과 연동이 가능하므로 git설치를 권장드립니다.)

Nexus3에 Repository 생성
•	cloud-release 생성 확인(repository 생성은 Nexus Repository3 운영자 가이드 참조)
 
업로드 위치 확인
•	업로드 하고자 하는 repository하위에 업로드 shell 파일 위치 확인
•	windows 로컬 기준 default repository의 위치는 C:\user\{유저명}\.m2\repository\
•	shell 파일 : nexus_bulk_upload.sh

 
nexus_bulk_upload.sh 설정
 
•	username, password는 본인 nexus계정 설정
•	nexusurl은 업로드할 repository 경로 설정(nexus browser에서 URL COPY 클릭하면 해당 경로의 URL확인 가능)
•	설정 완료 후 shell 실행
[기타]
하위 페이지
•	[Gitlab + Jenkins] Gitlab 과 Jenkins 연동
•	[Jenkins] Freestyle Project 설정을 통한 Gitlab 연동 (Pipeline X)
[Gitlab + Jenkins] Gitlab 과 Jenkins 연동

•	Gitlab 에서 AccessToken 발급
•	Jenkins 프로젝트 생성
•	Gitlab 웹훅 생성
•	Jenkins 설정
Gitlab 에서 AccessToken 발급
project 선택 후 Settings - Access Tokens 접근
Token name 에 생성할 토큰의 이름을 입력하고 scope 를 api, read_api, read_repository 를 선택 후 Create project access token 클릭
 
Your new project access token 의 token 정보를 복사하여 보관
 
Jenkins 프로젝트 생성
'새로운 Item' 메뉴에서 pipeline 프로젝트 생성
 
톱니바퀴 모양의 구성 선택
 
 
build Triggers 항목에 'Build when a change is pushed to GitLab. GitLab webhook URL:' 을 클릭 후 '고급...' 항목 클릭
 
Secret token 에서 Generate 클릭해 토큰 생성
 
저장 버튼 클릭 후 저장
Gitlab 웹훅 생성
project 선택 후 Settings - Webhooks 접근
 
URL 과 Secret token 에 Jenkins 의 URL 과 token 등록,  Push 할 branch 를 Push events 에 등록
 
Add webhook 버튼 클릭
 
Webhooks 하단에 추가된 webhook 확인
 
테스트를 위해 추가된 webhook 의 테스트 버튼에서 Push events 클릭
 
상단에 'Hook executed successfully: HTTP 200' 메시지 확인
 
Jenkins 설정
Jenkins 관리 - Security - Manage Credentials 접근
 
Stores scoped to Jenkins 의 Jenkins 클릭
 
Global credentials(unrestricted) 클릭
 
Add Credentials 클릭
 
Kind : Gitlab API token 선택, API token 에 Gitlab 에서 발급한 access token 등록, ID 입력
 
등록 신용증명 확인
 
Jenkins 관리 - 시스템 설정 접근
 
Gitlab 환경설정 등록(이름, Gitlab URL, 신용증명)
 
Test Connection 버튼 클릭하여 테스트 진행, success 메시지 확인
 
저장 버튼 클릭 후 저장
[Jenkins] Freestyle Project 설정을 통한 Gitlab 연동 (Pipeline X)
순서 : Add Credentials → 새로운 Item / Freestyle project → 소스 코드 관리 → 대시보드 빌드 수행 및 결과 확인
메이븐 빌드까지 X, jenkins 워크스페이스에 해당 Gitlab Repository 딜리버리까지 진행함 

1.Add Credentials
이미지	설명
 	•	http://172.32.161.36:8080/credentials/store/system/domain/_/ 접근
•	Add Credentials 클릭
•	(해당주소에 해당하는 UI를 찾기가 힘들어서 해당 페이지 주소로 접근함)
 	•	Scope Global로 설정
•	Username은 접속하는 Gitlab 아이디를 기입
•	Password는 Gitlab에서 생성한 Access token으로 접근함 (아래 단계에서 생성한 token을 입력)
 
	•	GitLab 페이지에서 로그인 후 User settings 접근
•	Access Tokens 탭에서 접근
•	만료기간 설정
•	Select Scopes에서 필요 권한 설정 후 Token name 기입하여 생성
 	•	생성이 완료되면 new personal access token에서 해당 토큰을 복사함
•	해당 토큰은 한번만 보여지기 때문에 별도로 보관 필요
 	•	생성한 토큰을 Password에 기입하여 저장함

2.새로운 Item / Freestyle project
이미지	설명
 	•	Freestype project 클릭하여 생성
 	•	소스코드 관리탭 클릭
•	git 선택
•	repository URL에 해당 대상 저장소 주소 입력
•	Credentials를 설정 안하면, Failed to로 시작하는 에러문구 발생함
 	•	생성한 Credential을 선택하여 추가
•	Branch 지정은 다른 브랜치로 변경할 경우 변경진행 (Master로 진행하였음)
3. 대시보드를 통한 빌드 수행 및 결과 확인
이미지	설명
 
 	•	소스 커밋 및 push 진행
•	Gitlab 소스 변경 반영 확인
 	•	생성한 Job의 재생 버튼 클릭
 	•	젠킨스가 정상적으로 수행하면, 바뀐점 페이지에서 확인 가능함
 	•	Jenkins workspace에서 해당 Gitlab Repository 변경사항 반영됨


