# Internet & Network & Server

## IP address (Internet Protocol address)

- `ip addr` 리눅스 명령어
- `ifconfig | grep inet` 명령어를 통해 현재 내 기기의 ip주소(private)를 알 수 있다.
- `curl ipinfo.io/ip` 명령어를 통해 현재 내 기기의 public address를 알 수 있다. 이 외에도 public ip주소를 얻는 방법은 다양하다.

위와 같은 방법으로 하나의 public 주소로 인터넷 연결을 가능하게 되는데, router를 통해 연결을 받게되고, 이후 router에서 각 기기의 private 주소로 연결해줌으로 사용될 수 있다.

## Web server

웹 서버를 만드는 다양한 방법 중, 내 컴퓨터를 웹서버로 만드는 방법은 다음과 같은 소프트웨어를 사용할 수 있다:

- Apache
- Nginx
- IIS

### Apache

- `sudo apt-cache search apache`: apache라는 이름을 가진 패키지를 검색하게 된다. 혹은 apache ubuntu 혹은 apache mac 키워드로 검색해서 설치하게 된다.

- `sudo service apache2 start`: 아파치 웹서버 시작하기
- `sudo service apache2 stop`: 중지하기
- `sudo service apache2 restart`: 껏다 키기

Mac 사용시

- `sudo apachectl start`
- `sudo apachectl stop`

그리고 내 컴퓨터의 ip주소:8080(포트넘버는 확인해보기)으로 웹브라우저에서 접속하게 되면 실행됨을 확인할 수 있다.

셀 환경에서 웹브라우징을 할 수 있는 몇가지 프로그램이 있는데 그중: `elinks`를 사용해볼 수 있다. 이 소프트웨어를 사용해서 웹브라우저에 접속할 수 있다.
`sudo apt-get install elinks`: 해당 프로그램 설치
`elinks http://ip주소/`: 쉘환경에서 확인이 가능하다.

### 127.0.0.1 <localhost>

나 자신을 가리킬때 사용되는 약속되어 있는 특수한 ip 주소이다. 이와 같이 약속되어 있는 특수한 도메인 네임는 localhost이다.

### Apache - configuration & log

유닉스 계열에서는 어떤 프로그램이 어떻게 동작하게 될 것인가에 대한 설정 방법은 `/etc/`에 저장되어 있다. 그래서 브라우저에서 어떠한 요청이 왔을때 웹서버에서 어떻게 동작하는지에 대한 설정을 위해 예를든 아파치의 경우 `/etc/apache2/` 에서 설정을 변경시켜줄 수 있다.

`access.log` & `error.log`를 통해 서버에 어떤 요청이 왔는지, 동작하는 상태를 확인할 수 있다. 아파치의 경우 보통 `/var/log/apache2/`에 위치하고 있다.

## SSH (Secure Shell) 원격제어

SSH 프로그램을 사용해서 SSH 서버 그리고 클라이언트를 각 클라이언트와 서버컴퓨터에 설치를 한 후, 클라이언트에서 명령어를 통해 원격으로 서버컴퓨터를 제어할 수 있도록 할 수 있다. 무엇보다 암호화가 되어 있어 보안에 유리하다. 기본 포트로 22를 사용한다.

## Port 포트 & Port forwarding
