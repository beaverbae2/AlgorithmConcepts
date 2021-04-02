### Floyd-Warshall(플로이드 와샬) 알고리즘

**[참고자료](https://blog.naver.com/ndb796/221234427842)**

<br>

**관련 문제**

- [백준 21278 호석이 두마리 치킨](./문제풀이/백준_21278_호석이_두마리_치킨.md)
- [백준 10159 저울](./문제풀이/백준_10159_저울.md)
- [백준 1613 역사](./문제풀이/백준_1613_역사.md)

<br>

**정의**

- **모든 정점**에서 **모든 정점**으로의 최단거리
- `distance[a][b] = min(distance[a][b], distance[a][c]+distance[c][b])`

- c : 거쳐가는 중간 정점

<br>

**시간복잡도**

- O(n^3)

<br>

**적용방법**

1. distance 배열 초기화
   1. 출발점과 도착점이 같은 경우 0
   2. 나머지 INF
2. `distance[a][b] = min(distance[a][b], distance[a][c]+distance[c][b])`

<br>

**코드**

```java
import java.util.*;
import java.io.*;

/**
 * Floyd-Warshall
 * @author beaverbae
 *
 */

public class Main {
	static final int INF = 987654321;

	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		int M = Integer.parseInt(br.readLine());

		// 초기화
		int[][] dist = new int[N + 1][N + 1];
		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= N; j++) {
				if (i == j)
					continue;

				dist[i][j] = INF;
			}
		}
		
		// 입력
		for (int i = 0; i < M; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());

			dist[a][b] = Math.min(dist[a][b], w);
		}
		
		
		// 플로이드 와샬
		for (int k = 1; k <= N; k++) {// 거쳐가는 정점
			for (int i = 1; i <= N; i++) {// 출발 정점
				for (int j = 1; j <= N; j++) {// 도착 정점
					dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
				}
			}
		}
		
		// 정답 출력
		StringBuilder sb = new StringBuilder();
		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= N; j++) {
				if (dist[i][j] != INF) {
					sb.append(dist[i][j]).append(" ");
				} else {
					sb.append(0).append(" ");
				}
			}
			sb.append("\n");
		}

		System.out.println(sb.toString());
	}
}
```

