# 2020/02/24

## 안드로이드 현재 키보드 visibility 상태 여부 체크 [reference](https://twitter.com/chrisbanes/status/1230598177511788545?s=20)

~~~kotlin
val imeInsets = view.rootWindowInsets.getInsets(Type.ime())

if(imeInsets.isVisible) {
  //IME is currently visible ...
  //Lets move our view by the height of the IME
  view.translationX = imeInsets.bottom
}
~~~

