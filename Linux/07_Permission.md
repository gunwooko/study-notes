# Permission 권한

User가 File & Directory 에 대해서 Read, Write, Excute 할 수 있도록 혹은 할 수 없도록 제어하는 것.

- `ls -l example.txt`: 파일 상세정보 확인하기 => 권한과 누가 소유한 파일인지 확인할 수 있다.
- `echo 'hello' > example.txt`: hello 문자를 example.txt에 리다이렉션으로 출력하기.
  위와 같은 상황에서 소유자라면 가능할 것이다.
  그러나 만일 소유자가 아니라면, `Permission denied`가 나올 것이다.
