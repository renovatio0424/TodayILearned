# 2020:02:10

## How to put an Enum in Bundle
[reference](https://stackoverflow.com/questions/3293020/android-how-to-put-an-enum-in-a-bundle)

~~~java
enum YourEnum {
  Type1,
  Type2
}

// Bundle
// put
bundle.putSerializable("key", YourEnum.TYPE1);

// get 
YourEnum yourenum = (YourEnum) bundle. getSerializable("key"); 

// Intent
// put
intent.putSerializableExtra("key", yourEnum);

// get
yourEnum = (YourEnum) intent.getSerializableExtra("key");

~~~