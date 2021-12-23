# 컴퓨터 구조 기본

Storage: 프로그램이<예: 명령어(command)> 저장되어 있는 곳.
Memory: 프로그램이 실행되기 전에 옮겨지는 곳. Storage가 빠른 CPU를 따라가지 못하기 때문이다.
Processor: 프로그램을 처리한다.
Process: 실행되고 있는 상태에 있는 프로그램을 프로세스라 부른다.

# 프로세스 모니터링

`ps`: 프로세스 보여줘라
`ps aux`: 자세히 보여줘라
`ps aux | grep apache`: 해당 프로세스를 보여준다.
`kill PID번호`: 해당 프로세스를 킬한다.
`sudo top`: ps 보다 조금더 실용적인 프로그램. 프로세스 각 항목을 보여준다.
`sudo htop`: 시각적으로 조금더 보기 화려하다.

## 프로세스 항목:

- Command: 어떤 명령어로 실행되고 있는지 보여준다.
- RES: 실직적인 메모리 사용량
- CPU: 처리 사용 퍼센티지
- MEM: 메모리 사용 퍼센티지
- Load average: CPU 프로세서의 점유률 => 1분, 5분 15분간의 CPU가 얼마나 바쁜지의 평균치를 보여준다.
  - 1분에는 순간적인 점유율을 보여준다.

# Background 실행

예를 들어 vi로 파일을 편집후 ctrl + z를 누르면 foreground에서 background로 넘어가게 된다.
이후 `fg` 명령어로 background로 넘어간 프로그램을 바로 foreground로 변경할 수있다.
프로그램은 스택 형식으로 backgroundp에 계속 쌓일 수 있다.
특정 프로그램을 선택해서 열고 싶으면, `fg %숫자`를 통해 열 수 있다.
`jobs` 명령어를 통해 현재 background에 있는 프로그램을 볼 수 있다.
`kill %숫자`:
`kill -9 %숫자`: 해당 스택의 프로그램을 삭제한다.

TIP

- 종종 설치 혹은 빌드를 실행할때, 시간이 오래 걸리는 경우가 있다. 이럴때 명령어 뒤에 &를 붙여주면 백그라운드에서 명령어가 실행되고, 끝나게되면 Exit하게된다.
  예시: `ls -alR / > result.txt 2> error.log &`

# Daemon 혹은 Service

데몬이라 불리는 프로그램들은 항상실행된다는 특징이 있다.
ls, mkdir, rm 과 같은 프로그램은 원할때 키고 한순간 작동이후 끝난다.
그러나 웹서버와 같은 컴퓨터는 항상 켜져 있어야 한다.

## Service와 자동실행

`/etc/init.d/`에는 데몬프로그램들이 저장되어 있다.
여기에 저장되어 있는 프로그램을 키고 끌때는 `service`란 명령어를 사용한다.
`sudo service apache2 start`: apache2가 실행된다.
`sudo service apache2 stop`: 실행되지 않는다.
`ps aux | grep apache2`: 현재 실행되는 프로그램을 확인해볼 수 있다.

etc/ 에는 rc3.d(콘솔) 혹은 rc5.d(GUI형식) 라는 디렉토리가 있는데, 이곳에는 실행될때 자동으로 바로 실행되는 프로그램을 확인할 수 있다.
해당 프로그램 이름 앞에 S는 시작을 의미하고, K는 중단을 의미한다.
자동으로 프로그램을 실행하고 싶다면, 각각 해당 디렉토리에 링크를 걸어주면 된다. 또한 S혹은K뒤에 숫자가 나오는데 이것은 실행 우선순위를 나타낸다.

# Cron

정기적으로 프로그램을 실행해야 할때가 있다. 시간을 정기적으로 조정한다던지, 혹은 파일을 보내야한다던지가 있다. Cron을 사용해서 정기적으로 프로그램을 작동시킬 수 있다.

`crontab -e` 명령어로 정의할 수 있다. (keyword: crontab expression)
아래 순서로 같이 정의할 수 있다.
`m h dom mon dow command`
분 시간 일 월 요일 명령어

`*`로 처리하면 상관하지 않는 다는 것이다.

예시: `*/1 * * * * date >> date.log 2>&1`
확인은 `tail -f date.log`로 해볼 수 있다.

# Shell start up script

`alias l='ls -al'`: l은 ls -al의 별명으로 만들어라.

`echo $SHELL` 명령어를 통해 현재 사용하는 쉘이 저장된 장소를 찾아볼 수 있다.
보통 /bin/bash 아니면 /bin/zsh 이다.
`.bashrc` 혹은 `.zshrc`의 파일에 쉘를 수정해줄 수 있다.
nano 혹은 vi로 들어가서 수정한다. 즉 여러 명령어를 적어준다.
그러면 쉘이 시작될때 실행된다.
