# 第六章 C++标准模板库（STL）介绍
## 6.1 set的常见用法详解
关于使用set，首先要导入 #include < set>


PAT
```C++
//1063 Set Similarity (25 分)
//一个5分数据点报超时，确实遍历两个集合的元素插入到新集合有点耗时
//如果遍历一个集合的元素到另外一个集合查找，复杂度可以减至一半
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <map>
#include <math.h>
#include <vector>
#include <set>
#define maxn 100100

using namespace std;



int main(){
    int N;
    scanf("%d", &N);
    set<int> ls[maxn];
    set<int> tot;
    for (int i = 0; i < N; i++) {
        int temp;
        scanf("%d", &temp);
        for (int j = 0; j < temp; j++) {
            int ele;
            scanf("%d", &ele);
            ls[i].insert(ele);
        }
//        printf("size = %d\n", ls[i].size());
    }
    int M;
    scanf("%d", &M);
    for (int i = 0; i < M; i++) {
        tot.clear();
        int a, b;
        scanf("%d %d", &a, &b);
        a--;
        b--;
        for (set<int>::iterator it = ls[a].begin(); it != ls[a].end(); it++) {
            tot.insert(*it);
        }
        for (set<int>::iterator it = ls[b].begin(); it != ls[b].end(); it++) {
            tot.insert(*it);
        }
        
        printf("%.1lf", abs((int)ls[a].size() + (int)ls[b].size() - (int)tot.size()) * 1.0 * 100.0 / tot.size() * 1.0);
        printf("%%\n");
    }
    
    return 0;
};

```
