# DFS

### Date: 2024.01.09

---
### DFS(Depth-First Search)
- 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법
- **모든 노트**를 탐색하고자 할 때 유리하다.
- 방문 여부를 검사하는 것이 중요하다.


![](img/dfs.png?raw=true)

- 두 노드 f, t 간의 연결이 입력으로 들어올 경우, 다음과 같이 인접 리스트를 구현한다.

```python
for _ in range(M):
    f, t = map(int, input().split())
    if graph[f] == []:
        graph[f] = [t]
    else:
        graph[f].append(t)
    if graph[t] == []:
        graph[t] = [f]
    else:
        graph[t].append(f)
```

- DFS는 **Stack** 혹은 **Recursion**으로 구현된다.


### Stack

```python
def dfs(graph, start_node):
    ## deque 패키지 불러오기
    from collections import deque
    visited = []
    need_visited = deque()
    
    ##시작 노드 설정해주기
    need_visited.append(start_node)
    
    ## 방문이 필요한 리스트가 아직 존재한다면
    while need_visited:
        ## 시작 노드를 지정하고
        node = need_visited.pop()
 
        ##만약 방문한 리스트에 없다면
        if node not in visited:
 
            ## 방문 리스트에 노드를 추가
            visited.append(node)
            ## 인접 노드들을 방문 예정 리스트에 추가
            need_visited.extend(graph[node])
                
    return visited
```

### Recursion

```python
def dfs_recursive(graph, start, visited = []):
## 데이터를 추가하는 명령어 / 재귀가 이루어짐 
    visited.append(start)
 
    for node in graph[start]:
        if node not in visited:
            dfs_recursive(graph, node, visited)
    return visited
```


### References
- [깊이 우선 탐색(DFS)이란](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)
- [DFS 완벽 구현하기(Python)](https://data-marketing-bk.tistory.com/entry/DFS-%EC%99%84%EB%B2%BD-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-%ED%8C%8C%EC%9D%B4%EC%8D%AC)
