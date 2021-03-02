### Bubble sort

[참고자료](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)

**코드**

```java
import java.util.Arrays;

public class Bubble_sort {
	public static void main(String[] args) {
		int[] input = {6, 15, 5, 7, 25, 12};
		bubble_sort(input);
		System.out.println(Arrays.toString(input));
	}
	
	// 맨 뒤에서 부터 배열이 정렬
	private static void bubble_sort(int[] arr) {
		for (int i = arr.length-1; i >= 0; i--) {
			for (int j = 0; j < i; j++) {
				if (arr[j] > arr[j+1]) {// 내림 차순은 반대로
					int temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}
	}
}
```

