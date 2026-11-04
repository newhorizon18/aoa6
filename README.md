
# Experiment No. 6 – Bellman-Ford Algorithm

**Created By:** Krish Mhatre

## C Program

```c
#include <stdio.h>
#include <limits.h>

struct Edge {
    int u, v, w;
};

int main() {
    struct Edge e[100];
    int dist[50], V, E, S, i, j;

    printf("Enter number of vertices: ");
    scanf("%d", &V);

    printf("Enter number of edges: ");
    scanf("%d", &E);

    if(V < 1 || V > 50 || E < 0 || E > 100) {
        printf("Invalid graph size");
        return 1;
    }

    printf("Enter source vertex: ");
    scanf("%d", &S);

    if(S < 0 || S >= V) {
        printf("Invalid source vertex");
        return 1;
    }

    printf("Enter edges (source destination weight):\n");
    for(i = 0; i < E; i++) {
        scanf("%d%d%d", &e[i].u, &e[i].v, &e[i].w);

        if(e[i].u < 0 || e[i].u >= V ||
           e[i].v < 0 || e[i].v >= V) {
            printf("Invalid vertex");
            return 1;
        }
    }

    for(i = 0; i < V; i++)
        dist[i] = INT_MAX;

    dist[S] = 0;

    for(i = 1; i < V; i++) {
        for(j = 0; j < E; j++) {
            int u = e[j].u;
            int v = e[j].v;
            int w = e[j].w;

            if(dist[u] != INT_MAX &&
               (long long)dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
            }
        }
    }

    for(j = 0; j < E; j++) {
        int u = e[j].u;
        int v = e[j].v;
        int w = e[j].w;

        if(dist[u] != INT_MAX &&
           (long long)dist[u] + w < dist[v]) {
            printf("Negative weight cycle found!\n");
            return 0;
        }
    }

    printf("\nVertex\tDistance from Source\n");

    for(i = 0; i < V; i++) {
        if(dist[i] == INT_MAX)
            printf("%d\tINF\n", i);
        else
            printf("%d\t%d\n", i, dist[i]);
    }

    return 0;
}
```

## Terminal Input (Copy and Paste)

```text
7
10
0
0 1 6
0 2 5
0 3 5
1 4 -1
2 1 -2
2 4 1
3 2 -2
3 5 -1
4 6 3
5 6 3
```

## Output

```text
PS C:\AOA> gcc bellmanford.c -o bellmanford
PS C:\AOA> .\bellmanford.exe

Enter number of vertices: 7
Enter number of edges: 10
Enter source vertex: 0
Enter edges (source destination weight):
0 1 6
0 2 5
0 3 5
1 4 -1
2 1 -2
2 4 1
3 2 -2
3 5 -1
4 6 3
5 6 3

Vertex    Distance from Source
0         0
1         1
2         3
3         5
4         0
5         4
6         3
```

## Aim
To implement the Bellman-Ford Algorithm using C.

## Theory
Bellman-Ford is a shortest-path algorithm used to find the minimum distance from a source vertex to all other vertices.

It supports negative edge weights and detects reachable negative weight cycles.

## Algorithm
1. Enter the number of vertices and edges.
2. Enter the source vertex.
3. Initialize distances to infinity.
4. Set the source distance to zero.
5. Relax all edges V-1 times.
6. Check for negative weight cycles.
7. Display shortest distances.

## How to Run

Save as `bellmanford.c`.

Compile:

```bash
gcc bellmanford.c -o bellmanford
```

Run:

```powershell
.\bellmanford.exe
```

Paste the input from the Terminal Input section.

## Time Complexity

- Best Case: O(V × E)
- Average Case: O(V × E)
- Worst Case: O(V × E)
- Space Complexity: O(V + E)

## Conclusion
Successfully implemented Bellman-Ford Algorithm in C to find shortest paths from a source vertex.
