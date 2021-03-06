# General

* git은 파일을 데이터배이스에 저장할 때 까지의 3가지 단계를 가지고 있는데 Modified, Stage, Committed 로 나누어 진다. 수정된 modified 파일은 add 를 통해 stage상태를 넘어 가고 (데이터 베이스로 올려지기 전 상태) Committed를 통해 데이터배이스 저장소에 저장한다.

* Untracked, 관리대상이 아닌 파일들을 지칭하며 `git status` 명령어에도 관련 내용이 나오지 않는다. `git add` 명령어로 Staged상태로 만들 수 있다.

* Tracked, 관리대상인 파일들을 말하며 `git status`명령어를 통해 확인할 수 있다.
  1. Unmodified 상태는 스태이지상태로 되었던 파일이 커밋을 통해서 데이터 베이스로 보내진 후에 따로 수정이 되지 않은 상태를 말한다.
  2. Modified 상태는 Unmodified 나 Staged상태에 있는 상태에서 수정을 할 경우 Modified상태로 된다.
  3. Staged 상태는 커밋을 하기 위해 스냅샷을 저장해 놓은 상태

* Staged상태에서 수정한 후  `git status`에서 파일의 상태를 확인 해 보면 해당 파일이 Staged상태와 Modified상태에 동시에 이름이 올려져 있는 것을 확인할 수 있다. add file을 한 시점에 파일이 Staged에 저장되었기 때문에 발생하는 현상, 따라서 해당 파일을 다시 `git add`명령어를 통해 Staged 상태로 만들어 놓아야 해당 변경사항을 저장 할 수 있다.

* `.gitignore` 파일을 작성하여 로그 파일이나 빌드 시스템이 자동으로 생성한 파일(서버에 올릴 필요가 없는 파일들)을 자동으로 무시할 수 있게 만들 수 있다. www.gitignore.io 곳 에서 무시해야할 파일들을 프로그램이나 OS별로 정리해서  `.gitignore`파일에 작성할 문서를 자동으로 만들어 준다. 유용하게 이용가능

* staged된 파일을 `git commit`명령어로 커밋하면 설정된 에디터 창을 통해 아래와 같은 내용을표시한다.

