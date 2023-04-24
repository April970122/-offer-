# 01.斐波那契数列

## 描述：输入一个整数n，求斐波那契数列的第n项

### 1.第一种方法（暴力算法）

```c++
class Solution{
public:
    int Fibonacci(int n){
		int a=0,b=1;
        while(n--)
        {
            int c=a+b;
            a=b;
            b=c;
        }
        return a;
    }
};
```

```c++
class Solution{
public:
    int Fibonacci(int n){
		if(n==0) return 0;
        if(n==1) return 1;
        
        int a=0,b=1;
        for(int i=2;i<=n;i++)
        {
            int c=a+b;
            a=b;
            b=c;
        }
        return c;
    }
};
```

# 02.旋转数组的最小数字

## 描述：把一个数组最开始的若干元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。

### 1.第一种方法

```c++
class Sulotion{
public:
    int minNumberInRotateArray(vector<int>rotateArray)
    {
        int n = rotateArray.size()-1;//计算数组大小
        if(n<0)//数组大小为零则返回0
            return -1;
        
        while(rotateArray[n]==rorateArray[0]&&n>0) n--;//把重复的数字去掉，方便二分
        if(rorateArray[n]>=rorateArray[0]) return rorateArray[0];
        
        int l=0,r=n;//定义左右边界
        while(l<r)
        {
            int mid=l+r>>1;//l+r的值右移一位，相当于l+r的值除以2向下取整  [l,mid] [mid+1,r]
            if(rorateArray[mid]<rorateArray[0]) r=mid;
            else l=mid+1;
        }
        return rorateArray[r]
        
    }
};
```

# 03.矩阵的路径(不懂)

## 描述：设计一个函数，用来判断在一个矩阵中是否存在某字符串多有字符的路径。路径可以从矩阵中任意一个格子开始，每一步在矩阵中向左，向右，向下，向上移动一个格子。如果一条路径经过矩阵中的某一个格子，则之后不能再次进入这个格子。

### 1.第一种方法

```c++
class Solution{
public:
    bool hasPath(vector<vector<char>>&matrix,string str)
    {
        for(int i=0;i<matrix.size();i++)
            for(int j=0;j<matrix[i].size();j++)
                if(dfs(mtrix,str,0,i,j))
                    return ture;
        return false;
    }
    
    bool dfs(vector<vector<char>>&matrix,string &str,int u,int x,int y)//u:枚举的长度；x,y：枚举的起点和终点
    {
        if(u==str.size()) return true;
        if(matrix[x][y]!=str[u]) return false;
        int dx[4]={-1,0,1,0},dy{0,1,0,-1};//坐标遍历。左：（-1，0），右：（1，0），上（0，1），下：（0，-1）
        char t=matrix[x][y];
        matrix[a][b]='*';
        for(int i=0;i<4;i++)
        {
            int a=x+dx[i],b=y+dy[i];
            if(a>0&&a<matrix.size()&&b>=0&&b<matrix[0].size()&&matrix[a][b]==str[u])
            {
                if(dfs(matrix,str,u+1,a,b))  return true;  
            }
		}
         matrix[x][y]=t;
        return false;
	}
};  
```

### 2.第二种方法

```c++
class Solution{
public:
    bool hasPath(char*matrix,int rows,int cols,char*str)
    {
        for(int i=0;i<rows;i++)
            for(int j=0;j<cols;j++)
                if(dfs(matrix,rows,cols,str,0,i,j))
                    return true;
        return false;
    }
    
    bool dfs(char*matrix,int rows,int cols,char*str,int u,int x,int y)
    {
        if(str[u]=='\0') return true;
        
        int dx[4]={-1,0,1,0},dy{0,1,0,-1};//坐标遍历。左：（-1，0），右：（1，0），上（0，1），下：（0，-1）
        for(int i=0;i<4;i++)
        {
            int a=x+dx[i],b=y+dy[i];
            if(a>0&&a<rows&&b>=0&&b<cols&&matrix[a*cols+b]==str[u])
            {
                char t=matrix[a*cols+b];
                matrix[a*cols+b]='*';
                if(dfs(matrix,roes,cols,str,u+1,a,b))  
                    return true; 
                matrix[a*cols+b]=t;
            }
        }
        return false;
	}
};  
```

# 04.机器人的运动范围

## 描述：地上有一个m行和n行的方格子，横纵坐标范围分别是0~m-1和0 ~n-1。一个机器人从坐标0，0的格子开始移动，每一次只能向左右上下四个方向移动一格，但是不能进入横坐标和列坐标之和大于k的格子。

### 1.第一种方法

```c++
class Solution{
public:
    
    int get_single_sum(int x){
        int s=0;
        while(x)
            s+=x%10,x/=10;
        return s;
        
    }
    
    int get_sum(pair<int,int>p){
        return get,single_sum(p.first)+get_single_sum(p.second);
    }
    
    int movingCount(int threshold,int rows,int cols)
    {
        int res=0;
        if(!rows||!cols)
            return 0;
        
        vector<vector<bool>>st(rows,vector<bool>(cols));
        queue<pair<int,int>>q;
        
        q.push({0,0});
        
        int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
        
        while(q.size())
        {
            auto t=q.frount();
            q.pop();
            
            if(get_sum(t)>threshold || st[t.first][t,second]) continue;
            
            res++;
            st[t.first][t,second]=true;
            
            for(int i=0;i<4;i++)
            {
                int x=t,first+dx[i],y=t,second+dy[i];
                if(x>=0&&x<rows&&y>=0&&y<cols)
                {
                    q.push({x,y});
				}
            }
        }
        
        return res;
	}
};
```

