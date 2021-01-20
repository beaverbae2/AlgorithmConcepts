### Kruskal 알고리즘

**참고자료**

- https://m.blog.naver.com/ndb796/221230994142

<br>

**적용 -> UnionFind 활용**

1. 그래프의 간선을 가중치 크기 순으로 오름차순 정렬
2. 간선이 (V(정점의 개수) - 1) 개가 될때 까지 다음을 반복 
   1. 정렬된 그래프에서 간선을 하나씩 꺼내서 현재까지 형성된 MST가 사이클이 생기는 확인 -> **find 활용**
   2. 사이클을 형성한다면 : 포함X
   3. 포함하지 않는다면 : 포함O -> **union 활용**

<br>

**코드 - [프로그래머스 섬 연결하기](https://programmers.co.kr/learn/courses/30/lessons/42861)**

```java
import java.util.*;
/**
 * MST - Kruskal
 * @author beaverbae
 *
 */
class Solution {
    private int[] parent;
	private List<Node> graph;

	public int solution(int n, int[][] costs) {
		// parent 초기화
		parent = new int[n];
		for (int i = 0; i < parent.length; i++) {
			parent[i] = i;
		}

		// graph 초기화 및 간선 추가
		graph = new ArrayList<>();
		for (int i = 0; i < costs.length; i++) {
			int start = costs[i][0];
			int end = costs[i][1];
			int cost = costs[i][2];

			graph.add(new Node(start, end, cost));
		}

		// 비용의 오름차순으로 graph 정렬
		Collections.sort(graph);

		int cnt = 0;// MST에 추가된 간선의 개수
		int answer = 0;
		for (Node node : graph) {// MST 생성
			int start = node.start;
			int end = node.end;
			int cost = node.cost;

			if (findParent(start, end))// 사이클이 존재하면 pass
				continue;

			unionParent(start, end);
			answer += cost;
			cnt++;

			if (cnt == n - 1)
				break;// 간선의 개수가 (정점 개수 - 1)이면 종료
		}

		return answer;
	}

	public int getParent(int v) {
		if (parent[v] == v)
			return parent[v];
		return parent[v] = getParent(parent[v]);
	}

	public void unionParent(int a, int b) {
		a = getParent(a);
		b = getParent(b);

		if (a < b)
			parent[b] = a;
		else
			parent[a] = b;
	}

	public boolean findParent(int a, int b) {
		a = getParent(a);
		b = getParent(b);

		if (a == b)
			return true;
		return false;
	}

	static class Node implements Comparable<Node> {
		int start, end, cost;

		public Node(int start, int end, int cost) {
			this.start = start;
			this.end = end;
			this.cost = cost;
		}

		@Override
		public String toString() {
			return "Node [start=" + start + ", end=" + end + ", cost=" + cost + "]";
		}

		@Override
		public int compareTo(Node o) {
			return Integer.compare(this.cost, o.cost);// 비용의 오름차순으로 정렬
		}
	}
}
```

