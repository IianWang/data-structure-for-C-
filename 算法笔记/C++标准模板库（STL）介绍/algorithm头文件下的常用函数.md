# 第六章 C++标准模板库（STL）介绍
## 6.9 algorithm头文件下的常用函数
关于使用map，首先要导入 #include < algorithm>
using namespace std;

- max(x, y)
- min(x, y)
- abs(x) x必须得为整数，浮点数用fabs()
- swap(x, y) 交换x, y的值
- reverse(it1, it2) eg. reverse(a, a + len)把长度为len的数组进行反转，也可以作用于迭代器(iterator)
- next_permutation() 每执行一次都输出下一个排列样式
```C++
int ls[5] = {1, 2, 3};
do{
    printf("%d %d %d\n", ls[0], ls[1], ls[2]);
}while(next_permutation(ls, ls + 3));

//output
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```
- fill() 
```C++
int ls[5] = {1, 2, 3};
fill(ls, ls + 3, 0);
for(int i = 0; i < 3; i++){
    printf("%d\n", ls[i]);
}

//output
0
0
0
```
- sort() 不用多说了，常用，sort还可以针对容器排序
eg.sort(vi.begin, vi.end(), cmp)

顺便一提，sort()对字符串排序，是根据首字母的字典序大小排列的，比如"aaaaa"和"z"，依然认定"z"比"aaaaa"大

- lower_bound(first, last, val) 第一个大于等于val的位置
- upper_bound(first, last, val) 第一个大于val的位置(与上面的相比就是考虑到会有许多并列的元素)
- 
这两个之前在二分查找(4.5.1)讲过，前提是数组/容器有序，不断的找mod中点，将left或right移动到中点处附近，直到找到想要的元素，找不到最终就会停留在该元素应该出现的位置
