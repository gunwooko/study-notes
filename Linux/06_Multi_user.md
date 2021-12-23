# Multi users

- `id`: 사용자 정보를 보여준다.
  uid: user id
  gid: group id
- `who`: 현재 시스템에 누가 접속해있는지 알려준다.

# Super(root) user vs user

`sudo`: 관리자의 권한으로 명령어를 실행시킨다.
`su`: Change user ID or become superuser.
`su - root`: 관리자 상태로 옮기기.
리눅스에서는 보통 터미널 앞에 root이 나오고 $가 아닌 #이 뜬다.
`exit`: root 유저에서 로그아웃해서 일반유저로 넘어가기

## Ubuntu에서 관리자로 넘어가기

일반적으로 우분투에서는 관리자로 넘어가는 것이 막혀있다.

- `sudo passwd -u root`: 여기서 `-u`는 unlock이다. 이렇게 함으로 보안을 풀어준다.
- `sudo passwd -l root`: 관리자 보안으로 잠구기.
- 관리자의 홈디렉토리는 `/root` 이다.

# 사용자추가

- `sudo useradd -m hello`: 홈디렉토리에 hello 디렉토리를 만들면서 유저를 추가해준다.
- `sudo passwd hello`: hello가 사용할 비번을 등록한다.
- `su - hello`: hello 유저로 넘어간다.
- `sudo usermod -a -G sudo hello`: hello 유저에게 sudo의 권한을 준다.