* 깃에서 내 이름으로 저장소를 만든 후에는 리모트 명령어로 로컬과 연결시켜줘야 한다.

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Your branch is up-to-date with 'origin/master'.
# Changes to be committed:
#	new file:   README
#	modified:   CONTRIBUTING.md
#
~
~
~
".git/COMMIT_EDITMSG" 9L, 283C
```
위의 내용 첫 번째 줄에는 커밋한 파일을 설명할 수 있는 큰 제목 두 번째 줄 부터는 간단한 설명을 남겨놓을 수 있다.

* 너무 일찍 커밋했거나 어떤 파일을 빼먹었을 때 그리고 커밋 메시지를 잘못 적었을 때 `git commit --amend`명령을 실행한다. 한번 되돌리면 복구가 불가능 하다. 이 명령은 Staging Area를 사용하여 커밋한다. 만약 마지막으로 커밋하고 나서 수정한 것이 없다면(커밋하자마자 바로 이 명령을 실행하는 경우)조금 전에 한 커밋과 모든 것이 같다. 이 때는 커밋 메시지만 수정한다. 편집기가 실행되면 이전 커밋 메시지가 자동으로 포함된다. 메시지를 수정하지 않고 그대로 커밋해도 기존의 커밋을 덮어쓴다.

* 리모트 저장소가 여러 개 등록되어 있으면 다른사람이 기여한 내용을 쉽게 가져올 수 있다.

* Merge의 종류에는 2가지가 있다.
1. 상위커밋에 기반하여 새롭게 만들어진 브랜치와의 커밋은 fast-forward 형식으로 Merge된다.

2. 상위커밋과는 다른 바향으로 새롭게 만들어진 브랜치와의 커밋은 3-way-Merge 라고 하며 각 브랜치가 가리키는 커밋 두개와 공통의 조상 하나를 사용하여 Merge한다. 이 경우 단순히 브랜치 포인터를 최신 커밋으로 옮기는 게 아니라 3-way Merge 의 결과를 별도의 커밋으로 만들고 나서 해당 브랜치가 그 커밋을 가리키도록 이동시킨다. 그래서 이런 커밋은 부모가 여러 개고 Merge 커밋이라고 부른다.Git은 Merge 하는데 필요한 최적의 공통 조상을 자동으로 찾는다. 이런 기능도 Git이 다른 버전 관리 시스템보다 나은 점이다.
***

# CLI 명령어

* git add (file name)

파일을 처음 생성하고나면 Untracked 상태인데 Tracked 위의 명령어를 통해 바로 Staged 상태로 만들어 준다. 또한 수정된 파일(Modified상태) 또한 해당 명령어로 Staged상태로 만들어 준다.(참고: staged 상태는 Tracked상태 종류의 3가지 중 하나, 데이타베이스에 커밋 하기전 스냅샷을 만드는 단계)


* git clone [url]

저장소를 클론하는 것, 서버의 있는 데이터를 복제해서 가져온다.


* git status

파일의 상태를 확인하기 위한 명령


* git status -s /or git status --short

파일의 현재 상태를 간단하게 보여준다.


* git diff

파일이 변경되었다는 사실이 아니라 어떤 내용이 변경됐는지 살펴볼 때 사용하는 명령어 / 워킹 디렉토리에 있는 것과 Stage 하지 않을 것을 비교하여 보여줌, 따라서 수정한 모든 파일이 Staging Area에 있다면 아무것도 출력하지 않는다


* git diff --staged

저장소에 커밋한 것과 Staging Area에 있는 것을 비교교하여 보여줌


* git diff --cached

Staged 상태인 파일을 확인한다 `git diff --staged`와 같은 명령어


* git commit

Staged된 파일들을 커밋한다.


* git commit -v

커밋 후에 생성되는 파일 창에 diff 메시지를 추가해서 보여준다.


* git commit -m "text"

커밋과 동시에 파일에 대한 설명을 text자리에 간단하게 추가할 수 있다


* git commit -a

Tracked상태의 파일을 모두 Staging Area에 넣는다.


* git rm 파일명

git에서 파일을 제거 하려면 `git rm` 명령으로 Tracked 상태의 파일을 삭제한 후에 (정확하게는 Staging Area에서 삭제하는 것) 커밋해야 한다.이 명령은 워킹 디렉토리에 있는 파일도 삭제하기 때문에 실제로 파일도 지워진다.
git 명령을 사용하지 않고 단순히 워킹 디렉터리에서 파일을 삭제하고 git status 명령으로 상태를 확인하면 Git은 현재 "Changes not staged for commit"(즉, Unstaged 상태)라고 표시해 준다. 그리고 git rm 파일명 명령을 실행하면 삭제한 파일은 Staged상태가 된다.
커밋하면 파일은 삭제되고 Git은 이 파일을 더 추적하지 않는다.


* git rm --cached 파일명

해당 파일을 Staging Area에서만 제거하고 워킹 디렉토리에 있는 바일은 지우지 않고 남겨둔다.


* git mv 기존파일이름 바꿀파일이름

파일이름을 변경한다.


* git log

커밋 히스토리를 조회하는 명령어, 가장 퇴근의 커밋이 가장 먼저 나온다.


* git log -p -2

`-p`는 각 커밋의 diff 결과를 보여준다. `-2`는 최근 두개의 결과만 보여준다.


* git log --graph

브랜치와 머지 히스토리를 보여주는 아스키 그래프를 출력한다.


* git reset HEAD 파일이름

Staged상태의 파일을 Unstaged상태로 변경한다.

* git checkout --피일이름

Modified(수정되고 커밋되지 않은 상태)상태의 파일을 최근 커밋된 버전으로 다시 되돌리는 명령어


* git remote

현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다. 저장소를 Clone하면 origin이라는 리모트 저장소가 자동으로 등록되기 때문에 origin이라는 이름을 볼 수 있다.


* git remote -v

리모트 저장소에 대한 단축이름과 URL을 함께 볼 수 있다.


* git remote add 저장소이름(보통origin) url

기존 워킹 디렉토리에 새 리모트 저장소를 추가한다.


* git fetch 리모트이름(단축이름)

리모트 저장소에서 데이터를 가져오는 단축키
Clone한 이후에(혹은 마지막으로 가져온 이후에) 수정된 모든 것을 가져온다. git fetch명령은 리모트 저장소의 데이터를 모두 로컬로 가져오지만, 자동으로 Merge하지 않는다.


* git pull 리모트이름
Clone 한 서버에서 데이터를 가져오고 그 데이터를 자동으로 현재 작업하는 코드와 Merge시킨다.


* git push 리모트저장소이름 브랜치이름
```
git push origin master
```
master 브랜치를 origin서버에 Push한다. / 이 명령은 Clone 한 리모트 저장소에 쓰기 권한이 있고, Clone 하고 난 이후 아무도 Upstream 저장소에 Push 하지 않았을 때만 사용할 수 있다. 다시 말해서 Clone 한 사람이 여러 명 있을 때, 다른 사람이 Push 한 후에 Push 하려고 하면 Push 할 수 없다. 먼저 다른 사람이 작업한 것을 가져와서 Merge 한 후에 Push 할 수 있다.


* git remote show 리모트저장소이름

리모트 저장소의 구체적인 정보를 확인할 수 있다.


* git remote rename 기존이름 바꿀이름

리모트 저장소의 이름을 변경한다.


* git remote remove 이름 또는 git remote rm 이름

리모트 저장소를 삭제한다.


* git tag

이미 만들어진 태그가 있는지 확인한다.


* git tag -a 태그이름 -m "메시지"

Annotated태그를 만든다. /Lightweight 태그는 브랜치와 비슷한데 브랜치처럼 가리키는 지점을 최신 커밋으로 이동시키지 않는다. 단순히 특정 커밋에 대한 포인터일 뿐이다. Annotated 태그는 Git 데이터베이스에 태그를 만든 사람의 이름, 이메일과 태그를 만든 날짜, 그리고 태그 메시지도 저장한다. GPG(GNU Privacy Guard)로 서명할 수도 있다. 일반적으로 Annotated 태그를 만들어 이 모든 정보를 사용할 수 있도록 하는 것이 좋다. 하지만 임시로 생성하는 태그거나 이러한 정보를 유지할 필요가 없는 경우에는 Lightweight 태그를 사용할 수도 있다.
-m 옵션을 통해서 메시지를 함께 저장할 수 있다. 명령을 실행할 때 메시지를 입력하지 않으면 git은 편집기를 실행시킨다.


* git tag 태그이름
Lightweight 태그는 기본적으로 파일에 커밋 체크섬을 저장하는 것뿐이다. 다른 정보는 저장하지 않는다. Lightweight 태그를 만들 때는 -a, -s, -m 옵션을 사용하지 않는다.


* git tag -a 태그명 이전커밋히스토리의커밋체크섬

예전에 커밋한 파일에 태그를 한다. `git log`를 통해 커밋 히스토리를 확인하고 커밋 고유번호인 체크섬ㅁ을 몇자리면 명기하여 어떤 커밋인지를 나타내 준다.


* git push 저장소이름 태그이름

git push 명령은 자동으로 리모트 서버에 태그를 전송하지 않는다. 태그를 만들었으면 서버에 별도로 Push 해야 한다.


* git branch 브랜치이름

새로운 브랜치를 만든다.


* git branch -d 브랜치이름

해당 브랜치를 삭제한다


* git checout 브랜치이름

해당 브랜치 이름으로 헤드를 이동시킨다. 헤드를 이동시키면 해당 해드는 해당 브랜치가 있는 커밋을 가리키고 워킹디렉토리의 파이도 그 시점으로 되돌려 놓는다. 이렇게 헤드를 옮길 경우 다른 브랜치의 작업들과는 별개로 진행된다.


* git checkout -b 새로운브랜치이름

브랜치를 만들면서 Checkout까지 한 번에 하려면 git checkout 명령에 `-b`라는 옵션을 추가한다.


* git ls-tree --full-tree -r HEAD

Tracked 된 로컬 파일 전체를 확인할 수 있다.
