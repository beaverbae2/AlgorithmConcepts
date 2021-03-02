### Insertion sort

[참고자료](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)

**코드**

```java
import java.util.Arrays;

public class Insertion_sort {
	public static void main(String[] args) {
		int[] input = {6, 15, 5, 7, 25, 12};
		insertion_sort(input);
		System.out.println(Arrays.toString(input));
	}
	
	// i 앞의 배열들은 모두 정렬된 상태
	private static void insertion_sort(int[] arr) {
		for (int i = 1; i < arr.length; i++) {
			int temp = arr[i];
			int j = i-1;
			while (j >= 0 && temp < arr[j]) {
				arr[j+1] = arr[j];
				j--;
			}
			
			arr[j+1] = temp;
		}
	}
}
```

