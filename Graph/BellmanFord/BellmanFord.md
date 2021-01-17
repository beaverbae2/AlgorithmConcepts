### BellmanFord

**관련 문제 : [백준 1865 웜홀](https://www.acmicpc.net/problem/1865)**



**참고자료**

- [벨만포드 설명영상](https://www.youtube.com/watch?v=Ppimbaxm8d8)

- [그림으로 이해하는 벨만 포드](https://ratsgo.github.io/data%20structure&algorithm/2017/11/27/bellmanford/)

- [백준 웜홀 풀이](https://m.blog.naver.com/PostView.nhn?blogId=miyamae&logNo=220918830855&proxyReferer=https:%2F%2Fwww.google.com%2F)



**적용**

- 양의 간선으로만 이루어진 그래프
- 음의 간선도 포함된 그래프
  - 음수 간선 순환이 없는 경우
  - 음수 간선 순환이 있는 경우

-> 다익스트라의 확장 버전



**로직**

1. 출발 노드 설정

2. 최단 거리 테이블(dist) 초기화

3. **vertex-1 의 개수 만큼** 다음을 반복

   - 전체 간선 E개를 하나씩 확인

   - 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블 갱신

- 음수 간선 순환이 발생하는지 확인하려면 3번 과정을 **한 번 더 수행**

  - 최단 거리 테이블의 원소에 변화O : 음수 간선 순환 존재
  - 변화X : 음수 간선 순환 존재



**코드(백준 1865 웜홀)**

```java
import java.util.*;
import java.io.*;

/**
 * BellmanFord
 * @author beaverbae
 * @see https://m.blog.naver.com/PostView.nhn?blogId=miyamae&logNo=220918830855&proxyReferer=https:%2F%2Fwww.google.com%2F
 * @see https://ratsgo.github.io/data%20structure&algorithm/2017/11/27/bellmanford/
 *
 */

public class Main {
	static List<Node> graph;
	static int N, M, W;
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int TC = Integer.parseInt(br.readLine());
		StringBuilder sb = new StringBuilder();
		for (int tc = 0; tc < TC; tc++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			N = Integer.parseInt(st.nextToken());
			M = Integer.parseInt(st.nextToken());
			W = Integer.parseInt(st.nextToken());
			
			graph = new ArrayList<>();
			
			for (int i = 0; i < M; i++) {
				st = new StringTokenizer(br.readLine());
				int start = Integer.parseInt(st.nextToken());
				int end = Integer.parseInt(st.nextToken());
				int cost = Integer.parseInt(st.nextToken());
				
				graph.add(new Node(start, end, cost));
				graph.add(new Node(end, start, cost));
			}
			
			for (int i = 0; i < W; i++) {
				st = new StringTokenizer(br.readLine());
				int start = Integer.parseInt(st.nextToken());
				int end = Integer.parseInt(st.nextToken());
				int cost = Integer.parseInt(st.nextToken());
				
				graph.add(new Node(start, end, (-1) * cost));
			}
			
			if (bellmanford()) sb.append("YES").append("\n");
			else sb.append("NO").append("\n");
		}
		System.out.println(sb);
	}
	
	private static boolean bellmanford() {
		boolean update;//
		int[] dist = new int[N+1];
		final int INF = 987654321;
		
		Arrays.fill(dist, INF);
		dist[1] = 0;
		
		// 시간 복잡도 O(VE)
		// V : 지점의 수
		// E : 간선의 수
		// N번 체크(지점의 수)
		for (int cnt = 0; cnt < N; cnt++) {//모든 지점들에 대해 수행
			update = false;
			for (Node node : graph) {//모든 간선에 대해 수행
				if (dist[node.end] > dist[node.start] + node.cost) { 
					dist[node.end] = dist[node.start] + node.cost;
					update = true;
				}
			}
			
			if (!update) return false;
		}
		
		return true;//N번째에도 갱신 된다면 음수 사이클이 존재
	}

	static class Node {
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
	}
}

```