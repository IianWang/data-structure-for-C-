# 二叉树遍历的应用
## 递归前序方式生成二叉树
```C++
struct node{
    char data;
    node* left;
    node* right;
}binary_tree,*tree;

void CreatePer(node* &tree){//此处需要加引用，不加不会报错但什么也不会输出
    char temp;
    scanf("%c", &temp);
    if(temp == '#'){
        tree = NULL;
    }
    else{
        tree = new node;//这里如果再次node* tree相当于覆盖掉了形参上声明的那个tree
        tree -> data = temp;
        //每次调用自身的时候会在形参中声明好新的临时变量tree，无需在函数内部再次声明
        //只需要在函数内部给这个临时变量分配内存即可，
        CreatePer(tree -> left);
        CreatePer(tree -> right);
    }
}

void travelPre(node* tree){
    if(tree == NULL){
        return;
    }
    else{
        printf("%c\n", tree -> data);
        travlPre(tree -> left);
        travlPre(tree -> right);
    }
}

int main(){
    CreatePer(tree);
    travelPre(tree);
};
```
