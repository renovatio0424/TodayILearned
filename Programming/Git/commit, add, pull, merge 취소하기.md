# 2020/03/04

## Git commit, add, pull, merge 취소하기 [(reference)](https://anster.tistory.com/162)

### cancel merge, commit 

* ORIG_HEAD : reset 을 이용해 HEAD를 변경하고 나면, 이전의 HEAD는 .git/ORIG_HEAD 라는 이름으로 저장됨


~~~
$ git reset --hard ORIG_HEAD
$ git reset --merge ORIG_HEAD
~~~
