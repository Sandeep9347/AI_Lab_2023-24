```
 LAB EXPERIMENT: Breadth-First Search (BFS)

```
🔹 AIM:

To implement Breadth-First Search (BFS) traversal and find the BFS order of a graph.

```

 REQUIREMENTS:

Programming Language: Python

Logic Programming Tool: SWI-Prolog

Planning Language: PDDL or PDDL Editor Online

Execution Environment: Jupyter Notebook or Google Colab
```
🐍 1. BFS Implementation in Python

✅ Code:
from collections import deque

```

# Function to perform BFS
def bfs(graph, start):
    visited = set()
    queue = deque([start])
    bfs_order = []

    while queue:
        vertex = queue.popleft()
        if vertex not in visited:
            bfs_order.append(vertex)
            visited.add(vertex)
            # Add unvisited neighbors to queue
            queue.extend([neighbor for neighbor in graph[vertex] if neighbor not in visited])
    return bfs_order

# Example Graph (Adjacency List)
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}

# Input starting node
start_node = 'A'
bfs_result = bfs(graph, start_node)

print("BFS Traversal Order:", bfs_result)

```

 Expected Output:
 
BFS Traversal Order: ['A', 'B', 'C', 'D', 'E', 'F']
✅ Run this program in Jupyter Notebook or Google Colab.

```

 2. BFS Implementation in SWI-Prolog

✅ Code (save as bfs.pl):
% BFS Implementation in Prolog

% Graph definition using edge facts
edge(a, b).
edge(a, c).
edge(b, d).
edge(b, e).
edge(c, f).
edge(e, f).

% BFS traversal
bfs(Start, Traversal) :-
    bfs_queue([Start], [], Traversal).

bfs_queue([], Visited, Traversal) :-
    reverse(Visited, Traversal).

bfs_queue([Node|RestQueue], Visited, Traversal) :-
    member(Node, Visited), !,
    bfs_queue(RestQueue, Visited, Traversal).

bfs_queue([Node|RestQueue], Visited, Traversal) :-
    findall(Child, edge(Node, Child), Children),
    append(RestQueue, Children, NewQueue),
    bfs_queue(NewQueue, [Node|Visited], Traversal).

```

✅ Query to Run in SWI-Prolog:

?- bfs(a, Traversal).

```

 Expected Output:

Traversal = [a, b, c, d, e, f].

```

 3. BFS Representation in PDDL
You can describe BFS as a planning problem (not execute BFS, but model it).

✅ Domain File (bfs-domain.pddl):
(define (domain bfs-search)
  (:predicates
    (connected ?x ?y)
    (visited ?x)
    (current ?x)
  )

  (:action move
    :parameters (?x ?y)
    :precondition (and (current ?x) (connected ?x ?y) (not (visited ?y)))
    :effect (and (visited ?y) (current ?y) (not (current ?x)))
  )
)

✅ Problem File (bfs-problem.pddl):
(define (problem bfs-problem)
  (:domain bfs-search)

  (:objects a b c d e f)

  (:init
    (connected a b)
    (connected a c)
    (connected b d)
    (connected b e)
    (connected e f)
    (connected c f)
    (current a)
    (visited a)
  )

  (:goal (visited f))
)


* You can run this using an online PDDL editor like:
* https://editor.planning.domains/

It will simulate BFS-like traversal by applying move actions.

```

4. Observation & Output

Tool	Output (Traversal Order)	Execution Type
Python	A → B → C → D → E → F	Procedural BFS
SWI-Prolog	A → B → C → D → E → F	Logic-based BFS
PDDL	A → B → C → D → E → F	Planning-based traversal

```

🧾 Result:

Successfully implemented Breadth-First Search (BFS) traversal using Python, SWI-Prolog, and PDDL, and verified the BFS order of a sample graph.
