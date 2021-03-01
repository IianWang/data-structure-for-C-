# 第六章 C++标准模板库（STL）介绍
## 6.3 string的常见用法详解
关于使用string，首先要导入 #include < string>
using namespace std;


**string.c_str() 真的很好用，任何只接受char[]类型的函数，string都可以调用c_str()来传入，解决格式问题。**


**1.定义及访问**
string str;
string str = "abcd";

读入需要用cin
输出cout，如果是printf则变量后加.c_str()。

(1) 通过下标访问：str[i]

(2) 通过迭代器方便（有些情况如insert()、erase()函数是要求迭代器为参数，所以涉及到这两者则需要用迭代器）



**2.常用函数**
- operator+=（字符串合并直接相加） str1 + str2
- compare operator（字符串直接比大小）规则是字典序
- length()/size() 
- insert() 有多种写法
  - insert(pos, string)，在pos位置插入**字符串string**
  - insert(it, it2, it3)，it 欲在原字符串插入的位置，it2、it3为待插字符串的首位迭代器
- erase()
  - erase(it)，it为欲删除元素的迭代器
  - erase(first, last)，需要删除区间的迭代器
  - erase(pos, length)，位置和删除的字符个数
- clear()
- substr(pos, len)返回从pos位置开始，长度为len的字符串
- string::npos
- find(str2) str2是str的子串，返回其在str中第一次出现的位置，如果不是则返回string::npos（可以认为是-1）
- find(str2, pos)从pos位置开始匹配str2
- replace()
  - replace(pos, len, str2)，从pos开始，长度为len的字符串替换为str2
  - replace(it1, it2, str2)，[it1, it2)迭代器范围的字符串替换为str2
  
  
PAT
```C++
//1060 Are They Equal (25 分)
//重做！书上的解
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

int n;
string deal(string s, int &e){
    int k = 0; //s 的下标
    while (s.length() > 0 && s[0] == '0') {
        s.erase(); //去掉s前面的前导零
    }
    if(s[0] == '.'){
        s.erase(s.begin());
        while (s.length() > 0 && s[0] == '0') {
            s.erase(s.begin());
            e--;
        }
    }
    else{
        while (k < s.length() && s[k] != '.') {
            k++;
            e++;
        }
        if (k < s.length()) {
            s.erase(s.begin() + k);
        }
    }
    if (s.length() == 0) {
        e = 0;
    }
    int num = 0;
    k = 0;
    string res;
    while (num < n) {
        if (k < s.length()) {
            res += s[k++];
        }
        else res += '0';
        num++;
    }
    return res;
}


int main(){
    string s1, s2, s3, s4;
    cin >> n >> s1 >> s2;
    int e1 = 0, e2 = 0;
    s3 = deal(s1, e1);
    s4 = deal(s2, e2);
    if (s3 == s4 && e1 == e2) {
        cout << "YES 0." << s3 << "*10^"<<e1<<endl;
    }
    else cout << "NO 0." << s3 << "*10^" << e1 << " 0." << s4 << "*10^" << e2 << endl;
    
    
    return 0;
};

  ```
