## [Kotlin] 코틀린 constructor, init block 호출 순서

~~~kotlin
class Person(private val name: String) { //primary constructor
    private var age: Int = 0
    set(value) {
        println("property called")
        field = value
    }
    private lateinit var address: String
    private lateinit var company: String

    constructor (name: String, age: Int, address: String) : this(name) { //secondary constructor
        println("constructor 1 called")
        this.age = age
        this.address = address
    }

    constructor (name: String, age: Int, address: String, company: String) : this(name) { //secondary constructor
        println("constructor 2 called")
        this.age = age
        this.address = address
        this.company = company
    }

    init {
        println("init called")
        if (!::address.isInitialized)
            this.address = "unknown address"
        if (!::company.isInitialized)
            this.company = "unknown company"

    }
}

/**
 * result
 * 
 * init called
 * constructor 2 called
 * age called
 * */
~~~