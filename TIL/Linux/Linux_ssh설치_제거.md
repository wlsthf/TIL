# Linux_ ssh 설치 / 제거

```sh
# 상태확인
netstat -ntlp
# 활성화 돼있는 포트들이 출력된다.

# 특정 서비스가 동작하는지 확인하는 방법
systemctl status sshd
netstat -ntlp | gerp sshd


# 활성화 돼있는 서비스를 중지시킨다.
systemctl stop geoserver
systemctl stop tomcat
systemctl stop sshd

# 해당 명령어가 들지 않는다면 각 파일 bin폴더로 들어가서 중지파일을 실행시킨다.
cd /some/thing/dir/bin
./shutdown.sh

# ssh제거
yum remove openssh-server

# 설치 유무 확인
rpm -qa | grep ssh

# ssh설치
yum -y install openssh-server

# ssh 서버 시작
systemctl start sshd
systemctl enable sshd

# 서비스 확인
systemctl status sshd
netstat -ntlp | grep sshd

# ssh는 기본적으로 22번 포트이기 때문에 포트변경
systemctl stop sshd
systemctl status sshd
vi /etc/ssh/sshd_config/sshd_config
#PORT 22
# 이부분을 
PORT 9999
# 변경

# 방화벽 설정
firewall-cmd --permanent --zone=public --add-port=9999/tcp
firewall-cmd --reload

# 설정변경후 서비스 재시작
systemctl start sshd
systemctl status sshd
netstat -ntlp | grep sshd

# 기타 프로그램 재실행
systemctl start tomcat
systemctl start geoserver

# 실행이 안된다면 해당 디렉토리로 가서 실행파일 실행
cd /some/thing/dir/bin
./startup.sh

# 상태확인
netstat -ntlp
```

