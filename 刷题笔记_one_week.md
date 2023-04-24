# 01.数组中重复的数字

## 描述：在一个长度为n的数组里的所有数字都在0到n-1的范围内。数组中某些数字是重复的，但不知道有几个数字重复，也不知道每个数组重复几次，请找出数组中任意一个重复的数字。

### 1.第一种方法

```c++
int dupblicate(vector<int> &nums)

{
	sort(nums.begin(),nums.end())
	for(int i=0;i<nums.size();i++)
	{
		if(nums[i]==nums[i+1])
		return nums[i];
	}
	return -1;
}
```

### 2.第二种方法

```C++
int dupblicate(vector<int>&nums)
{
    set<int>s;
    for(int i=0;i<nums.size();i++)
    {
        if(s.find(nums[i])==s.end())
            s.insert(nums[i]);
        else
            return nums[i];
	}
    return -1;

```

### 3.第三种方法

```C++
int dupblicate(vector<int>&nums)
{
	for(int i=0;i<nums.size();i++)
    {
        while(nums[i] !=i)
        {
            if(nums[i]==nums[nums[i]])
                return nums[i];
            else
                swap(nums[i],nums[nums[i]]);
        }
    }
    return -1;
}
```

```python
class Solution:
    def findRepeatNumber(self,nums:List[int])->int:
        for i,num in enumerate(nums):
            while nums[i]!=i:
                m=nums[i]
                if nums[m]==m:
                    return m
                else:
                    nums[i]=nums[m]
                    nums[m]=m
        return -1
```



# 02.二维数组中的查找

## 描述：在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增，请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

###  1.第一种方法

```c++
bool Find(int target,vector<vector<int>>arr)//创建一个二维数组
{
    if(arr,empty() || arr[0].empty())
        return false;
    int i=0,j=arr[0].size()-1;
    while(i<=arr.size()-1 && j>=0)
    {
        if(target==arr[i][j])
            return true;
        else if(target>arr[i][j])
            i++;
        else(target<arr[i][j])
            j--;
	}
    return false;
}
```

# 03.替换空格--（不会）

## 请实现一个函数，将一个字符中的每个空格替换成%20.

### 1.第一种方法

```c++
class Solution
{
public:
    string replaceSpace(string s)
    {
        if(s.empty())
            return s;
        int count=0;
        for(auto i:s)
            if(i==' ')
                count++;
        s.resize(s.length()+count*2,0);
        for(int i=s.length()-1;i>=0;i--)
        {
            if(s[i]!=' ')
                s[i+count*2]=s[i];
            if(s[i]==' ')
                count--;
            	s[i+count*2]="%";
            	s[i+count*2]="2";
            	s[i+count*2]="0";
        }
        return s;
	}
};
```

### 2.第二种方法

```c++
class Solution
{
public:
    string replaceSpace(string s)
    {
 		string res;
        for(auto i:s)
            if(i==' ')
                res +='%20';
        	else
                res+=x;
        return res;
	}
};
```

# 04.从尾到头打印链表

## 描述：输入一个链表头节点，按照从尾到头的顺序返回节点的值

### 1.第一种方法

```c++
class Solution{
public:
    vector<int>printListReversingly(ListNode*head){
        vector<int>res;
        ListNode*p=head;
        while(p!=NULL){
            res.push_back(p->val);
            p=p->next;
        }
        return vector(res.rbegin(),res.rend());//倒序
    }
};
```

### 3.第二种方法

```c++
class Solution{
public:
    vector<int>printListReversingly(ListNode*head){
        vector<int>res;
        ListNode*p=head;
		stack<int>stk;
        
        while(p!=NULL)
        {
            stk.push(p->val);
            p =p->next;
        }
        int len=stk.size();//将元素压入栈底
        for(int i=0;i<len;i++)
        {
            res.push_back(stk.top());//取栈顶元素
            stk.pop();//弹出栈顶元素
        }
        return res;
    }
};
```

# 05.重建二叉树

## 描述：输入某个二叉树的前序遍历和中序遍历的结果，请重建二叉树。

二叉树的四种遍历方法：前序遍历：根节点——左子树——右子树

