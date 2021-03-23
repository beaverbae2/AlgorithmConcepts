### Merge sort

**분류 : 분할 정복**

<br>

**시간 복잡도 : O(NlogN)**

<br>

**접근**

- 배열의 원소가 하나 남을 때까지 분할, 이후 합병하면서 정렬

<br>

**코드**

```java
import java.util.Arrays;

public class Merge_sort {
	public static void main(String[] args) throws Exception {
		int[] arr = {6, 5, 3, 1, 8, 7, 2, 4};
		
		sort(arr, 0, arr.length-1);
		System.out.println(Arrays.toString(arr));
	}

	private static void sort(int[] arr, int low, int high) {
		if (low < high) {
			int mid = (low + high) / 2;
			sort(arr, low, mid);// 왼쪽
			sort(arr, mid+1, high);// 오른쪽
			merge(arr, low, mid, high);// 병합
		}
	}

	private static void merge(int[] arr, int low, int mid, int high) {
		int[] temp = new int[arr.length];// 임시 배열(정렬)
		int i = low;// 왼쪽 배열의 시작 인덱스
		int j = mid+1;// 오른쪽 배열의 시작 인덱스
		int k = low;// 임시 배열의 시작 인덱스
		
		// 왼쪽 or 오른쪽 배열의 중 한쪽의 인덱스 범위 초과시 종료
		while (i <= mid && j <= high) {
			if (arr[i] < arr[j]) {
				temp[k++] = arr[i++];
			} else {
				temp[k++] = arr[j++];
			}
		}
		
		// 남은 원소 추가
		while (i<=mid) {
			temp[k++] = arr[i++];
		}
		
		// 남은 원소 추가
		while (j<=high) {
			temp[k++] = arr[j++];
		}
		
		// 원본 배열에 정렬된 임시 배열의 값 저장
		for (k = low; k <=high; k++) {
			arr[k] = temp[k];
		}
	}
}
```

