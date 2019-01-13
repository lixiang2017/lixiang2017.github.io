---
title: Floyd
date: 2018-12-15 23:55:33
categories:
tags:
---
###### 问题描述
求无向图中各点之间的最短路径长度和对应的最短路径。如果有多条最短路径，给出一条即可。
![](floyd.png)
```c
#include <stdio.h>
#define MAXV 100 

int D[MAXV][MAXV] = {0};
int min_path[MAXV][MAXV] = {0};

void Floyd(int A[MAXV][MAXV], int n)
{
    int i, j, k;
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
        {
            min_path[i][j] = -1;
            if(i == j)
            {
                D[i][j] = 0;
                continue;
            }
            if(A[i][j])
            {
                D[i][j] = A[i][j];
            }
            else
            {
                D[i][j] = 99;   // a very large number, more than any of A[i][j]
            }
            
        }

    for (k = 0; k < n; k++)
    {
        for (i = 0; i < n; i++)
            for (j = 0; j < n; j++)
                if (D[i][j] > (D[i][k] + D[k][j]))
                {
                    D[i][j] = D[i][k] + D[k][j];
                    min_path[i][j] = k;
                }
    }
}

// print shortest path from i to j
void print_shortest_path(int i, int j)
{
    printf("shortest path from %d to %d is  ", i, j);
    printf("%d ->", i);
    while(min_path[i][j] != -1)
    {
        printf(" %d ->", min_path[i][j]);
        i = min_path[i][j];
    }
    printf(" %d\n", j);
}

int main()
{
    int n = 7;
    int A[MAXV][MAXV] = {
        {0, 1, 0, 1, 1, 0, 0},
        {1, 0, 1, 1, 0, 0, 0},
        {0, 1, 0, 1, 1, 0, 0},
        {1, 1, 1, 0, 1, 0, 0},
        {1, 0, 1, 1, 0, 1, 0},
        {0, 0, 0, 0, 1, 0, 1},
        {0, 0, 0, 0, 0, 1, 0}
        };

    // shortest path
    Floyd(A, n);
    int a = 2;
    int b = 6;
    printf("shortest path length from %d to %d is %d\n", a, b, D[a][b]);
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {
            printf("shortest path length from %d to %d is %d\n", i, j, D[i][j]);        
            // print_shortest_path(i, j);
        }
    }

    return 0;
}
```
![](floyd_1.png)
![](floyd_2.png)
