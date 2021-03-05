### MST(Minimum Spanning Tree)

**참고자료**

- https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html

<br>

**트리와 그래프의 차이**

- 트리는 사이클이 없는 그래프이다

<br>

**Spanning Tree**

- 최소 연결 부분 그래프
- 정점의 개수가 n일 때, 간선을 n-1개 뽑음
- 하나의 그래프에는 많은 Spanning Tree가 존재 가능

<br>

**Minimum Spanning Tree**

- Spanning Tree 중 가중치 합이 가장 작은 그래프

<br>

**정리하자면 MST는**

- 사이클이 없고
- n개의 정점을 가지는 그래프에서, n-1 개의 간선만을 사용하고

- 간선의 가중치 합이 최소인 트리이다

<br>

**MST의 구현**

- [Kruskal 알고리즘](./Kruskal_알고리즘.md)
- Prim 알고리즘

