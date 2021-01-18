### ArrayList vs LinkedList

[참고자료](https://www.nextree.co.kr/p6506/)



**성능비교**

|                 | ArrayList | LinkedLIst         |
| --------------- | --------- | ------------------ |
| 인덱싱          | O(1)      | O(n)               |
| 맨 앞 삽입/삭제 | O(n)      | O(1)               |
| 맨 뒤 삽입/삭제 | O(1)      | O(1) or O(n)       |
| 중간 삽입/삭제  | O(n)      | search time + O(1) |

- 삽입 삭제가 빈번한 경우 : LinkedList 사용
- 인덱싱을 자주 해야하는 경우 : ArrayList 사용