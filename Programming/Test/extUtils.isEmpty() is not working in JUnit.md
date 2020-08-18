# TextUtils.isEmpty() is not working in JUnit 

## Cause
TextUtils.isEmpty() always return false 

## Solution
```kotlin
//Use PowerMock
@RunWith(PowerMockRunner::class)
@PrepareForTest(TextUtils::class)
class MyTest {
    
    @Before
    fun setUp() {
        PowerMockito.mockStatic(TextUtils::class.java)
        `when`(TextUtils.isEmpty(any(CharSequence::class.java)))
            .thenAnswer(object : Answer<Boolean> {
                override fun answer(invocation: InvocationOnMock?): Boolean {
                    if (invocation == null || invocation.arguments[0] !is CharSequence) {
                        throw Exception("is not CharSequence")
                    }

                    val string = invocation.arguments[0] as CharSequence?
                    return string.isNullOrEmpty()
                }
            })
    }
}
```
