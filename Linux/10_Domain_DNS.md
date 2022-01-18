# Domain & DNS (Domain Name System)

우리들은 혹은 우리의 컴퓨터는 세상의 모든 ip 주소를 알 수 없다. 그렇기에 보통 우리가 도메인으로 브라우져에 접속하게 되면 DNS에서 전화번호부책 처럼 해당 ip주소를 찾아서 우리에게 알려주게 되고, 그것으로 해당 서버에 접속할 수 있게 된다.

## hosts 파일

DNS가 있기 전에, hosts 파일이란 것이 있었다. 각각의 컴퓨터에 hosts 파일이 있었고 이 파일에는 도메인-ip주소의 정보를 확인할 수 있었다.

`elinks google.com`를 보면 google.com를 확인할 수 있다. `/etc/hosts`에 `127.0.0.1`에 google.com을 등록해놓으면 다시 elinks로 확인했을때 구글이 아닌 내 컴퓨터의 웹서버를 확인할 수 있다.

이는 컴퓨터가 우선 적으로 hosts파일을 확인한 후 없으면 DNS에 요청을 하기 때문이다.

활용도: 예를 들어 내가 운영하고 있는 사이트가 있는데, 업데이트를 진행하고 프러덕션에 빌드를 하기 전에 테스트를 하고 싶으면, 내 컴퓨터에 개발환경을 hosts 파일을 변경해서 우선적으로 테스트해볼 수 있다.
이와 같은 방법으로 해커들의 공격대상이 될 수도 있는 파일이다.

## Domain name

- `/etc/resolv.conf`: 내컴퓨터의 DNS 서버 ip 주소
- `host google.com`: 구글이란 도메인의 ip주소를 알려준다.
- Sub Domain: 각각의 도메인 앞에 prefix를 붙여서 subdomain을 만들어서 각각에 ip주소를 할당해서 서버에 접속할 수 있도로 할 수 있다.

## DNS principle

- `dig +trace [domain name]`: 해당 도메인네임의 ip주소를 알려주는데, 그 사이에 어떤 과정을 거치는지 모두 보여준다.
  - root dns 서버에 물어보고
  - com, ga, io 등등의 dns 서버에 물어보고
  - domain이름 dns 서버에 물어보게된다.
