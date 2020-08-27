`git checkout origin/master`

원격 저장소에 체크아웃 후 commit 하면 HEAD가 분리되어 커밋됨

![Untitled](https://user-images.githubusercontent.com/69679325/91434711-32a05080-e8a0-11ea-8a4c-9549b8db0f9c.png)


`git fetch` 는 원격 저장소 상태를 로컬 저장소에 반영함. 원격 저장소 브랜치들 위치도 반영된다.

- 원격 저장소에는 있지만 로컬에는 없는 커밋들을 다운로드 받습니다. 그리고...
- 우리의 원격 브랜치가 가리키는곳을 업데이트합니다 (예를들어, `o/master`)
- 필요한 데이터를 다운로드는 하지만, 실제로 로컬 파일들이나 브랜치를 변경하지는 않습니다.

`git pull` = `git fetch; git merge origin/<branch>`

`git pull —-rebase` = `git fetch; git rebase origin/<branch>`

checkout 없이 rebase

`git rebase <branch1> <branch2>`

rebase 

장점:

- rebase는 여러분의 커밋 트리를 깔끔하게 정리해서 보기가 좋습니다 모든게 한 줄에 있기때문이죠.

단점:

- rebase를 하게 되면 커밋 트리의 (보이는)히스토리를 수정합니다.

원격 브랜치를 추적

`git checkout -b foo o/master`

`git branch -u o/master foo`

만약 `foo`가 현재 작업하고 있는 브랜치라면 생략해도 됩니다:

`git branch -u o/master`

다른 브랜치에 있어도 push 가능

`git push <remote> <place>` 

`git push origin master`

특정 브랜치를 다른 원격 브랜치에 push

`git push origin <source>:<destination>`

fetch는 push와 반대 개념일 뿐 비슷하게 작동한다. 위 push 처럼 특정 저장소와 브랜치를 지정해줄 수 있다.

지정하지 않으면 모든 브랜치를 fetch한다.

`git push origin :<destination>`

source 부분이 비어있으면 원격 브랜치 삭제

`git fetch origin :<destination>`

source 부분이 비어있으면 새 브랜치 만듬

같은 원리로 pull도 인자를 줘서 사용 가능