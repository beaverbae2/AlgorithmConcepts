### Quick sort

**분류 : 분할 정복**

<br>

**시간복잡도**

- 일반 : O(NlogN)
- 최악(오름차순) : O(N^2)

<br>

**접근**

- pivot을 설정하여, pivot의 왼쪽에는 pivot보다 작은 값, 오른쪽에는 pivot보다 큰 값
- pivot은 정렬되어 있다

<br>

**코드**

```java
/**
 * 
 * @author beaverbae
 * @see https://m.blog.naver.com/ndb796/221226813382
 */

public class Quick_sort {
	public static void main(String[] args) {
		int[] arr = {1, 10, 5, 8, 7, 6, 4, 3, 2, 5};
		sort(arr, 0, arr.length-1);
		System.out.println(Arrays.toString(arr));
	}
	
	private static void sort(int[] arr, int start, int end) {
		if (start < end) {// q는 정렬된 위치
			int q = partition(arr, start, end);
			System.out.println(q);
			sort(arr,start, q-1);
			sort(arr,q+1, end);
		}
	}

	private static int partition(int[] arr, int start, int end) {
		int pivot = start;// 첫번째를 기준으로 잡음
		int low = start+1;
		int high = end;
		
		// 기준값(arr[pivot]) 보다 작은 값은 pivot 왼쪽으로, 큰 값은 오른쪽으로
		while (low <= high) {
			while (low <= end && arr[low] <= arr[pivot]) {//pivot 값보다 작거나 같은 원소가 나오는 경우
				low++;
			}
			
			while (high > start && arr[high] > arr[pivot]) {//pivot 값보다 큰 원소가 나오는 경우
				high--;
			}
			
			if (low > high) {// 교차한 경우
				swap(arr, pivot, high);
			} else {
				swap(arr, low, high);
			}
		}
		
		return high;
	}
	
	private static void swap(int[] arr, int i, int j) {
		int temp = arr[j];
		arr[j] = arr[i];
		arr[i] = temp;
	}
```

