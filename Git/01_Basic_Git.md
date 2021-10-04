# Git

Git은 버전 관리시스템(Version Control System)으로 파일 변화를 시간에 따라 기록했다가 이후에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템이다.

> Git이란 소스코드를 효과적으로 관리하기 위해 개발된 '분산형 버전 관리 시스템'이다. 원래는 Linux 소스코드를 관리할 목적으로 개발되었다. Git에서는 소스 코드가 변경된 이력을 쉽게 확인할 수 있고, 특정 시점에 저장된 버전과 비교하거나 특정 시점으로 되돌아갈 수도 있습니다.

# GitHub

Git을 사용하는 사람들이 모여 협업을 할 수 있도록 있게 한 유용한 플렛폼이다. 개발하고 다른 개발자들과 오픈소스를 공유하고 협업할 수 있게 해준다.

간략하게 깃과 깃허브를 사용해 협업이 어떻게 이뤄지는지 말하자면, 깃허브에 Remote repository가 있고, 이곳에 Original repository와 My repository가 있다.
메인테이너의 Original repo에서 My repo로 가지고 오는 작업을 `fork`한다고 한다. 그리고서 Remote repo의 My repo에 저장된 코드를 내 노트북 즉, Local repository로 가져와 작업할 수 있게 하는 것을 `clone`이라고 한다.
내 로컬노트북에서 무언가를 수정하고 다시 Remote repo로 적용을 시키려면 `git push`라는 명령어를 사용하는데, 이렇게 해주면 나의 Local repo의 변경 사항이 My repo의 remote repo에도 똑같이 적용된다. Ex) `$ git push origin master` _(git push = 명령어, origin = 보내는 대상, master = 브렌치 이름 / Local repo에서 My repo는 origin이다.)_
여기서 만약 협업 중에 누군가 Remote repo의 My repo를 수정해서, Local repo로 가져오고(적용하고) 싶으면 `git pull`명령어를 사용하면 된다. 이 명령은 파일을 병합시킨다. Ex) `$ git pull origin master` _(git push = 명령어, origin = 가져오는 대상, master = 브렌치 이름)_
만약에 Original repo의 메인테이너가 변경을 했을 때 나의 Local repo로 가져오고 싶으면 `$ git pull upstream master`를 사용하는데 upstream은 Local repo에서 봤을 때 원본 repo를 upstream이라고 한다. (\*단, upstream repo를 등록해줘야 한다. git remote add upstream <URL>)

