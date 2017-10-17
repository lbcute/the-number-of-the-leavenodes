#include<iostream>
#include<queue>
using namespace std;
typedef struct node//定义一个node结构
{
  char data;
  struct node *leftchild;//node的左右孩子分别是这种结构的指针
  struct node *rightchild;
  
}bintreenode,*bintree;//声明这种结构的对象和指针，指针用于下面申请新的对象内存
//利用前序遍历的方法创建树
void createbintree(bintree &T)//参数是struct的指针
{
  char c;
  cin>>c;
  if(c=='#')
    T=NULL;//如果输入为#,则说明这个地方不是结点了，指针域赋值为空
  else
  {
    T=new bintreenode;//如果输入的数据符合要求，则用指针申请内存
    T->data=c;
    createbintree(T->leftchild);//递归创建左子树
    createbintree(T->rightchild);//递归创建右子树，根据堆栈的原理只有左子树都创建好了才会创建右子树
  }
}

int count=0;//count用于统计叶子结点的数目
int leavenumber(bintree root)
{
  
  if(root==NULL)
  {
    return count;//如果是空树，返回0
  }
  else
  {
    queue<bintree>que;//que为队列
    que.push(root);//先让根结点入队
  
    while(!que.empty())//队列不为零则进行循环
    {
      root=que.front();//root表示队列的第一个元素
      if(root->leftchild == NULL&&root->rightchild == NULL)
	count++;//如果这个结点的左右孩子都是空的，则为叶子结点，将count加1
      que.pop();//从队列删除
      if(root->leftchild!=NULL)
      {
	que.push(root->leftchild);//左孩子入队

      }
      if(root->rightchild!=NULL)
      {
	que.push(root->rightchild);//右孩子入队
	
      }
    }
    return count;//返回叶子数
  }
  
}
int main()
{
  bintree q;
  cout<<"请按前序遍历的方式输入一棵树："<<endl;
  cout<<"比如：输入一棵只有两层的树，第一层为a,第二层为b,c;则应这样输入：ab##c##然后按enter结束即可"<<endl;
  createbintree(q);
  cout<<"这棵树的叶子结点数目是："<<endl;
  cout<<leavenumber(q)<<endl;
 
}











