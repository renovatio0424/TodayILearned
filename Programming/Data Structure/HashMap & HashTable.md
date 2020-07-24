# 2020/02/12

## HashMap & HashTable 	[(video)](https://img.youtube.com/vi/KyUTuwz_b7Q/0.jpg)

[![Reference](https://img.youtube.com/vi/KyUTuwz_b7Q/0.jpg)](https://www.youtube.com/watch?v=KyUTuwz_b7Q)

### 1. Hash Table
	찾는 순서
	1. 배열에 특정 값을 저장한다
	2. 찾고자하는 값으로 계산하여 해당 값이 저장되어 있는 인덱스를 알아낸다
	3. 계산한 인덱스에서 값을 리턴한다
	=> 원하는 값을 가장 빠르게 찾는 방법


example) 

|  |  |  |  | Mia |  |  |  |  |  |  |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|

	1. Mia 를 찾고 싶다
	2. Mia 의 해쉬값을 찾는다

	M = 77
	i = 105
	a = 97 
	total = M + i + a = 279 
	hash = 279 % 11 = 4
	
	3. hash 값으로 원하는 값을 입력 또는 찾는다

### 2. Hashing Algorithm

	- key 값을 주소로 바꿔주는 계산
	- 숫자로 된 키값은 가용한 메모리 만큼 나누고 나머지를 사용한다.
	- 알파벳으로 된 키값은 아스키 코드의 합을 가용 메모리 만큼 나누고 나머지를 사용한다. 
	- Folding method 는 키를 같은 부분으로 값들의 합을 나누고 나머지를 사용한다. 

	ex) 01452 8345654
	-> 01 + 45 + 28 + 34 + 56 + 54 = 218

### 3. Collisions
: 같은 인덱스에 다른 값이 들어가야 되는 경우

	1. Load Factor = 저장된 아이템의 총 갯수 / 배열의 크기 => load factor 가 작을 수록 효율이 좋다
	2. best case = collision 이 없는 경우 
	3. worst case = collision 이 많은 경우
	
### 4. Collision 해결법
	- Open Addressing
		- Linear probing
		- plus 3 rehash
		- quadratic probing (failed attempt)^2
		- Double hashing 
	- Closed Addressing
	
### 5. 해쉬 함수의 요구 사항
	- collision 최소화
	- 일정하게 분배된 해쉬 값
	- 쉬운 계산
	- 어떤 collision 이든 해결이 되어야함
	
### 6. Summary
	- 많은 양의 데이터를 인덱싱할 때 사용
	- 각 키들에 대한 주소는 키에 의해 계산된다
	- Collision 은 open or closed addressing 을 통해 해결 할 수 있다. 
	- 해싱은 데이터베이스 인덱싱, 컴파일러, 캐싱, 비밀번호 인증 등등 에서 사용된다. 
	- 삽입, 삭제, 제거 가 같은 시간 안에 처리된다. (데이터가 많든 적든)
