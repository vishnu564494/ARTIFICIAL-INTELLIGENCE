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

from collections import deque

def jug():
    cap = (A, B, C)          # capacities
    start = (x, y, z)        # start state
    goal = (gx, gy, gz)      # goal state

    visited = set()
    q = deque([start])

    while q:
        a, b, c = q.popleft()

        if (a, b, c) == goal:
            print(a, b, c)
            return

        if (a, b, c) in visited:
            continue
        visited.add((a, b, c))

        # all pour operations
        q.append((max(0,a-(cap[1]-b)), min(cap[1],b+a), c))
        q.append((max(0,a-(cap[2]-c)), b, min(cap[2],c+a)))
        q.append((min(cap[0],a+b), max(0,b-(cap[0]-a)), c))
        q.append((a, max(0,b-(cap[2]-c)), min(cap[2],c+b)))
        q.append((min(cap[0],a+c), b, max(0,c-(cap[0]-a))))
        q.append((a, min(cap[1],b+c), max(0,c-(cap[1]-b))))
        

def ucs(graph, start, goal):
    visited = set()
    pq = [(0, start)]   # (cost, node)

    while pq:
        cost, node = heapq.heappop(pq)

        if node == goal:
            print("Cost:", cost)
            return

        if node in visited:
            continue
        visited.add(node)

        for neighbor, weight in graph[node]:
            if neighbor not in visited:
                heapq.heappush(pq, (cost + weight, neighbor))

import heapq

def astar(graph, h, start, goal):
    pq = [(0, start)]
    g = {start: 0}

    while pq:
        f, node = heapq.heappop(pq)

        if node == goal:
            print("Cost:", g[node])
            return

        for neigh, cost in graph[node]:
            new_g = g[node] + cost

            if neigh not in g or new_g < g[neigh]:
                g[neigh] = new_g
                f = new_g + h[neigh]
                heapq.heappush(pq, (f, neigh))

                