![](https://images.velog.io/images/gunwooko/post/cc5c8a26-02e4-4fff-8baf-dbcd8483f54c/github.png)

# Git Workflow

![](https://images.velog.io/images/gunwooko/post/5c8db753-db36-4a40-891c-75c7a91b94e1/IMG-6965.jpg)

Repository는 기록-작업 흐름을 모두 포함한 개념이다.
![](https://images.velog.io/images/gunwooko/post/c18e5c90-af4e-4b51-9b24-d5453efa2402/IMG-6966.jpg)
위에서 보면 동그라미 부분이 commit을 한 부분이다. 그리고 commit된 부분에서 또 다른 가지가 내려오는 것을 branching 한다고 하고, 나눠진 가지가 다시 위로 올라가 합쳐지는 것을 merging이라고 부른다. Repository는 여러 단계로 나뉘어 있는데 크게 나누면 master branch, develop branch 그리고 feature branch로 나뉜다. master branch는 엔드유저 즉, 사용자에게 직접 배포되는 소스가 담겨 있고, develop branch에는 말 그대로 개발과정 중의 소스가 담겨 있는데, 이곳에서 충분한 테스트가 이뤄지고 새롭게 feature branch에서 기능들이 추가되어 merging되면 또 다른 버그나 다른 문제점들이 생기는지 테스트를 한다.

# CLI (Command-line interface)

터미널이라고도 알려져 있는데 사용하는데 유용한 다양한 명령어가 있다.

- `ls` 디렉토리 확인하기 / `ls -al` 자세히 확인하기
- `cd` 디렉토리 들어가기 / `cd ..` 나가기
- `mkdir` 디렉토리 만들기
- `rm` 삭제 (주의해서 사용해야한다)
- `pwd` 현재 디렉토리 확인
- `touch` 파일 만들기
- `~` 홈 디렉토리
- `/` 루트 디렉토리
- `clear` 터미널 화면 깨끗이 하기
- `sudo` 관리자 권한으로 실행 (주의해서 사용해야한다)
- `chown` change owner 즉 파일, 또는 폴더의 소유권을 변경하는 명령어

- `git help` 다양한 명령어를 설명과 함께 나열해준다.
- `git init` `.git` 파일은 git을 추적하는 파일인데 해당 디렉토리가 없으면 git을 add 할 수 없다. 그렇기에 `git init` 명령어를 사용해 `.git` 디렉토리를 만들 수 있다. `git init`을 하게되면 그 명령을 하는 저장소가 현재 디렉토리가 되고, 이 말은 그곳이 Local repo가 된다는 말이다.
- `git status` git의 현재 상태를 확인할 수 있다.
- `git log` commit된 기록을 볼 수 있다.
- `git add` staging area에 파일을 올려준다. 이 과정을 반드시 거쳐야 commit이 가능하다. `$ git add 파일명` / Tip: `$ git add .` 모든 파일 추가해준다.
- `git commit` staging area에 추가된 파일들의 snapshot을 하나하나 만들어준다. `$ git commit -m "커밋 메세지"`. 커밋 메세지를 잘 써줘야 작업기록을 추적하는 데 유리하다.
- `git push` Local repo에 있는 커밋된 파일들을 remote repo로 보내준다.
- `git remote -v` 원격 저장소에 연결되어 있는 주소가 나온다. (해당 디렉토리에서 실행해야 한다.)
- `git checkout branchName` 브랜치 선택하기
- `git checkout -t remotePath/branchName` 원격 브랜치 선택하기
- `git branch branchName` 브랜치 생성하기
- `git branch -r` 원격 브랜치 목록보기
- `git branch -a` 로컬 브랜치 목록보기
- `git branch -m branchName changeBranchName` 브랜치 이름 바꾸기
- `git stash` [git stash 명령어 사용하기](https://gmlwjd9405.github.io/2018/05/18/git-stash.html) 아직 마무리하지 않은 작업을 스택에 잠시 저장할 수 있도록 하는 명령어 [Stash 기능 소개](https://wit.nts-corp.com/2014/03/25/1153)
- `git branch -d <branchname>` 브랜치 삭제하기

# Git Workflow

간략한 git workflow는 다음과 같다.

1. 깃허브의 repository에서 나의 repository로 `fork`한다.
2. 나의 repository에서 나의 local로 가져오기 위해 `clone` 한다.
   `$ git clone <Repo URL>`
3. 동료와 공동작업을 위해 나의 local과 상대방의 repository와 연결한다.
   `$ git remote add pair <Repo URL for pairs fork>`
4. 그리고서 코드를 작성한 후 local에 커밋해준다.
   `$ git add <change file>`
   `$ git commit -m "commit message"`
5. 그다음에 나의 remote repository (origin)에 푸쉬해준다.
   `$ git push origin master (or other branch name)`
6. 이 상태에서 나의 동료는 `pull` 명령어를 사용해 변경된 내용을 자신의 local로 가져올 수 있다.
   `$ git pull pair master (or other branch name)`
7. 이 순서를 계속해서 반복해서 작업한다.

## Git branch

여러 개의 branch를 만들 수 있는데, 각각의 branch는 서로 독립되어 영향을 주지 않는다. 이것이 필요한 이유는 여러 명의 개발자가 동시에 협업하는 과정에서 일어날 수 있는 실수와 동선의 겹침을 막아주고 정상적으로 작업할 수 있도록, 각자의 작업 공간을 만들어 주는 것이다. 그렇기에 각자가 맡은 파트 혹은 기능을, branch를 만들어 독립적으로 개발하고서 합칠 수 있는 것이다. 또한 branch가 유용한 이유는 원본에 영향을 끼치지 않기에 여러 가지 테스트도 해볼 수 있다.
Branch는 항상 현재 작업 공간을 베이스로 만들어진다. 그렇기에 내가 어떤 branch에 있는지 먼저 확인할 필요가 있고, 또한 branch를 옮기는 (작업 공간을 옮기는) 방법도 알아야 한다.

### Git checkout <브랜치 이름>

`$ git checkout <브랜치 이름>`과 같은 명령어로 이동할 수 있다. 만일 현재 위치가 원본이라고 하면, 위의 명령어로 인해 작업 공간이 브랜치 이름으로 옮겨가게 된다.

### Git checkout -b <새로 만들 브랜치 이름>

`$ git checkout -b <새로 만들 브랜치 이름>` 명령어로 새로운 branch를 만들고 해당 branch로 이동하게 된다. 위의 명령어는 만들고 이동하는 두 가지가 합쳐져 있다.

## Project git workflow

아래와 같은 과정을 (1~5번) 계속해서 반복해준다.
![](https://images.velog.io/images/gunwooko/post/16669646-492c-4020-bfc1-87162564b398/Project%20Git%20Workflow.jpg)

# 참고

- [Git 튜토리얼 - Branch 만들기](https://backlog.com/git-tutorial/kr/stepup/stepup2_2.html)
- [Git을 이용한 버전 관리](https://backlog.com/git-tutorial/kr/intro/intro1_1.html)
- [Git Reset에 관하여](https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-Reset-%EB%AA%85%ED%99%95%ED%9E%88-%EC%95%8C%EA%B3%A0-%EA%B0%80%EA%B8%B0)
- [Git 되돌리기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EB%90%98%EB%8F%8C%EB%A6%AC%EA%B8%B0)
- [Git 수정, 저장하기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)
- [Git에 관하여](https://git-scm.com/book/ko/v2)
- [Git 정리](https://dimdim.tistory.com/entry/GIT%EC%97%90-%EB%8C%80%ED%95%9C-%EB%82%B4%EC%9A%A9%EC%A0%95%EB%A6%AC-%EC%A0%95%EB%A6%AC%EC%A4%91)
- [깃허브 설명](https://nolboo.kim/blog/2013/10/06/github-for-beginner/)
- [git/gui란? git/gui 툴 소개](https://dora-guide.com/git-gui-client/)
