### UnionFind

**참고자료**

- https://gmlwjd9405.github.io/2018/08/31/algorithm-union-find.html
- https://m.blog.naver.com/ndb796/221230967614

<br>

**정의**

- disjoint set (서로소 집합) 만들기
- **집합** A와 B가 서로소 인가 확인
  - A : {1, 2, 5}
  - B : {3, 4}
  - 집합 A와 B는 서로소
- 그래프에서 노드 A와 노드 B가 같은 **그래프**에 속하는지 확인

<br>

**구현**

1. parent 배열 

   ```java
   int[] parent = new int[N];// parent[i] = i번쨰 노드의 부모(최상단) 노드
   ```

2. parent 배열 초기화

   ```java
   public static void initParent() {
   	for (int i = 1; i < parent.length; i++) {
   		parent[i] = i; // 자기 자신을 부모 노드로 초기화
   	}
   }
   ```

3. 부모 찾기 (그래프의 최상단노드 찾기 / 집합의 대표값 찾기)

   ```java
   public static int getParent(int v) {// 부모 노드와 자기 자신이 같을 때까지 반복	
   	if (parent[v] == v) return parent[v]; 	
   	return parent[v] = getParent(parent[v]);// 경로 압축
   }
   ```

4. 부모 합치기 (서로 다른 두 그래프 합치기 / 서로소인 두 집합 합치기)

   ```java
   public static void unionParent(int a, int b) {
       a = getParent(a);
       b = getParent(b);
       
   	// 크기가 작은 노드를 부모로 함
       if (a < b) parent[b] = a; 
       else parent[a] = b;
   }
   ```

5. 같은 부모를 가지는지 확인 (같은 그래프에 있는지 / 같은 집합에 속하는 원소인지)

   ```java
   public static boolean findParent(int a, int b) {
       a = getParent(a);
       b = getParent(b);
   
       if (a == b) return true;
       return false;
   }
   ```

<br>

**전체 코드**

```java
import java.util.Arrays;

public class UnionFind {
	private static int[] parent;// parent[i] = i번쨰 노드의 부모 노드

	public static void main(String[] args) {
		parent = new int[4 + 1];

		// 주의 : 1과 2는 서로 같은 집합(그래프)이다!!
		// 같은 집합(그래프)이어도 parent의 원소는 다를 수 있다
		// 두 원소(노드)가 같은 집합(그래프)에 속하는지 확인할 땐 findParent를 실행
		
		// 1
		initParent();
		unionParent(1, 2);
		unionParent(2, 3);
		unionParent(3, 4);
		System.out.println(Arrays.toString(parent));// [0, 1, 1, 1, 1]
		System.out.println(findParent(1, 4));// true
		System.out.println(Arrays.toString(parent));// [0, 1, 1, 1, 1]
		System.out.println(findParent(2, 3));// true
		System.out.println(Arrays.toString(parent));// [0, 1, 1, 1, 1]

		// 2
		initParent();
		unionParent(3, 4);
		unionParent(2, 3);
		unionParent(1, 4);
		System.out.println(Arrays.toString(parent));// [0, 1, 1, 2, 2]
		System.out.println(findParent(1, 4));// true
		System.out.println(Arrays.toString(parent));// [0, 1, 1, 2, 1]
		System.out.println(findParent(2, 3));// true
		System.out.println(Arrays.toString(parent));// [0, 1, 1, 1, 1]
	}

	// parent 배열 초기화
	public static void initParent() {
		for (int i = 1; i < parent.length; i++) {
			parent[i] = i;
		}
	}

	// 부모 찾기
	public static int getParent(int v) {
		if (parent[v] == v) return parent[v];
		return parent[v] = getParent(parent[v]);
	}

	// 부모 합치기
	public static void unionParent(int a, int b) {
		a = getParent(a);
		b = getParent(b);

		if (a < b) parent[b] = a;
		else parent[a] = b;
	}

	// 같은 부모를 가지는지 확인
	public static boolean findParent(int a, int b) {
		a = getParent(a);
		b = getParent(b);

		if (a == b) return true;
		return false;
	}

}
```

