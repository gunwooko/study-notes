# Permission 권한

User가 File & Directory 에 대해서 Read, Write, Excute 할 수 있도록 혹은 할 수 없도록 제어하는 것.

- `ls -l example.txt`: 파일 상세정보 확인하기 => 권한과 누가 소유한 파일인지 확인할 수 있다.
- `echo 'hello' > example.txt`: hello 문자를 example.txt에 리다이렉션으로 출력하기.
  위와 같은 상황에서 소유자라면 가능할 것이다.
  그러나 만일 소유자가 아니라면, `Permission denied`가 나올 것이다.

`-rw-r--r-- 1 gunwoo staff 0 Jan 5 22:59 perm.txt`

위를 나눠보면 이렇게 나눌 수 있다:  
`-|rw-|r--|r-- |1| gunwoo staff |0| Jan 5 22:59 |perm.txt|`

- `-`: type을 나타낸다. - 는 파일이란 뜻, d는 디렉토리를 나타낸다.
- `rw-|r--|r--`: Access mode로 첫번째는 Owner의 권한, 두번째는 Group의 권한, 세번째는 Others의 권한을 나타낸다.
  - r: read 읽고
  - w: write 쓰고
  - x: execute 실행한다.
- `gunwoo staff`: 첫번째는 Owner를 나타내고, 두번째는 Group을 나타낸다.

## 권한 변경 - chmod (change mode)

`chmod o-r perm.txt`: 다른 사용자에게 읽기 권한을 빼라
`chmod o+r perm.txt`: 다른 사용자에게 읽기 권한을 주어라
`chmod o+w perm.txt`: 다른 사용자에게 쓰기 권한을 주어라
`chmod u-r perm.txt`: 소유자에게 읽기 권한을 빼라

## 실행 그리고 권한 설정 (execute)

다음 결과는 `hi-machine.sh` 파일을 실행했을 때이다:
`zsh: permission denied: ./hi-machine.sh`

그러나 `/bin/zsh hi-machine.sh`를 했을 경우 결과를 볼 수 있는데, 이것은 /bin/zsh 라는 특정 명령어로 파일을 실행 시켰기 때문이다.

`chmod u+x hi-machine.sh` 명령어를 통해 실행 권한을 부여시킬 수 있다.:

변경후: `-rwxr--r-- 1 gunwoo staff 32 Jan 5 23:19 hi-machine.sh`

## 디렉토리의 권한

- 디렉토리에서의 read 권한은 해당 디렉토리를 열람할 수 있느냐 없느냐이다.
- 디렉토리에서의 write 권한은 해당 디렉토리 안에서 파일을 생성할 수 있냐 없냐, 그리고 안에 있는 파일을 삭제할 수 있냐 없냐에 있다. 또한 파일의 이름을 변경, 이동또한 관련이 있다. (파일 생성, 삭제, 수정)
- 디렉토리에서의 execute 권한은 `cd` 명령어로 해당 디렉토리에 들어갈 수 있느냐 없냐이다.

만일 권한을 수정하고픈 디렉토리 안에 또 다른 디레토리가 있다고 가정했을때, 안에 있는 모든 디렉토리의 권한을 수정하고 싶을때는 `chmod -R o+w perm` 명령에서 볼 수 있듯, `-R` recursive 옵션(재귀적으로)을 주어서 할 수 있다.

## chmod with octal

- Octal modes

| #   |       Permission        | rwx |
| :-- | :---------------------: | --: |
| 7   | read, write and execute | rwx |
| 6   |     read and write      | rw- |
| 5   |    read and execute     | r-x |
| 4   |        read only        | r-- |
| 3   |    write and execute    | -wx |
| 2   |       write only        | -w- |
| 1   |      execute only       | --x |
| 0   |          none           | --- |

`chmod 444 perm.txt`: 모든 사람들(owner, group, others)에게 read only이 권한을 부여한다.

## chmod: Class & Operation

| Reference |  Class |
| :-------- | -----: |
| u         |  owner |
| g         |  group |
| o         | others |
| a         |    all |

| Operator |                                                                  Description |
| :------- | ---------------------------------------------------------------------------: |
| +        |                                                                          add |
| -        |                                                                       remove |
| =        | the modes specified are to be made the exact modes for the specified classes |

- `chmod a= perm.txt`: 모든 사용자에게 모든 권한 없애기
- `chmod o=r perm.txt`: others 클래스의 사용자에게 read 권한 주기
- `chmod a=rwx perm.txt`: 모든 사용자에게 모든 권한 주기
