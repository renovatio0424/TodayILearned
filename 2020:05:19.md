# 2020/05/19

## URI (Uniform Resource Identifier) 

### 0. URI 정의
    A Uniform Resource Identifier (URI) is a string of characters that unambiguously identifies a particular resource.
    URI 는 특정 리소스를 명확하게 식별하는 문자열입니다.

### 1. URI 구조

    URI = scheme:[//authority]path[?query][#fragment]
    
  ![URI](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d6/URI_syntax_diagram.svg/2136px-URI_syntax_diagram.svg.png)

### 2. URI Builder

http://blog.yena.io/category/posts?param=study#section 라는 Uri를 만들고 싶을 때.
    
~~~java
  Uri.Builder builder = new Uri.Builder()
      .scheme("http")
      .authority("blog.yena.io")
      .appendPath("category")
      .appendPath("posts")
      .appendQueryParameter("param", "study")
      .fragment("section");

  Uri myUri = builder.build();
~~~

Reference
1. [Wikepedia](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)
2. [[Android] Url 만들기 & Uri.Builder](https://blog.yena.io/studynote/2017/11/05/Android-Uri.html)
