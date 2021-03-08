# 第六章 C++标准模板库（STL）介绍
## 6.1 set的常见用法详解
关于使用set，首先要导入 #include < set>
using namespace std;

**1.定义及访问**
一维：set<int/char/double/node> name; //node:结构体，name:自定义变量名

二维：set<int/char/double/node> name[size]; //size:每一维的长度

不支持下标直接访问，只能it++枚举

**2.常用函数（除了erase其它都无参数）**
- insert(x)
- find(x)
- erase()两种方法
  - erase(x)//删除元素x
  - erase(x, st.end())//删除元素x至set末尾的元素
- size()
- clear()

**3.set的常见用途**

主要：自动去重并升序排序，省了常规的hash去重然后调用sort


PAT
```C++
//1063 Set Similarity (25 分)
//一个5分数据点报超时，确实遍历两个集合的元素插入到新集合有点耗时
//如果遍历一个集合的元素到另外一个集合查找，复杂度可以减至一半
//代码待修改
//复习

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

//二刷，set集合直接可以复制给另一个set变量，所以这块的复杂度就省了，另一个就是计算交集和并集了
//并集：设置一个临时set temp，将set a复制给 temp，遍历set b insert到 temp内，最后temp的长度即a、b的并集
//交集：交集可以通过公式计算得出a.size() - (temp.size() - b.size())即为交集的个数
//输出%字符，只需再加一个%即可
#include <iostream>
#include<bits/stdc++.h>
const double eps = 1e-8;
const double odds = 0.65;
#define Equ(a, b) (fabs((a) - (b))<(eps))
#define Cpa(a, b) ((a) > (b))
#define maxn 51
const int INF = 100000000;
using namespace std;
set<int> ls[maxn];

int main()
{
    int N;
    scanf("%d", &N);
    for(int i = 1; i <= N; i++){
        int a;
        scanf("%d", &a);
        for(int j = 0; j < a; j++){
            int b;
            scanf("%d", &b);
            ls[i].insert(b);
        }
    }
    int M, x, y;
    scanf("%d", &M);
    for(int i = 0; i < M; i++){
        scanf("%d %d", &x, &y);
        set<int> temp;
        temp = ls[y];
        for(set<int>::iterator it = ls[x].begin(); it != ls[x].end(); it++){
            temp.insert(*it);
        }
        double up, down;
        down = temp.size();
        up = ls[x].size() - (temp.size() - ls[y].size());
        printf("%.1lf", up * 100.0 / down);
        printf("%%");
        printf("\n");
    }

    return 0;
}

```
