## Learn git branching main 간단 정리
---
https://learngitbranching.js.org/?locale=ko

커밋은 스냅샷을 저장

스냅샷은 이동 빠르지만 크기가 큼. 델타는 크기는 작지만 이동할 때 느림.

모든 경우 스냅샷은 아님. delta로 저장하는 것이 효율적일 땐 delta로 저장함

특정 시점에 garbage collection 하여 delta로 변환함. 모든 것을 변환하지는 않음. 오래 된 커밋으로 이동하는 경우가 흔치 않으므로.

브랜치는 참조일 뿐이라 가볍다. `브랜치를 서둘러서, 그리고 자주 만드세요`

깃 상대 참조 

`git checkout HEAD^` 하나 위 커밋으로 체크아웃

`git checkout HEAD~4` 4개 위 커밋으로 체크아웃

`git branch -f bugFix HEAD^` HEAD 위의 커밋으로 bugFix브랜치를 체크아웃

`git reset <commit>` : 해당 커밋으로 되돌아감, 커밋 삭제

`git revert <commit>` : 해당 커밋으로 돌아가기 위해 반대되는 커밋들을 추가함

`git cherry-pick <commit> <commit> ..<commit>` : 필요한 커밋들만 복사해서 현재 브랜치 아래로 순서대로 추가함

`git rebase -i <commit>` : 인터랙티브 리베이스, 원하는 것 pick, 순서 재배열 가능 실제 git에선 vim같은 편집기가 열린다.

`git tag <tag_name> <commit>` : 이정표를 만든다. 브랜치와 다르게 이동 불가

`git describe [<commit>]` : 부모노드중 가장 가까운 태그 출력, 커밋 지정안하면 HEAD