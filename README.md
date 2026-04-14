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

def water_jug(cap1, cap2, goal):
    visited = set()
    q = deque([(0, 0)])

    while q:
        x, y = q.popleft()

        if x == goal or y == goal:
            print(x, y)
            return

        if (x, y) in visited:
            continue
        visited.add((x, y))

        # operations
        q.append((cap1, y))   
        q.append((x, cap2))   
        q.append((0, y))      
        q.append((x, 0))      
        q.append((x - min(x, cap2-y), y + min(x, cap2-y)))  
        q.append((x + min(y, cap1-x), y - min(y, cap1-x)))  
            
                
