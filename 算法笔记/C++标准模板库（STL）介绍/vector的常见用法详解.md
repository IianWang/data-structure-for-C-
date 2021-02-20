# 第六章 C++标准模板库（STL）介绍
## 6.1 vector的常见用法详解
关于使用vector，首先要导入 #include < vector>

**1.定义及访问**

一维：vertor<int/char/double/node> name; //node:结构体，name:自定义变量名

二维：vertor<int/char/double/node> name[size]; //size:每一维的长度

下标访问：vi[i]; i ∈ [0, n]

迭代器访问：vector<typename>::iterator it = vi.begin(); //vi.begin()为首元素**地址**，it指向这个地址

输出： 
```C++
//第一种写法STL通用
vector <int> ls;
for(vector<int>::iterator i = ls.begin(); i != ls.end(); i++){ // 迭代器vector<int>::iterator不支持比大小，所以只能用 !=
    printf("%x", *i); //这里用*获取地址下的值
}

//第二种写法vertor、string特有
vector<int>::iterator it = ls.begin()
for(int i = 0; i < n; i++){
    printf("%x", *(it + i));
}
```
*(it + i) //数组内存连续，i ∈ [0, n]，所以直接加整数即可，因为是地址注意使用"*"取该地址的值

STL容器中，只用在vector、string中才可以用it + i访问每一位（也就是说这个情况下才可以看做内存连续）


**2.常用函数（除了erase其它都无参数）**
- push_back()
- pop_back()
- size()
- clear()
- insert()
eg. v.insert(vi.begin() + 2, -1); 将-1插入vi[2]的位置
- erase() 两种用法
  - vi.erase(v.begin() + 3); 删除单个元素
  - vi.erase(v.begin() + 1, v.begin() + 4); 删除v[1]、v[2]、v[3]（参数遵循左闭右开）


用途：后续更新，主要看看哪种情况使用vertor替代tyname[]更好，达到那种不用会麻烦死的地步


PAT

```C++
//1039 Course List for Student (25 分)
//按科目输入选择该课的学生列表，最后按学生输出该学生选择的所有科目（一个学生可以选多科）
//总结一个思路一个误区
//思路：设置二维数组，hash每个学生的姓名(误区在这里)返回int类型值K，在数组K处添入数字i(课程代号)，最后根据K输出i
//关于数组开多大？hash一节有提到转换阈值根据进制数来定：eg.26进制，26^len - 1。
//关于二维数组，这里的二维数据用的是vector类型，vector自带size，会比较方便读取二维内的元素
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <map>
#include <math.h>
#include <vector>
#define maxn 26 * 26 * 26 * 26

using namespace std;

vector<int> ls[maxn];

int hash_str(char str[]){
    int id = 0;
    for (int i = 0; i < 3; i++) {
        id = id * 26 + str[i] - 'A';
    }
    id = id * 26 + str[3] - '0';
    return id;
}


int main(){
    int N, K;
    scanf("%d %d", &N, &K);
    
    for (int i = 0; i < K; i++) {
        int courses, users;
        scanf("%d %d", &courses, &users);
        for (int j = 0; j < users; j++) {
            char name[10];
            scanf("%s", name);
            ls[hash_str(name)].push_back(courses);
        }
    }
    
    for (int i = 0; i < N; i++) {
        char name[10];
        scanf("%s", name);
        printf("%s %d", name, ls[hash_str(name)].size());
        if (ls[hash_str(name)].size()) {
            sort(ls[hash_str(name)].begin(), ls[hash_str(name)].end());
            for (vector<int>::iterator it = ls[hash_str(name)].begin(); it != ls[hash_str(name)].end(); it++) {
                printf(" %d", *it);
            }
        }
        printf("\n");
    }

    return 0;
};

```

```C++
//1047 Student List for Course (25 分)
//和上一道一样类型，只不过上一道给科目的学生列表，这一道给学生的科目列表
//复习！把这道题按照考试模拟一下
```
