# 2020:02:10

## [Git] 이미 remote repository 에 push 해버린 commit 들 합치기 (Squash)
[reference](https://json.postype.com/post/209499)

[reference2](https://github.com/wprig/wprig/wiki/How-to-squash-commits)
1. 합칠 브랜치로 이동한다. 
2. rebase 를 한다.
~~~ git
//git local repository
$ git rebase -i HEAD~2 // HEAD~2는 HEAD로 부터 2개의 commit 을 의미한다. 
~~~
3. 합칠 commit 의 pick 을 squash 로 바꾼다. 
4. commit message 를 수정한다. 
5. push 한다.
~~~ git
//git local repository
$ git push --force-with-lease origin
~~~
