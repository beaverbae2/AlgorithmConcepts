### Selection sort

[참고자료](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)

**코드**

```java
import java.util.Arrays;

public class Selection_sort {
	public static void main(String[] args) {
		int[] input = {6, 15, 5, 7, 25, 12};
		selection_sort(input);
		System.out.println(Arrays.toString(input));
	}
	
	// 현재 인덱스의 값과 최솟값의 위치를 swap
	private static void selection_sort(int[] arr) {
		for (int i = 0; i < arr.length-1; i++) {
			int min_index = i;
			
			for (int j = i+1; j < arr.length; j++) {
				if (arr[min_index] > arr[j]) {
					min_index = j;
				}
			}
			
			// swap
			int temp = arr[min_index];
			arr[min_index] = arr[i];
			arr[i] = temp;
		}
	}
}
```

