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
