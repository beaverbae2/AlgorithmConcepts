### 자바 Map

**참고자료**

- https://soft.plusblog.co.kr/74

<br>

**정의**

- <key, value> 쌍으로 이뤄진 자료구조
- key는 고유값이며,  key를 통해 value를 확인

<br>

**주요 메소드**

- put(Object key, Object value) : boolean
  - 추가
  - 이미 같은 key값이 존재하는 경우 새로운 value로 바뀐다
- remove(Object key) : boolean
  - 삭제
- get(Object key) : Object
  - key와 쌍을 이루는 value확인
- containsKey(Object key) : boolean
  - 해당 key를 가지고 있는지 확인
- size() : int
  - 크기 반환
- iterator() : Object -> 탐색 시 사용

<br>

**종류**

- **여기서 말하는 순서는 key가 기준**

- HashMap
  - 가장 일반적인 map
  - 순서가 ~~지맘대로~~ 이다(순서 보장X)

- LinlkedHashMap
  - key값 입력 순으로 순서가 보장
- TreeMap
  - key값이 대해 정렬 가능-> Comparator 활용
  - heap 구조

<br>

**시간복잡도**

|               | Get/Add/Remove | Contains | Next     | DataStructure           |
| ------------- | -------------- | -------- | -------- | ----------------------- |
| HashMap       | O(1)           | O(1)     | O(h/n)   | Hash Table              |
| LinkedHashMap | O(1)           | O(1)     | O(1)     | Hash Table + LinkedList |
| TreeMap       | O(log n)       | O(log n) | O(log n) | Red - black tree        |

<br>

**예제 코드**

```java

import java.util.*;

public class MapTest {
	public static void main(String[] args) {
		HashMap<String, Integer> map = new HashMap<>();
//		LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
//		TreeMap<String, Integer> map = new TreeMap<>(new Comparator<String>() {// Comprator로 정렬 기준 정하기
//
//			@Override
//			public int compare(String o1, String o2) {
//				
//				return o2.compareTo(o1);// 내림차순으로 정리
//			}
//		});
		String[] fruits = {"banana", "apple", "orange", "kiwi", "peach"};
	
		// 추가
		int n = 0;
		for (String fruit : fruits) {
			map.put(fruit, n);
			n++;
		}
		System.out.println("map : "+map);
		map.put("banana", n);// 이미 가지고 있는 key 한 번 더 추가
		System.out.println("map : "+map);
		
		// 삭제
		map.remove("banana");
		System.out.println("banana 있어요 ? : "+map.containsKey("banana"));
		
		// 탐색
		Iterator<String> iter = map.keySet().iterator();
		while(iter.hasNext()) {
			String key = iter.next();
			System.out.println("key : "+key+", value : "+map.get(key));// value 얻기
		}
		
	}
}

```

