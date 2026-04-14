def bfs(graph, start):
    visited = set()          
    queue = deque([start])  

    visited.add(start)

    while queue:
        node = queue.popleft()   # Dequeue
        print(node, end=" ")

        # Visit all neighbors
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)


def dfs(graph, node, visited):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)

        # Visit all neighbors
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)
            
                
