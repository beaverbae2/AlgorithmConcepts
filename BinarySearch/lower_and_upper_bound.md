### lower bound와 upper bound

**참고자료**

- https://velog.io/@junhok82/lowerbound-upperbound

<br>

**정의**

- 배열 arr가 오름차순 정렬되어 있을 때, 어떤 target값을 개수를 구함

- lower bound : target값과 같거나 큰 원소들중 가장 작은 인덱스 구함
- upper bound : target값보다 큰 원소들중 가장 작은 인덱스 구함

<br>

**원리**

![](./bound.png)

- 초기화
  - left : 0
  - right : N (배열의 크기)
  - [left, right)

- lower bound

  - arr[mid] >= target인 경우
    - mid(현재 인덱스)가 정답 후보
    - 다음 단계에 mid의 왼쪽, 즉 [left , mid) 구간에서 **target보다 크거나 같은 값** 또 존재하는지 확인 필요
    
  - arr[mid] < target 인 경우
    - 다음 단계에 mid의 오른쪽 [mid+1, right) 구간 확인

- upper bound

  - arr[mid] > target인 경우
    - mid(현재 인덱스)가 정답 후보
    - 다음 단계에 mid의 왼쪽 (left, mid) 구간에서 **target 보다 큰 값**이 또 존재하는지 확인 필요

  - arr[mid] <= target 인 경우
    -  다음 단계에 mid의 오른쪽  [mid+1, right) 구간 확인

<br>

**구현 코드**

```java
/**
 * 
 * @author beaverbae
 * @see https://velog.io/@junhok82/lowerbound-upperbound
 * 
 */

public class Lower_Upper_bound {
	static int[] arr = {1, 2, 3, 3, 3, 4, 5, 6};
	static int N = arr.length;
	static final int target = 3;
	
	public static void main(String[] args) {
		System.out.println(lower_bound());
		System.out.println(upper_bound());
	}
	
	private static int lower_bound() {
		int left = 0;
		int right = N;
		
		while (left < right) {
			int mid = (left + right) / 2;
			
			if (arr[mid] >= target) {
				right = mid;
			} else {
				left = mid + 1;
			}
		}
		
		return right;
	}
	
	private static int upper_bound() {
		int left = 0;
		int right = N;
		
		while (left < right) {
			int mid = (left + right) / 2;
			
			if (arr[mid] > target) {
				right = mid;
			} else {
				left = mid + 1;
			}
		}
		
		return right;
	}
}
```

