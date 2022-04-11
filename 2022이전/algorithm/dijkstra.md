# Dijkstra (다익스트라)

> 다익스트라 알고리즘은 그래프에서 출발점에서 목표점 까지의 최단거리를 구할 때 사용하는 알고리즘



![](./image/dijkstra.PNG)



### 사용 변수

* distance 배열 : 각각의 노드까지의 최단거리 저장하는 배열
* check 배열 : 각각의 노드를 방문했는지 체크



### 순서

1. Edge class 생성 (end 연결된 노드, value 가중치)
2.  ArrayList[] 배열 생성하여 노드 관계를 초기화 
3. distance 배열을 가장 큰 값으로 초기화 (Integer.MAX_VALUE)
4. 우선순위 큐 생성
5. 시작노드 우선순위 큐 넣고, distance 배열에 시작노드 0으로 초기화
6. bfs를 통해 방문한 노드 check 배열 true 변경, distance 값 최소 비교후 갱신



### 주요 코드

```java
        // 우선순위 큐를 사용해야 한다. 성능이 더 좋아짐
        PriorityQueue<Integer> q = new PriorityQueue<Integer>();
        // 시작점 설정해주고 시작점 - 시작점 거리는 0이다.
        q.add(K);
        distance[K] = 0;
        while (!q.isEmpty()) {
            // 다음에 방문할 vertex 설정
            int current = q.poll();
            // 방문했기 떄문에 true, INF는 아니다.
            visited[current] = true;
 
            for (int i = 0; i < list[current].size(); i++) {
                // 현재 vertex에서 다음 vertex를 차근차근 비교해서 우선순위 큐에 넣어야한다.
                int next = list[current].get(i).end; // 다음 vertex
                int value = list[current].get(i).value; // 현재 - 다음 간 edge값
 
                // 이전에 있던 값이 더 크다면 굳이 다시 방문할 필요가 없다. 이미 그 전이 더 최단 경로이기 때문에
                if (distance[next] > distance[current] + value) {
                    distance[next] = Math.min(distance[next], value + distance[current]);
                    q.add(next);
 
                }
 
            }
        }
```





### 문제

[백준 1753](https://www.acmicpc.net/problem/1753)



### 정리된 코드

[다익스트라-우선순위큐사용-코드](https://github.com/kyun9/PracticeAlgorithm/blob/master/src/p2021_1/다익스트라연습.java)

[dijkstra code - 1](https://github.com/kyun9/PracticeAlgorithm/blob/master/src/B_Study/B_Dijkstra_1753.java)

[dijkstra code - 2](https://github.com/kyun9/PracticeAlgorithm/blob/master/src/B_Study/B_Dijkstra_1753_2.java)