​											中序遍历：左子树——根节点——右子树

​											后序遍历：左子树——右子树——根节点

​											层次遍历：只需按层次遍历即可

### 1.第一种方法

```c++
class Solution{
    public:
    map<int,int>hash;//创建一个哈希表
    vector<int>preorder,inorder;
    
    TreeNode*bulidTree(vector<int>& _preorder,vector<int>& _inorder){
        preorder=_preorder,inorder=_inorder;
        for(int i=0;i<inorder.size();i++)//这是中序遍历的
            hash[inorder[i]]=i;
        return dfs(0,preorder.size()-1,0,inorder.size()-1);//深度优先搜索 递归
    }
    TreeNode*dfs(int pl,int pr, int il,int ir){
        if(pl>pr)
            return NULL;
        auto root=new TreeNode(preorder[pl]);//找根节点
        int k=hash[root->val];//左子树的长度
        auto left=dfs(pl+1,pl+k-il,il,k-1);//左右递归遍历
        auto right=dfs(pl+k-l+1,pr,k+1,ir);
        root->left=left,root->right=right;
        return root;
    }
};
```

### 2.第二种方法

```c++
class Solution{
public:
	unordered_map<int,int>pos;
    TreeNode*bulidTree(vector<int>pre,vector<int>vin)
    {
        int n=vin.size();
        for(int i=0;i<n;i++)
            pos[vin[i]]=i;//记录中序序列的位置信息
        return dfs(pre,vin,0,n-1,0,n-1);
    }
    TreeNode*dfs(vector<int>pre,vector<int>vin,int pl,int pr,int vl,int vr)
    {
        if(pl>pr)
            return NULL;
        TreeNode*root=new TreeNode(pre[pl]);//找根节点，前序遍历的首位
        int k=pos[pre[pl]]-vl;//左子树的长度
        root->left=dfs(pre,vin,pl+1,pl+k,vl,vl+k-1);
        root->right=dfs(pre,vin,lp+k+1,pr,vl+k+1,vr);
        
        return root;
    }
};
```

# 06.二叉树的下一个节点

## 描述：给定一个二叉树和其他的一个节点，找出中序遍历顺序的下一个节点并返回。注意，树中的节点不仅包含左右结点，同时包含指向父节点的指针

### 1.第一种方法(分情况讨论)

```c++
class Solution{
    public:
    TreeLinkNode*GetNext(TreeLinkNode*p){
        //右子树存在，右子树最左边的节点
        if(p->right)
        {
            p=p->right;
            while(p->left)
                p=p->left;
            return p;
        }
        //右子树不存在，只有左子树
        while(p->next)
            //p不是根节点
            if(p==p->next->right)
                return p->next;
        	p=p->next;
    }
    return NULL;  
}
```

# 07.两个栈实现队列

###  1.第一种方法

```c++
class MyQueue{
public:
    /*Initialize your data structure here.*/
    stack<int>stk,cache;
    MyQueue(){
        
    }
    /*Push element x to the back of queue.*/
    void push(int x){
        stk.push(x);
	}
    
    void copy(stack<int>&a,stack<int>&b){
        while(a.size()){
            b.push(a.top());
            a.pop();
		}
    }
    /*removes the element from in front of queue and returns taht element*/
    int pop(){
        copy(stk,cache);
        int res=cache.top();
        cache.pop();
        copy(cache,stk);
        return res;
    }
    
    /*get the front element*/
    int peek(){
        copy(stk,cache);
        int res=cache.top();
        copy(cache,stk);
        return res;
	}
    /*returns whether the queue is empty*/
    bool empty()
    {
        return stk.empty();
    }
}
```

### 2.第二种方法(和第一种方法一样)

```c++
class Solution{
public:
    void push(int node)
    {
        stack1.push(node);
    }
    
    void copy(stack<int>&a,stack<int>&b){
        
        while(a.size()){
            b.push(a.top());
            a.pop();
		}
    } 
    int pop(){
        copy(stack1,stack2);
        int res=stack2.top();
        stack2.pop();
        copy(stack2,stack1);
        return res;
    }
    
private:
    stack<int>stack1;//定义两个栈容器
    stack<int>stack2;
};
```

