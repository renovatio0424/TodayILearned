## [Git] Cherry-Pick   [(reference)](https://imasoftwareengineer.tistory.com/7)
: 다른 브랜치에 있는 특정 커밋들을 현재 브랜치에 머지하고 싶은 경우 사용

example
~~~
git checkout cherry-pick-branch
git cherry-pick 76ae30ef //commit number
~~~

### Conflict 발생시 option
    1. continue : conflict 발생시 conflict 를 resolve 처리후 cherry-pick 진행
    2. abort : cherry-pick 취소 
