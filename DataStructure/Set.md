### 자바 Set

**참고자료**

- https://soft.plusblog.co.kr/74
- https://coding-factory.tistory.com/554

<br>

**정의 : 중복된 값을 갖지 않는 집합**

<br>

**중복 걸러내는 과정**

- 객체 저장하기 전에 객체의 해시 코드 확인
- 저장되어있는 객체의 **해시 코드**와 비교
  - 모두 다르면 : 저장O
  - 같으면
    - equals() 메소드로 두 객체 비교 후 같으면 중복 판단(저장X)

<br>

**주요 메소드**

- add(Object o) : boolean -> 추가
- remove(Object o) : boolean -> 삭제
- size() : int -> 크기
- contains(Object o) -> boolean -> 해당 요소의 유무
- iterator() : Object -> 탐색 시 사용

<br>

**종류**

- HashSet 
  - 가장 일반적인 set
  - **순서가 보장 되지 않는다**
- LinkedHashSet
  - 순서대로 저장된다
- TreeSet
  - 정렬 가능-> Comparator 활용
  - heap 구조

<br>

**시간 복잡도**

|               | Add/Remove | Contains | Next     | DataStructure        |
| ------------- | ---------- | -------- | -------- | -------------------- |
| HashSet       | O(1)       | O(1)     | O(h/n)   | HashTable            |
| LinkedHashSet | O(1)       | O(1)     | O(1)     | HashTable+LInkedList |
| TreeSet       | O(log n)   | O(log n) | O(log n) | Red-black Tree       |

<br>

**예제 코드**

```java

import java.util.*;
/**
 * 
 * @author beaverbae
 *
 */

public class SetTest {
	public static void main(String[] args) {
		// 선언
		HashSet<String> set = new HashSet<>();
//		LinkedHashSet<String> set = new LinkedHashSet<>();
//		TreeSet<String> set = new TreeSet<>(new Comparator<String>() {// Comparator로 정렬 기준 정하기
//
//			@Override
//			public int compare(String o1, String o2) {
//				return o2.compareTo(o1);// 내림차순 정렬
//			}
//		});
				
		// add
		set.add("A");
		set.add("E");
		set.add("B");
		set.add("B");
		set.add("C");
		set.add("D");
		System.out.println("set에 저장된 값들 : "+set);// 중복 허용X
		System.out.println("set에 A가 있나요? : "+set.contains("A"));
		
		// remove
		set.remove("D");
		set.remove("A");
		System.out.println("set에 저장된 값들 : "+set);// 중복 허용X
		System.out.println("set에 A가 있나요? : "+set.contains("A"));
		
		
		// 탐색 - Iterator 활용
		Iterator<String> iter = set.iterator();
		int idx = 0;
		System.out.println("탐색 시작");
		while(iter.hasNext()) {
			System.out.println(idx+" : "+iter.next());
			idx++;
		}
		System.out.println("탐색 종료");
		
		// 탐색 - for each 문 활용
		idx = 0;
		System.out.println("탐색 시작");
		for (String str : set) {
			System.out.println(idx+" : "+str);
			idx++;
		}
		System.out.println("탐색 종료");
		
	}
}

```

