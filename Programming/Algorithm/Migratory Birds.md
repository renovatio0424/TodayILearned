# 2020/02/13

## Migratory Birds (Algorithm) [reference](https://www.hackerrank.com/challenges/migratory-birds/problem)

### Problem 
당신은 다른 대륙으로 이주하는 새들의 수를 연구를 돕도록 요청받았습니다. 
당신이 관심있는 각 타입별 새들은 Integer 값으로 구분이 가능합니다. 
특정 종류의 새들이 관측 될때마다, sightings 배열에 추가됩니다. 
당신의 일은 만약 두 종류 이상의 새들이 같으면 가장 작은 id 값을 선택해서 type number 를 print 하세요

### example

~~~
// 다음의 배열이 주어진다면
arr = [1,1,2,2,3]
// 1,2 타입은 2
// 3 타입은 1
print 1
~~~

### 해결 방법
  1. 각 타입별 카운트를 한다.
  2. 카운트 값이 2이상이고 value 가 max인 key를 찾는다

### HashMap 에서 Max 값인 키 찾기 [reference](https://stackoverflow.com/questions/5911174/finding-key-associated-with-max-value-in-a-java-map)

~~~java
Collections.max(typeMap.entrySet(), Map.Entry.comparingByValue()).getKey()
~~~

### Solution

~~~java
List<Integer> arr = new ArrayList();

arr.add(1);
arr.add(4);
arr.add(4);
arr.add(4);
arr.add(5);
arr.add(3);

// 각 타입 별로 몇번씩 겹쳤는지 카운트
HashMap<Integer,Integer> typeMap = new HashMap<>();

for (int birdType : arr) {
  if(typeMap.containsKey(birdType)){
  int beforeCount = typeMap.get(birdType);
  typeMap.put(birdType, ++beforeCount);
} else
  typeMap.put(birdType, 1);
}

// 카운트 수가 2보다 크고 가장 큰 수 선택
int result =  Collections.max(typeMap.entrySet(), Map.Entry.comparingByValue()).getKey();

System.out.println(result);
~~~

--------------------------------------------
## Class Hierarchy 보기 (Android Studio Shorcut)
~~~
mac : control(^) + H
~~~
