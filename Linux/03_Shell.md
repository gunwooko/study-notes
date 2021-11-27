# Shell vs Kernel

 <img src="https://srinisbookcom.files.wordpress.com/2020/11/bb6fa-kernel_shell.jpg" width="370">
 
 References: https://srinisbook.com/linux-tutorial/introduction/

Hardware: 물리적 기계, cpu, memory, ssd, gpu, etc
Kernel: 하드웨어를 직접적으로 제어하는 운영체제에서 가장 중심이 되는 코어다.  
Shell: 사용자가 입력한 명령을 해석해서 kernel이 이해할 수 있도록 해주는 프로그램.

인간이 커널을 직접적으로 다루기는 어렵기 때문에 인간이 이해할 수 있는 명령어를 받아서 커널에게 해석해주는 역활을 하는 것이 쉘이다.
쉘에는 다양한 종류가 있고 자신에게 맞는 혹은 상황에 맞는 쉘을 사용할 수 있다.

# Shell

내가 사용하는 쉘이 어떤것인지 확인하는 방법은: `echo $0` 명령어를 통해 알 수 있다.

## bash vs zsh

이 둘은 상당히 유사하다. zsh은 bash가 없는 추가적인 기능이 있어 조금더 편리하다는 평가를 받고 있다.

- bash에서는 `cd` 명령어와 tab을 치게되면 숨겨진파일(.)도 보여주지만, zsh은 숨겨진 파일은 나오지 않게 해준다.
- zsh는 사용자의 명령어 편의성을 위해 `cd` 절대경로에서 절대경로의 앞글자만 입력해도 tab을 누르면 자동완성해준다.
- `/bin`: 유닉스 계열의 기본 프로그램들이 설치저장되어 있는 폴더이다. => bash, zsh, ls, mkdir 등등이 있다.

# Shell Script

Shell script 사용하기: (bash)

```
#!/bin/bash                => 현재 이 스크립트는 bin 디랙토리의 bash 프로그램을 사용한다는 말이다. 첫번째 줄은 약속이다.
if ! [ -d bak ]; then      => bak이란 디랙토리가 존재하지 않는다면,
        mkdir bak          => bak이란 디랙토리를 생성하라.
fi                         => if문을 거꾸로 적어서 if문이 끝남을 알려준다.
cp *.log bak               => 여기서부턴 bak이란 디텍토리가 있다는 것을 확신할 수있다. 그리고 다음 명령으로 `.log`로 끝나는 파일을 bak으로 복사해줘라.

```
