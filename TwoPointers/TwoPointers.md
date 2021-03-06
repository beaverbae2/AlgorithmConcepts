### Two Pointers (투 포인터)

**참고자료**

- https://code0xff.tistory.com/128
- https://m.blog.naver.com/kks227/220795165570

<br>

**관련문제**

- 구간
  - [백준 1806 부분합](./문제풀이/백준_1806_부분합.md) **(중요)**
  - [2020 카카오 인턴쉽 - 보석 쇼핑](./문제풀이/2020_카카오_인턴쉽_보석쇼핑.md)
- 두 지점
  - [백준 2470 두용액](./문제풀이/백준_2470_두용액.md)

<br>

**정의**

- **연속되는 값(구간)** or **두 지점**을 활용하여 특정 목표값을 찾음
- 시간복잡도 : O(N) -> 선형시간

<br>

**적용방법**

- 구간 or 두 지점을 가르키는 두 개의 포인터 생성
  - start : 시작점
  - end : 끝점
- 문제 조건에 따라
  - start 나
  - end 를 이동시킨다
- **종료 조건** (종료 조건 설정이 어렵당...)
  - start 또는 end의 범위가 올바른 위치가 아닌 경우 종료
    - ex) start > end
    - ex) end >= 배열의 길이
  - 구간 끝까지 잘 탐색하는지 디버깅 해주는게 좋음

<br>

**코드 - [백준 2003 수들의 합 2](https://www.acmicpc.net/problem/2003)**

```java
import java.util.*;
import java.io.*;

/**
 * Two Pointers
 * 
 * @author beaverbae
 *
 */

public class Main {
	public static void main(String[] args) throws Exception {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());

		int[] arr = new int[N];
		st = new StringTokenizer(br.readLine());
		for (int i = 0; i < arr.length; i++) {
			arr[i] = Integer.parseInt(st.nextToken());
		}

		// Two Pointers

		// 초기화
		int start = 0, end = 0, sum = 0, answer = 0;

		// 탐색
		while (true) {
			if (sum >= M) {// start 이동 조건
				if (sum == M) {// 정답인 경우
					answer++;
				}
				sum -= arr[start++];

			} else {// end 이동 조건
				if (end == arr.length) {// 반복문 종료 조건
					break;
				}
				sum += arr[end++];
			}
		}

		System.out.println(answer);
	}
}
```



