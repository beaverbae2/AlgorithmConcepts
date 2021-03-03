### Hash Table

**참고자료**

- https://mangkyu.tistory.com/102

- https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o

<br>

**주요 키워드 : key, value, bucket, hash, hash function**

<br>

**정의**

- key 1개와 value 1개가 1:1로 연결
- key를 통해 value 획득
- key는 고유하다

<br>

**구조**

- 구성요소
  - key : 고유값
  - hash function : key -> hash
  - bucket : hash를 인덱스로 하여 value를 저장하는 배열
- 동작
  - key가 hash function을 통해 hash로 변경
  - hash는 value와 1:1 매칭이 되어 bucket에 저장

<br>

**시간 복잡도**

- 삽입, 삭제, 검색
  - 평균 : O(1)
  - 최악 : O(N)

<br>

**해시 충돌 (Hash collision)**

- 서로 다른 두 개 이상의 key가 같은 hash를 같는 현상

- 무조건 발생한다
  - key는 무한개이고 hash는 유한하므로
- 해결방법
  - 서로 상보적임
  - 분리연결법(Separate Chaining)
    - 기존 값과 총돌 값을 list 또는 tree로 연결
    - 장점
      - 한정된 bucket을 효울적 사용가능
      - hash function의 성능에 덜 의존적
    - 단점
      - 한 hash에 자료가 쏠리면 검색 효율 저하
      - 외부 저장 공간 사용(list)
  - 개방주소법(Open Addressing)
    - 비어있는 해시를 찾아서 저장
    - 방법
      - 선형 탐색(Linear Probing) : 다음 hash(+1) or n개(+n)를 건너뛰어서 비어있는 hash에 저장
      - 제곱 탐색(Quadratic Probing) : 충돌 발생한 hash의 제곱을 한 hash에 저장
      - 이중 해시(Double Hashing) : 다시 해시 함수를 한 번 더 적용하여 새로운 hash 해당
    - 장점
      - 외부 저장 공간 필요 없음
    - 단점
      - hash function의 성능에 영향을 많이 받음(비어있는 hash를 얼마나 빨리 찾느냐...)

<br>

**자바에서 Hash Table과 HashMap의 차이**

- Hash Table은 synchronized 키워드 붙어있음

- Hash Table은 병렬 프로그래밍시 동기화 지원

- HashMap은 자원X