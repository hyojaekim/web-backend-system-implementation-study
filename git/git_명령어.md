# Git 명령어

### 이전 명령어를 취소하고 싶은 경우
* git reflog (명령어 history 확인)
  * 돌아가고 싶은 HEAD@{n} 확인
* git reset --hard HEAD@{n}

### 과거 특정 커밋을 수정하고 싶은 경우
* git log 수정할 커밋 확인
* git rebase --interactive
  ```
  pick ~~~ 커밋(4)
  pick ~~~ 커밋(3)
  ...
* git rebase --interactive HEAD~n
* 원하는 커밋 내용 수정
* git add . & git commit --amend
* git rebase --continue
* git push
  * 이렇게 하면 거절됨
  * git push --force
  * 조금이라도 더 안전하게 작업하려면, 덮어쓰기 전에 로컬의 remotes/브랜치A가 참조하고 있는 것과 현재 원격의 브랜치A가 참조하고 있는 내용이 동일할 경우에만, 즉, 다른 누군가가 원격의 브랜치A에 push를 하지 않은 상태에서만 git push --force를 실행하는 git push --force-with-lease를 실행할 수도 있다.
* [참고자료](https://homoefficio.github.io/2017/04/16/Git-%EA%B3%BC%EA%B1%B0%EC%9D%98-%ED%8A%B9%EC%A0%95-%EC%BB%A4%EB%B0%8B-%EC%88%98%EC%A0%95%ED%95%98%EA%B8%B0/)

### 커밋 메시지 수정

* 방법 1
  * git rebase -i HEAD~3
  * 변경하고자 하는 커밋에 pick -> edit
  * git commit --amend
  * git rebase --continue
  * git push -f
* 방법 2
  * git commit --amend -m "test"
  * git push -f
