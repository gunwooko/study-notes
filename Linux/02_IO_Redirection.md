# IO Redirection - Input/Output

예를 들어 `ls -l` 명령어를 통해 출력된 결과를 한 파일로 저장하고 싶다면?
명령어를 이렇게 작성하게 되면 `ls -l > result.txt`: result.txt란 새파일에 ls -l의 결과물(출력=output)을 redirect(`>`) 해준다란 의미이다.
보통 `ls -l` 명령어를 입력하면, 관련된 정보가 모니터로 출력되는 것을 볼 수 있다. 그러나 출력 방향을 변경함으로 redirect 하는 것이다.

유닉스 계열의 운영체제에서 프로그램이 실행되는 프로세스에는 Input과 Output이 있다.
<img src="https://player.slideplayer.com/16/5117573/data/images/img3.jpg" width="470">
Reference: https://slideplayer.com/slide/5117573/

- Unix process: 명령어, 프로그램, 프로세스 ex) `ls` 명령어, `apt-get`, etc
  유닉스 계열의 시스템은 어떤 프로그램이 실행되면 그것을 프로세서라 부른다.
- 프로세스에는 크게 입력과 출력으로 이루어져있다.
- Command-line Arguments: 예를 들어 `ls` 뒤에 옵션으로 들어가는 arg이다. `ls -l`에서 `-l`가 해당한다.

유닉스에서는 프로세서에는 두가지 출력이 존재한다.

- Standard Output(stdout): 예를 들어 `ls -l` 명령어를 입력했을 때 출력되는 결과이다. 보통 모니터로 출력이 된다.
- Standard Error(stderr): 예를 들어 `rm noexistfile.txt`를 실행하면, 에러가 나오게 된다. 이 해당 에러 메세지를 redirection 하고 싶어서 `rm noexistefile.txt > results.txt`를 하게되면 에러가 나타난다. 즉 redirect하지 못했다는 것이다.

  그 이유는 stdout을 redirect 시도를 했다는 의미이다. `>`만 사용했을 때에는 `1>`의 1이 생략되어 있다.
  `1>`은 stdout을 의미하고
  `2>`은 stderr를 의미한다.
  그렇기에 의도한대로 에러 메세지를 redirect하고 싶으면 `rm noexistfile.txt 2> results.txt`를 해야할 것이다.

  두가지 사용하기 위해서 `rm noexistefile.txt 1> results.txt 2> error.log` 이렇게 사용할 수 있다.

Standard Input(stdin): 한가지의 입력만 존재한다.
예를 들어 `cat` 명령어는 인자로 사용자의 키보드 입력을 받을 수 있다. `cat hello`
그리고 해당 `cat` 명령어는 stdinput으로도 입력값을 받을 수 있는데, 들어가는 입력값으로 다른 파일의 출력값을 redirect 해줄 수 있다. `cat < hello.txt`
또한 `cat`이란 명령어의 인자(command-line arg)로 인자를 받아 사용할 수 있다. `cat hello.txt`

other example: `head`
`head -n1 readme.txt`: arg로 인자를 입력
`head -n1 < readme.txt`: stdin으로 인자를 입력
결과는 같다.

응용:
`head -n1 < readme.txt > otherreadme.txt`: readme.txt에 있는 내용을 `head -n1` 명령어에 입력해서 `otherreadme.txt`에 출력하라.

위와 같은 데이터의 흐름을 `IO Stream` 이라고도 부른다.

## IO redirection - append

`>>`를 사용하면 된다.
예) `ls -al >> result.txt` 를 사용하게 되면, 기존의 result.txt의 뒤에 추가가 된다.

`<<`도 있지만 거의 사용되지 않는다.
ex) `mail gunwoo.dev@gmail.com <<anycheck hi hello gunwoo anycheck`

## /dev/null

만일 출력값을 화면에 출력하지도, 다른 파일로 redirect 하고 싶지 않을때에는 `/dev/null`로 보내버리면 된다.
`ls -al > /dev/null`
`/dev/null`은 유닉스 계열에서 휴지통과 같은 곳이다.
