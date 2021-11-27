# Linux Directory Structure (Unix File System Structure)

- `/`: Root directory 가장 최상위
- `/bin`: User Binaries 이곳에는 여러가지 프로그램들이 있다. 실행가능한 프로그램을 binary라고 불리는데, 사용자들이 사용할 수 있는 프로그램이 저장되어 있다.
- `/sbin`: System Binaries 시스템 실행 프로그램이 있다. 루트 유저 혹은 시스템 관리자들이 주로 사용하는 명령어들이 있다. 예) `reboot`
- `/etc`: Configuration Files 설정 파일 프로그램. 운영체제, 설치한 프로그램, 등의 설정을 변경하고 싶을때 예) `wgetrc`
- `/dev`: Device Files
- `/proc`: Process Information
- `/var`: Variable Files. 변경가능한 파일. `bin sbin etc`와 같은 파일은 프로그램을 업데이트 혹은 설정을 변경하기 전까지 변경하지 않는다.
- `/tmp`: Temporary Files 임시 저장 파일. 시스템이 리붓되면 삭제된다.
- `/usr`: User Programs 보통 사용자가 설치하는 프로그램은 `/usr` 아래에 저장이 되고, 운영체재기 기본적으로 저쟁되는 프로그램은 `bin sbin lib`에 저장이 된다.
  - `/usr/bin`
  - `/usr/sbin`
  - `/usr/bin`
- `/home`: Home Directories 사용자들의 디렉토리이다. 이곳 아래에 사용자파일(데이터)이 담긴다. 루트에서 `cd ~` 이렇게 하면 바로 home으로 가게된다.
- `/boot`: Boot Loader Files
- `/lib`: System Libraries
- `/opt`: Optional add-on Applications
- `/mnt`: Mount Directory
- `/media`: Removable Media Devices
- `/srv`: Service Data

# 파일 찾는 법

- `locate 파일이름`: 해당 파일을 찾아 준다.
  `locate` 명령어는 디렉토리를 찾아보는것이 아니라, 데이터베이스에서 정보를 찾아본다.
  그리고 이 데이터베이스를 `mlocate`라고 한다.
  `sudo updatedb`란 명령어를 통해 mlocate란 데이터베이스에 현재 컴퓨터에 있는 여러가지 정보들이 저장이 된다.
  많은 리눅스 시스템에선 하루에 한번씩 이 작업이 작동되도록되어 있다.
  그리고 이미 정리되어 있는 데이터베이스를 찾아보기 때문에 빠르게 찾을 수 있게된다.

- `find`: 실제로 디렉토리를 찾아본다. 현재 상황을 찾아보기 때문에 더욱 정확하다. 또한 사용할 수 있는 옵션등이 다양하다.
  - `find /`이렇게 하면 루트 디렉토리에서 부터 하위로 찾는 것을 의미한다.
  - `find .` 현재 디렉토리에서부터 하위 디렉토리로 찾는 것을 의미한다.
  - `find . -name *.log`: 현재 디렉토리에서부터 .log 란 이름이 들어간 파일을 찾는다.
  - `find . -type f -name hello.txt`: 현재 디랙토리에서부터 hello.txt 이름의 파일 타입을 찾아라.

# 파일 찾는 법 2 & `$PATH` 환경변수

- `whereis` : 실행파일을 찾아주는 명령어다. 여러개의 경로로 찾아 준다.
  - `whereis ls`: ls 명령어가 담긴 경로와 또한 메뉴얼도 리턴해준다.

`ls`란 명령어는 `/bin/ls`에 있음에도 불구하고, 어떠한 위치에서든지 `ls`를 입력하면 작동할 수 있다.
그 이유는 `$PATH`란 변수에 있다.

`echo $PATH`를 통해서 이 변수에 어떤 값이 들어있는지 알 수 있다. 해당 변수에는 파일의 경로가 담겨있고, `:`로 구분되어 있다.

`ls`란 명령어를 실행하면, 컴퓨터는 PATH 값을 확인해서 `ls` 실행파일이 담긴 값을 찾는다. 그리고 있으면 실행시키는 것이다.

PATH 변수는 사용자가 만든 변수가 아닌 유닉스에서 자체적으로 만들어준 변수있다. 이런 변수를 환경변수라고 부른다.

또한 PATH 변수를 수정해서 사용자가 원하는 파일을 실행할 수 있게도 만들 수 있다.
