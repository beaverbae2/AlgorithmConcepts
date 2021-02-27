### 파라메트릭 서치

[참고 자료](https://sarah950716.tistory.com/16)

<br>

**관련 문제**

- [백준 1654 랜선 자르기](./문제풀이/백준_1654_랜선_자르기.md)
- [백준 2110 공유기 설치](./문제풀이/백준_2110_공유기_설치.md)
- [2019 카카오 겨울 인턴쉽 - 징검다리 건너기](./문제풀이/2019_카카오_겨울_인턴쉽-징검다리_건너기.md)

<br>

**정의**

- **최적화 문제** (문제 상황을 만족하는 특정 변수의 최댓값 or 최솟값)을 **결정 문제**(해당 값이 정답인가 아닌가)로 변환
- 다음의 조건 충족
  - **결정 문제**로 변환했을 때 쉽게 풀리는 경우
  - 최솟값을 구하는 경우 : 최솟값이 x라면, **x이상의 값은 문제의 조건 모두 만족**
  - 최댓값을 구하는 경우 : 최댓값이 x라면, **x이하의 값은 문제의 조건 모두 만족** 

<br>

**적용 방법**

- 예시 문제 : [백준 2805 나무 자르기](https://www.acmicpc.net/problem/2805) 

- 최적화 문제 : 적어도 M미터의 나무를 가져가기 위한 **절단기 높이의 최댓값**

- 결정 문제 

  - **현재 할당한 절단기의 높이**에서 M미터 이상의 나무를 가져갈 수 있는가

  - 초기화 
    - 절단기의 최소 높이(start 또는 left) : 0
    - 절단기의 최대 높이(end 또는 right) : 주어진 나무 중 최댓값
  - 탐색
    - **현재 할당한 절단기 높이(mid) 에서 나무를 몇 미터 가져갈 수 있는지 조사**
    - M미터 보다 작다면 
      - 나무를 **더** 잘라야함 -> 절단기 높이를 더 **낮춤**
      - 절단기의 최대 높이 = 현재 높이 - 1
    - M미터 이상이라면
      - **정답이 될 수 있는 조건**
      - 나무를 **덜** 잘라야함 -> 절단기 높이를 더 **높임**
      - 절단기의 최소 높이 = 현재 높이+1

<br>

**코드**

```java
import java.util.*;
import java.io.*;

/**
 * Parametric Search
 * @author beaverbae
 *
 */

public class Main {
	static int[] input;
	static int N;
	static long M;
	static long max;
	
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		
		input = new int[N];
		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < N; i++) {
			input[i] = Integer.parseInt(st.nextToken());
			max = Math.max(max, input[i]);
		}
		
		System.out.println(parametric_search());
	}
	
	private static long parametric_search() {
		long result = 0;
		
		long start = 0;
		long end = max;
		
		while(start<=end) {
			long mid = (start+end)/2;// 절단기의 높이
			
			long sum = 0;
			for (int i = 0; i < input.length; i++) {
				if (input[i] - mid <= 0) continue;
				
				sum += (input[i] - mid);
			}
			
			if (sum < M) {// 자르는 높이는 줄여야함
				end = mid-1;
			} else {
				start = mid+1;
				result = mid;
			}
		}
		
		return result;
	}
	
}
```

