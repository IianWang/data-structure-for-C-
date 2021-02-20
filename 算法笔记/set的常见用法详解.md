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

