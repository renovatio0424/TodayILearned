# 2020/04/22 

## Lateinit Issue [(reference)](https://kotlinlang.org/docs/reference/whatsnew12.html#checking-whether-a-lateinit-var-is-initialized)

~~~kotlin
println("isInitialized before assignment: " + this::lateinitVar.isInitialized)
lateinitVar = "value"
println("isInitialized after assignment: " + this::lateinitVar.isInitialized)

/*** result
* isInitialized before assignment: false
* isInitialized after assignment: true
*/
~~~
