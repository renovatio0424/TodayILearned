# 2020/05/14

## also (Kotlin)

~~~kotlin
val person: Person = getPerson().also {
    print(it.name)
    print(it.age)
}
~~~
