### Merge sort

**분류 : 분할 정복**

<br>

**시간 복잡도 : O(NlogN)**

<br>

**접근**

- 배열의 원소가 하나 남을 때까지 분할, 이후 합병하면서 정렬
- 분할
  - low: 시작 인덱스, high : 끝 인덱스, mid : 중간 인덱스
  - 분할 : mid를 기준으로 두 개로 분할
    - 범위 1 : (low, mid)
    - 범위 2 : (mid+1, high)
  - 합병 : 분할된 두 배열(**정렬되어 있음**)을 **순서대로** 합침
    - 임시 배열 필요 : 공간 복잡도 

<br>

**코드**

```java
package A2021_04_09;

import java.util.Arrays;

public class MergeSort {
	public static void main(String[] args) {
		int[] arr = {6, 5, 3, 1, 8, 7, 2, 4, 5};
		merge_sort(arr, 0, arr.length-1);
		System.out.println(Arrays.toString(arr));
	}
	
	private static void merge_sort(int[] arr, int low, int high) {
		if (low < high) {
			int mid = (low + high) / 2;
			merge_sort(arr, low, mid);// 정렬이 되어 있는 상태
			merge_sort(arr, mid+1, high);// 정렬이 되어 있는 상태
			merge(arr, low, mid, high);
		}
	}

	private static void merge(int[] arr, int low, int mid, int high) {
		int l = low;
		int r = mid+1;
		
		int[] temp = new int[high-low+1];// 임시배열, 공간 복잡도 줄이기
		int idx = 0;
		
		// 한쪽의 인덱스가 벗어날 때까지 반복
		while (l <= mid && r <= high) {
			if (arr[l] < arr[r]) {
				temp[idx] = arr[l];
				l++;
				idx++;
			} else {
				temp[idx] = arr[r];
				r++;
				idx++;
			}
		}
		
		// 남아있는 왼쪽 인덱스에 대해 작업
		while (l <= mid) {
			temp[idx++] = arr[l++];
		}
		
		// 남아있는 오른쪽 인덱스에 대해 작업
		while (r <= high) {
			temp[idx++] = arr[r++];
		}
		
		idx = 0;
		for (int i = low; i <= high; i++) {
			arr[i] = temp[idx++];
		}
	}
}
```

