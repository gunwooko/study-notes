# Group - 파일과 디렉토리를 여러 사용자들이 공동으로 관리할 수 있는 방법

한 컴퓨터에는 다양한 유저가 사용할 수 있다.(리눅스-유닉스에서는) 이런 경우 한 특정 사람들에게 권한을 주고 싶을 때가 있다. 예를 들면 디자인어, 개발자, 어드민 등등.
이런 상황에서는 개발자인 유저들을 그룹핑하고 디자인어 유저들을 그룹핑해서 해당 그룹에 권한을 부여함으로 해결할 수 있다.

## groupadd

- `groupadd developer`: create a new group 새로운 그룹추가 (예제는: developer라는 이름을 가진 group을 생성하라)

그리고 새롭게 생성된 그룹은 유닉스의 모든 그룹정보가 저장되는 `/etc/group`에 저장됨을 확인할 수 있다.

## usermod

- `usermod -a -G developer USER_NAME`: 해당 유저네임을 자긴 유저를 developer 그룹에 추가하라

이후 유저를 exit하고 다시 접속하게되면 변경됨을 확인할 수 있다.

## chown (change owner and group)

`chown OWNER_NAME:GROUP_NAME DIR_NAME`

- `chown gunwoo:developer .`: 현재 디랙토리의 오너를 건우로 그리고 그룹은 developer로 변경하라
