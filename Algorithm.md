# 算法笔记

## 第1章 如何使用本书

1. 常见OJ

   PAT、codeup、POJ、CodeForce

2. 评测结果

   AC：答案正确

   CE：编译错误

   WA：答案错误（代码漏洞、算法错误）

   TLE：超时

   RE：运行错误（段错误：非法访问内存、数组越界）、浮点错误（除数、模数为0）、递归爆栈

   MLE：内存超限

   PE：格式错误（最接近AC的错误，因为多输出了空格或换行导致）

   OLE：输出超限（输出了过多内容）

## 第2章 C/C++快速入门

### 技巧

1. cin和cout消耗的时间比scanf和printf多得多
2. stdio.h更推荐使用等价写法：cstdio

***

### 基本数据类型

1. **变量名**的第一个字符必须是字母或下划线，除第一个字符外的其他字符必须是**字母、下划线、数字**。

4. long long赋大于2^31-1的初值，则需要在初值后面加上LL

   ```C++
   long long bignum=123456789012345LL;
   ```

5. 对于整型数据，都可以在前面加个unsigned，表示无符号型（非负）

6. 题目要求10^9以内或者说32位整数，用int型

   ​               10^18以内或者说64位整数，用long long型

   ​                                           浮点型数据，用double来存储（不用float）

4. 小写字母比大写字母的ASCII码值大32。

5. 不能把字符串常量赋值给字符变量 `char c=”abcd”`错误

6. **常量**推荐const写法 `const double pi=3.14`

7. 除数如果是0，会导致程序异常退出，或是得到错误输出“1.#INF00”

8. 位运算符，int型上限2^31-1程序中把无穷大的数INF可以设置成(1<<31)

   ```c++
   const int INF=(1<<30)-1;  //在main函数外定义
   ```

9. 如果要输入“3 4”这种用空格隔开的两个数字，两个%d之间可以不加空格

   ```C++
   int a,b;
   scanf("%d%d",&a,&b);
   ```

   可以不加空格的原因是，除了%c外，scanf对其他格式符(如%d)的输入是以空白符（即空格、换行等）为结束判断标志的，因此除非使用%c把空格按字符读入，其他情况都会自动跳过空格。另外字符数组使用%s读入的时候以空格跟换行为读入结束的标志。

10. I/O

|                  | Input | Out  |
| :--------------: | :---: | :--: |
|       int        |  %d   |  %d  |
|    long long     | %lld  | %lld |
|      float       |  %f   |  %f  |
|      double      |  %lf  |  %f  |
|       char       |  %c   |  %c  |
| string/char数组  |  %s   |  %s  |
| 十六进制形式整数 |  %x   |  %x  |

3. 基本数据类型

![1556542505781](pic/1556598712864.png)

15. 输出格式 

  * %.1f  保留1位小数输出
  * %.nf  输出浮点数，精确到小数点后n位
  * %5d   不足五位 前方用空格填充
  * %05d  不足五位 前方用0填充  
  * %nd   以n字符宽度输出整数，宽度不足时用空格填充 
  *  %0nd  以n字符宽度输出整数，宽度不足时用0填充

16. 强制类型转换 `(int)r (double)a`

17. 字符型数据与整型数据互相转换

    ```C++
    int k = 'a' ;  //k内容变为'a'的ASCII码，即97 
    printf("%d",k) ;    //输出：97	
    
    int n = 98; 
    char k = n ;   //k内容变98,98是字符'b'的ASCII码 
    printf("%c",k) ;    //输出：b
    ```

18. ASCII码值

![1556542625921](pic/1556598744782.png)

19. 转义字符

![1556542638660](pic/1556598738792.png)

20. typedef 起名 

    ```C++
    typedef long long LL;
    typedef unsigned int uint;
    ```

21. 如果表达式是“！=0”，则可以忽略“！=0”
    如果表达式是“==0”，则可以忽略“==0”，并在表达式前添加非运算符“！”

    ```C++
    if(n)   if(n!=0)
    if(!n)  if(n==0)
    ```

22. case不用加大括号

    ```C++
    switch(rank){
            case'A':printf("A(90~100)\n");break;
            case'B':printf("B(80~89)\n");break;
            case'C':printf("C(70~79)\n");break;
            case'D':printf("D(60~69)\n");break;
            case'E':printf("E(0~59)\n");break;
            default:printf("error!\n");break;
    }
    ```

26. break直接跳出循环体，不再循环，但不退出if语句

    continue直接跳出当前循环层，进入下一层，不跳出循环体，继续循环。

***

### 数组

1. **数组**是由地址上连续的若干个相同类型的数据组合而成

2. 定义size的一维数组，只能访问下表0~size-1的元素

    ```C++
    int a[10]={0,1,2,3,4,5,6,7,8,9};
    ```

3. 二维数组 对定义为`int a[size1][size2]`的二维数组，其一维的下标取值只能是0~（size1-1）的元素；其二维的下标取值只能是0~（size2-1）的元素

    ```C++
    int a[5][6]={{3，1，2}，{8，4}，{}，{1，2，3，4，5}};
    ```

    除去这些被赋初值的元素之外的其他部分默认为0。

4. 如果数组大小比较大（10^6级别），需要定义到主函数外面，原因时函数内部申请的**局部变量**来自**系统栈**，允许申请的空间较小；而函数外部申请的**全局变量**来自**静态存储区**，允许申请的空间较大。

5. 多维数组

    ```c++
    int a[3][3][3]={ {{1,4,5},{},{2,6}} , {{},{},{}} , {{},{},{}} }
    ```

6. 字符数组

    ```c++
    char str[15]={‘G’，‘o’，‘o’，‘d’，‘,’，‘s’，‘t’，‘o’，‘r’，‘y’};  
    ```

    还可以直接赋值字符串（仅限于初始化，其他位置不允许）

    ```c++
    char str[15]=“Good Story!“;  
    ```

7. 字符数组的输入输出

    ```c++
    char str[10];
    scanf(“%s”,str);   //TAT TAT TAT   不需要&
    printf(“%s”,str);  //TAT
    //%s识别空格作为字符串的结尾（换行也是），因此后两个TAT不会被读入
    ```

    ```c++
    str[i]=getchar();  //输入单个字符
    putchar(str[i]);
    ```

    ```c++
    gets(str);    //输入字符串
    puts(str);    //输出字符串
    //识别换行\n作为输入结束
    ```

8. gets或scanf输入字符串时自动加\0,占用一个字符位

    puts和printf输出通过识别\0,作为结尾输出

9. 开字符数组时，长度至少比实际字符串长度多1

10. 字典序：两字符数组中第一个不同的字符的ascii码比较

***

### 函数

1. **全局变量**-定义在函数前

    **局部变量**-定义在函数内，只在函数内部生效，函数结束时局部变量销毁

2. 函数定义小括号内的参数-**形式参数**

    实际调用时小括号内的参数-**实际参数**

3. 数组作为参数第一维不需要写长度，需要[]，数组作为参数时，函数内直接修改其本身，但不允许返回数组

    ```c++
    void change(int a[],int b[][5]){}
    
    change(a,b);//a,b为数组
    ```

***

### 指针

1. **指针**指向内存地址，变量前加&，就表示变量的地址

2. 指针是一个unsigned类型的整数

3. **指针变量**用来存放指针

   ```C++
   int* p1,p2; //p1是指针（int*）变量，p2是int变量
   int *p1,*p2,*p3; //都是指针变量
   double *p1;
   char *p1;
   //int double char为指针的基类型
   ```

   指针变量赋值：将变量（a）的地址取出来，然后赋给相应的指针变量（p）

   ```C++
   int a;      
   int* p=&a;  
   //////////////////////
   int a;
   int* p;
   p=&a;	//不是  *p=&a;   赋值给p，而不是*p 
   ```

   取值*p， *放在p前，相当于钥匙，打开了地址所存的值

4. `p+1`是指`p`所指的`int`变量的下一个`int`型变量地址

5. 数组名称可以作为数组的首地址使用

   ```C++
   a == &a[0]
   //可得
   a+i == &a[i] 
   
   * a+i == a[i]
   
   scanf("%d", a+i);
   printf("%d", *(a+i));
   ```

6. 指针类型可以作为函数参数的类型，视为把变量的地址传入函数，如果在函数中对这个地址中元素进行改变，原先的数据确实会变

7. 引用（暂不涉及）

***

### 结构体

1. 结构体实例

   studentInfo为结构体的类型名，内部定义id、gender、name、major信息，大括号外定义Alice和Bob代表两个结构体变量，stu[1000]为结构体数组。

   ```C++
   struct studentInfo{
       int id;
       char gender;
       char name[20];
       char major[20];
   }Alice,Bob,stu[1000];  //直接定义
   
   studentInfo Alice；    //第二种定义方式
   studentInfo stu[1000]；
   ```

   结构体里面定义除了自己本身之外的任何数据类型，可以定义自身类型的指针变量

   ```c++
   struct node{
       node n;      //error
       node* next;  //success
   }
   ```

2. 访问结构体元素 . 和 ->

   ```C++
   struct studentInfo{
       int id;
       char name[20];
       studentInfo* next;   //多了一个指针next用来指向下一个学生的地址，
   }stu，*p;				//普通变量 指针变量
   
   ```

   ```C++
stu.id
   stu.name
   stu.next

   (*p).id         p->id    //只有指针才可以用.
   (*p).name		p->name
   (*p).next		p->next
   ```
   
3. 结构体的初始化

   ```C++
   stu.id=1;  //普通初始化方法
   scanf("%d",&stu.id);
   ```

   默认生成的构造函数初始化

   ```C++
   struct studentInfo{
       int id;
       char gender;
       //默认生成的构造函数
       studentInfo(){}
   };				
   
   ///////////////////初始化参数并赋值
   struct studentInfo{
    int id;
       char gender;
       //对结构体内部变量赋值
       studentInfo(int _id, char _gender){
           //赋值
           id = _id;
           gender = _gender;
       }
   };	
   
   studentInfo stu = studentInfo(10086,'M');//创建结构体stu并赋值
   
   
   struct studentInfo{
       int id;
       char gender;
       //用以不初始化就定义结构体变量
       studentInfo(){}
       //只初始化gender
       studentInfo(char _gender){
           gender = _gender;
       }
       //同时初始化id、gender
       studentInfo(int _id, char _gender){
           //赋值
           id = _id;
           gender = _gender;
       }
   };	
   ```
   

***

### 补充

1. cin、cout

   ```C++
   #include<iostream>
   using namespace std;
   cin>>n;//输入n
   cin>>n>>db>>c>>str;
   char str[100];
   cin.getline(str,100);//整行读入char型数组
   string str;
   getline(cin,str);//整行读入string型数组
   
   ```

   ```C++
   cout<<n<<""<<db<<"\n"<<c<<str<<endl; //""空格 "\n"换行 endl换行
   
   #include<iomanip>//控制精度
   cout << setiosflags(ios::fixed)<<setprecision(2)<<123.4567<<endl;
   //double类型数据输出小数点后两位
   ```

2. 浮点数 等于/大于/小于

   ```C++
   const double eps = 1e-8;
   const double pi=acos(-1.0);					//圆周率
   
   #define Equ(a,b) ((fabs((a)-(b))<(eps))   	//宏定义 等于
   #define More(a,b) (((a)-(b))>(eps))   		//大于
   #define Less(a,b) (((a)-(b))>(-eps)) 		//大于等于
   #define Less(a,b) (((a)-(b))<(-eps))  		//小于
   #define Less(a,b) (((a)-(b))<(eps))   		//小于等于
   ```

***



## 第3章 入门模拟

### 3.1 简单模拟

1. 善用循环模拟

### 3.2 查找元素

1. 遍历查找
2. 二分查找

### 3.3 图形输出

1. 暂无

### 3.4 日期处理

1. 利用日期+1模拟

### 3.5 进制转换

1. K进制数到十进制数的转换（大小即十进制数）

![1556542702268](pic/1556598754408.png)

![1556542682057](pic/1556598757182.png)

2. 十进制到K进制数的转换-短除法（整数N为十进制）

![1556543192040](pic/1556598760934.png)

3. 十六进制数到二进制数的互相转换（4个二进制位正好对应于1个十六进制位）

![1556543213988](pic/1556598765251.png)

### 3.6 字符串处理

1. 回文串 判断一半
2. gets函数输入

***



## 第4章 算法初步

### 4.1 排序

#### 4.1.1 选择排序

#### 4.1.2 插入排序

#### 4.1.3 sort函数6.9.6

```c++
#include<iostream>
using namespace std;
int main(){
    int a[6]={9,4,2,5,6,-1};
    sort(a,a+4);//从小到大排序
    sort(a,a+6);
}

//char型默认 字典序

//比较函数 cmp
bool cmp(int a,int b){
    return a>b;
}
int main(){
    int a[6]={9,4,2,5,6,-1};
    sort(a,a+6,cmp);//从大到小排序
}

//结构体
//先按x从大到小排序，当x相等时，按y从小到大
bool cmp(node a,node b){
    if(a.x==b.x) return a.x>b.x;
    else return a.y<b.y;
}
//分数不同，分数高的排在前边 否则名字字典序小的排在前边
struct student{
    char name[10];
    char id[10];
    int score;
    int r;
}stu[100];

bool cmp(student a,student b){
    if(a.score!=b.score) return a.score>b,score;
    else return strcmp(a.name,b.name)<0;
    //若a.name字典序小于b.name strcmp返回-1
    // v 等同于a.name<b.name 
}
```

​	在STL标准容器中，只有vetor, string, deque可以用sort；set、map是用红黑树实现的，元素本身有序

***

### 4.2 散列

#### 4.2.1 散列定义与整数散列

​		空间换时间，读入数据时就进行预处理。判断是否出现过，直接true或false；判断出现几次，直接在其对应位置上进行相加。

>  将元素通过一个函数转换为整数，使得该整数可以尽量唯一的代表这个元素

* 散列函数

  + 直接定址法：数组的下标代表这个元素
+ 线性变化法：
  
  $$
  H(key)= a * key+b
  $$
  
  + 平方取中法：key的平方的中间若干位作为hash值
  + 除留余数法：

$$
\mathrm{H}(\mathrm{key})=\mathrm{key} \% \mathrm{mod}
$$
+ 解决冲突的方法

  * 线性探查法：key的hash值为H(key)，若已经被占，则检查下一个位置H(key)+1是否被占，超出表长，回到表头循环，直到有位置。
  
  * 平方探查法：检查下一个位置H(key)+1^2、H(key)-1^2、H(key)+2^2、H(key)-2^2。
  
    如果H(key)+k^2>Tsize，对Tsize取模
  
    如果H(key)-k^2<0，((H(key)-k^2)%Tsize+Tsize)%Tsize作为结果
  
    等价于H(key)-k^2不断加上Tsize直到出现第一个非负数
  
  * 链地址法（拉链法）:   7.3回头看

#### 4.2.2 字符串hash起步

​	**如何将一个二维整点P的坐标映射为一个整数，使得整点P可以由该整数唯一地代表。**

​	哈希函数`H(P)=x*Range+y`,这样对数据范围内的任意两个整点P1与P2。H(P1)都不会等于H(P2)，就可以用H(P)来唯一地代表该整点P。

​	字符串hash，字符串hash是指将一个字符串S映射为一个整数，使得该整数可以尽可能唯一地代表字符串S。

​	**字符串转换为唯一的整数**，假设字符串均由大写字母A~Z构成。A~Z视为0~25，这样就把26个大写字母对应到了二十六进制中。但是注意S不能太长。

```c++
int hashFunc(char S[],int len){  //hash函数
    int id=0;
    for(int i=0;i<len;i++){
        id=id*26+(S[i]-'A');
    }
    return id;
}
```

​	如果字符串中出现了小写字母，就变成了五十二进制(A-Z 0~25 a-z 26~51)转换为十进制的问题。

```C++
int hashFunc(char S[],int len){  //hash函数
    int id=0;
    for(int i=0;i<len;i++){
        if(S[i]>='A' && S[i]<='Z'){
            id=id*52+(S[i]-'A');
        }else if(S[i]>='a' && S[i]<='z'){
            id=id*52+(S[i]-'a')+26;
        }  
    }
    return id;
}
```

​	如果还出现了数字，两种处理方法：

* 增大进制到62
* 如果保证字符串末尾是确定个数的数字，把前面英文字母部分转整数，再将末尾数字直接拼接上去。

```c++
int hashFunc(char S[],int len){  //hash函数
    int id=0;
    for(int i=0;i<len-1;i++){
        id=id*26+(S[i]-'A');
    }
    id=id*10+(S[len-1]-'0');
    return id;
}
```

***

### 4.3 递归

#### 4.3.1 分治

> 将原问题划分成若干个规模较小而结构与原问题相同或相似的子问题(**子问题间相互独立**)，分别解决子问题，最后合并子问题的解，即可得到原问题的解

​	分解→解决→合并    用递归与非递归手段实现。

#### 4.3.2 递归

​	反复调用自身函数，每次都把问题范围缩小，知道缩小到可以直接得到边界数据的结果，然后再在返回的路上求出对应的解。

​	递归逻辑：	①**递归边界**——分解的尽头     ②**递归式**(递归调用)——分解问题的方法

	* 阶乘
	* 斐波那契数列
	* 全排列
	* n皇后

> 回溯法：如果在到达递归边界前的某一层，由于一些事实导致已经不需要往任何一个子问题递归，就可以直接返回上一层

***

### 4.4 贪心

#### 4.4.1 简单贪心 B1020 B1023

#### 4.4.2 区间贪心

​	区间不相交问题:给出N个开区间，从中选择尽可能多的开区间，使得这些开区间两两没有交集。解决思路：**总是选择左端点最大的区间，也可以总选择右端点最小的区间**。

```C++
struct Inteval{
    int x,y;
}I[maxn];

bool cmp(Inteval a,Inteval b){
    if(a.x!=b.x) return a.x>b.x;
    else return a.y<b.y;
}

int main(){
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d%d",&I[i].x,&I[i].y);
    }
    sort(I,I+n,cmp);
    int ans=1,lastX=I[0].x;
    for(int i=1;i<n;i++){
        if(I[i].y<=lastX){
            lastX=I[i].x;
        	ans++;
        }
    }
}
```

***

### 4.5 二分

#### 4.5.1 二分查找

​	见数据结构部分3.1

#### 4.5.2 二分法拓展

​	逼近精度法-模板

```c++
const double eps=1e-5;	//精度为10^-5
double f(double x){  //计算f(x)
    return ....;
}

double solve(double L,double R){
    double left=L,right=R,mid;
    while(right-left>eps){
        mid=(left+right)/2;
        if(f(mid)>0){
            right = mid;
        }else{
            left = mid;
        }
    }
    return mid;
}
```

#### 4.5.3 快速幂

​	给出三个正整数a、b、m（a<1e9、b<1e6、1<m<1e9）求a^b%m.

​	使用**快速幂**的做法，它基于二分的思想，因此也常称为二分幂。快速幂基于以下事实：

![1563952199862](pic/1563952199862.png)

​	b是奇数的情况总可以在下一步转换为b是偶数的情况，而b是偶数的情况总可以在下一步转换为b/2的情况。这样，在log(b)级别次数的转换后，就可以把b变为0，而任何正整数的0次方都是1.

![1563952336281](pic/1563952336281.png)

​	递归的思想，于是可以得到快速幂的递归写法，时间复杂度O(logb)

```c++
typedef long long LL;
//求a^b % m，递归写法
LL binaryPow(LL a,LL b,LL m){  
    if(b==0) return 1;  
    if(b%2==1) {  //if(b&1) 位与操作，判断b末位是否为1 二进制的最低位是1就是奇数,是0就是偶数
        return a*binaryPow(a,b-1,m)%m;
    }
    else{
        LL mul=binaryPow(a,b/2,m);
        return mul*mul % m;
    }//不要return binaryPow(a,b/2,m)*binaryPow(a,b/2,m)%m; 会增加时间复杂度
} 
```

* 如果初始时a有可能大于等于m,那么需要在进入函数前就让a对m取模.
* 如果m为1,可以直接在函数外部特判为0,不需要进入函数来计算(因为任何正整数对1取模一定等于0)

​    迭代的写法,对a^b来说,如果把b写成二进制,那么b就可以写成若干二次幂之和.

```C++
typedef long long LL;
//求a^b % m，迭代写法
LL binaryPow(LL a,LL b,LL m){  
LL ans=1;
    while(b>0){
        if(b&1){
            ans=ans*a%m;
        }
        a=a*a%m; //令a平方
        b>>=1;   //将b的二进制右移1位,即b=b>>1 或 b=b/2
    }
    return ans;
} 
```

***

### 4.6 two pointers

#### 4.6.1 讲述

​	给定一个递增的正整数序列和一个正整数M,求序列中的两个不同位置的数a和b,使得它们的和恰好为M,输出所有满足条件的方案.例如给定序列{1,2,3,4,5,6}和正整数M=8,就存在2+6=8与3+5=8.

```C++
while(i<j){
    if(a[i]+a[j]==m){  //找到其中一组
        printf("%d %d\n",i,j);
        i++;    //i向右移动
        j--;	//j向左移动
    }else if(a[i]+a[j]<m){
        i++;	//i向右移动
    }else{
        j--;	//j向左移动
    }
}
```

​	时间复杂度O(n)

​	序列合并问题.假设有两个递增序列A和B,要求将它们合并为一个递增序列C.

```c++
int merge(int A[],int B[],int n,int m){
    int i=0,j=0,index=0;	//i指向A[0],j指向B[0]
    while(i<n && j<m){
        if(A[i]<B[i]){	
            C[index++]=A[i++];
        }else{
            C[index++]=B[j++];
        }
    }
    while(i<n) C[index++]=A[i++];
    while(j<m) C[index++]=B[j++];
    return index;
}
```

#### 4.6.2 归并排序

​	见数据结构2.4 归并排序

#### 4.6.3 快速排序

​	见数据结构2.5 快速排序

​	生成随机数的函数

```C++
include<cstdlib.h><time.h>
int main(){
	srand((unsigned)time(NULL));
	printf("%d",rand());//范围 [0,32767]
	printf("%d",rand()%(b-a+1));//范围[0,b-a]
	printf("%d",rand()%(b-a+1)+a);//范围[a,b] b不大于32767
	printf("%d",(int)(round(1.0*rand()/RAND_MAX*50000+10000));//范围[10000,60000]
}
```

***

### 4.7 其他高效技巧与算法

#### 4.7.1 打表

​	空间换时间，一般指将所有可能需要用到的结果事先计算出来，这样后面需要用到时就可以直接查表获得。打表常见的用法有以下及几种：

1. **程序中一次性计算出所有需要用到的结果，之后查询直接取这些结果**

   查询大量Fibonacci数F(n)的问题中，进行预处理，把所有Fibonacci数预先计算并存在数组中。

2. **在程序B中分一次或多次计算出所有需要用到的结果，手工把结果写在程序A的数组中，然后在程序A中就可以直接使用这些结果**

   在高性能计算机上暴力求解出的答案，直接放在程序中，调用结果。

3. **对一些感觉不会做的题目，先用暴力程序计算小范围数据的结果，然后找规律，或许就能发现一些“蛛丝马迹”。**

   数据范围非常大的时候，可以找规律

#### 4.7.2 活用递推

​	如果能找到递推关系，就能让时间复杂度降低不少。

​	P148

```c++
#include<cstdio>
#include<cstring>
#include<iostream>
using namespace std;

const int MAXN = 100010;
const int MOD = 1000000007;
char str[MAXN];
int leftNumP[MAXN] = { 0 };

int main() {
	cin.getline(str,100010);
	int len = strlen(str);
	for (int i = 0; i < len; i++) {
		if (i > 0) {
			leftNumP[i] = leftNumP[i - 1];
		}
		if (str[i] == 'P') {
			leftNumP[i]++;
		}
	}
	int ans = 0, rightNumT = 0;
	for (int i = len - 1; i >= 0; i--) {
		if (str[i] == 'T') {
			rightNumT++;
		}
		else if (str[i] == 'A') {
			ans = (ans + leftNumP[i] * rightNumT) % MOD;
		}
	}
	printf("%d\n", ans);
	return 0;
}
```

#### 4.7.3 随机选择算法

​	从无序的数组中求出第K大的数.

​	当对A[left,right]执行一次randPartition函数后，主元左侧的元素的个数是确定的，且他们都小于主元。假设此时主元是A[p],那么A[p]就是A[left,right]中的第p-left+1大的数。令M=p-left+1，那么如果K==M成立，说明第K大的数就是主元A[p]；如果K<M成立，就说明第K大的数在主元左侧，往左侧递归即可。

```c++
//随机选择算法 返回第K大的数
int randselect(int A[],int left,int right,int K){
	if(left==right) return A[left]; //边界
    int p=randPartition(A,left,right);
    int M=p-left+1;
    if(K==M） return A[p];
    if(K<M){
        return randselect(A,left,p-1,K);
    }else{
        return randselect(A,p+1,right,K-M);
    }
}
```

```c++
int Partition(int A[],int left,int right){
    int temp=A[left];
    while(left<right){
        while(left<right && A[right]>temp) right--;
        A[left]=A[right];
        while(left<right && A[left]<=temp) left++;
        A[right]=A[left];
    }
    A[left]=temp;
    return left;
}
```



## 第5章 入门篇(3)——数学问题

### 5.1 简单数学

***

### 5.2 最大公约数与最小公倍数

#### 5.2.1 最大公约数

​	递归式：gcd(a,b)=gcd(b,a%b);

​	递归边界：gcd(a,0)=a;

```c++
int gcd(int a,int b){
    if(b==0) return a;
    else return gcd(b,a%b)
}
```

#### 5.2.2 最小公倍数

```c++
int gcd(int a,int b){
	if(b==0) return a;
	else return gcd(b,a%b)
}

int d=gcd(a,b);  //d为a b的最大公约数
int e=a/d*b; 	 //e为a b的最小公倍数 一定为整
```
***

### 5.3 分数的四则运算

#### 5.3.1 分数的表示和化简

 1. 分数的表示

    假分数

    ```c++
    struct Fraction{
        int up,down;//分子、分母
    };
    // down 非负数 up代表有正负号
    // 分数为0 up为0 down为1
    //分子分母没有除了1以外的公约数
    ```

 2. 分数的化简

    ```c++
    Fraction reduction(Fraction result){//返回Fraction类型的结构体
        if(result.down<0){
            result.up=-result.up;
            result.down=result.down;
        }
        if(result.up==0)[
            result.down=1;
        ]else{
            int d=gcd(abs(result.up),abs(result.down));
            result.up/=d;
            result.down/=d;
        }
        return result;
    }
    ```

#### 5.3.2 分数的四则运算

 1. 分数的加法

    ```c++
    Fraction add(Fraction f1,Fraction f2){//返回Fraction类型的结构体
        Fraction result;
        result.up=f1.up*f2.down+f2.up*f1.down;
        result.down=f1.down*f2.down;
        return reduction(result);
    }
    ```

    ![1564540044786](pic/1564540044786.png)

 2. 分数的减法

    ![1564540144594](pic/1564540144594.png)

 3. 分数的乘法

    ![1564540153517](pic/1564540153517.png)

 4. 分数的除法

    有特判，若读入的除数为0，只需判断f2.up是否为0，直接特判

    ![1564540164499](pic/1564540164499.png)

#### 5.3.3 分数的输出

```c++
void showResult(Fraction r){
    r=reduction(r);
    if(r.down==1) printf("%lld".r.up);	//整数
    else if(abs(r.up)>r.down){			//假分数
        printf("%d %d/%d",r.up/r.down,abs(r.up)%r.down,r.down);
    }else{								//真分数
        printf("%d/%d",r.up,r.down);
    }
}
```

​	一般分子，分母用longlong型来存储。

### 5.4 素数

​	素数/质数，指除了1和本身之外，不能被其他数整除的一类数。即对给定的正整数n,如果对任意的正整数a(1<a<n)，都有n%a!=0成立，那么称n是素数；否则，为合数。1既不是素数，也不是合数

#### 5.4.1 素数的判断

```c++
bool isPrime(int n){
    if(n<1) return false;
    int sqr=(int)sqrt(1.0*n);    //变为浮点数 sqrt只能对sqrt开根
    for(int i=2;i<=sqr;i++){
        if(n%i==0) return fasle;
    }
    return true;
}
```

​	只需要判断n能否被2,3,……,**⌊sqrt(n)⌋**中的一个整除，即可判断为素数

```c++
bool isPrime(int n){			//n没有接近int型变量的范围上界
    if(n<1) return false;		//n在10^9以内都安全
    for(int i=2;i*i<=n;i++){
        if(n%i==0) return fasle;
    }
    return true;
}
```

#### 5.4.2 素数表的获取

​	n不超过10^5的大小是可以打印素数表的

```c++
const int maxn=101;		//表长
int prime[maxn],pNum=0;	//prime数组存放所有的素数，pNum为素数个数
bool p[maxn]={0}; //P[i]==ture 表示i是素数
void find_prime(){
    for(int i=1;i<maxn;i++){
        if(isPrime(i)==true){
            prime[pNum++]=i;
            p[i]=true;
        }
    }
}
```

>埃氏筛法：从2开始，将每个质数的倍数都标记成合数，以达到筛选素数的目的

```c++
int prime[maxn],pNum=0;			//prime数组存放所有素数，pNum为素数个数
bool p[maxn]={0};				//如果i为素数,则p[i]为false；否则,p[i]为true
void Find_Prime(){
    for(int i=2;i<maxn;i++){	//2开始，i<maxn结束
        if(p[i]==false){		//如果i是素数
            prime[pNum++]=i;	//把素数i存在prime数组中
            for(int j=i+i;j<maxn;j+=i){
                //筛去所有i的倍数，循环条件不能写成j<=maxn
                p[j]=ture;
            }
        }
    }
}
```

$$
\mathrm{O}\left(\sum_{i=1}^{n} n / i\right)=O(n \log \log n)
$$

### 5.5 质因子分解

> 将一个正整数n写成一个或多个质数的乘积的形式。例如：6=2x3；8=2x2x2；或者写成指数形式。

​	由于每个质因子都可以不止一次的出现，因此不妨定义结构体factor，用来存放质因子及其个数

```c++
struct factor{
    int x,cnt;	//x为质因子，cnt为其个数
}fac[10];	//fac数组大小给到10就可以了 11就超过int范围
```

​	fac数组存放的就是给定的正整数n的所有质因子。例如对180来说，fac数组如下：

```c++
fac[0].x=2;
fac[0].cnt=2;

fac[1].x=3;
fac[1].cnt=2;

fac[2].x=5;
fac[2].cnt=1;
```

​	**对一个正整数n来说，如果存在1和本身之外的因子，那么一定是在sqrt(n)的左右成对出现。**

​	**对一个正整数n来说，如果存在[2,n]范围内的质因子，要么这些因子全部小于等于sqrt(n),要么只存在一个大于sqrt(n)的质因子，而其它质因子全部小于等于sqrt(n)**

1. 枚举1~sqrt(n)范围内所有质因子p，判断p是否为n的因子

   ```c++
   if(n%prime[i] ==0){
       fac[num].x=prime[i];
       fac[num].cnt=0;
       while(n%prime[i]==0){
           fac[num].cnt++;
           n/=prime[i];
       }
       num++;
   }
   ```

2. 如果上面步骤结束后n仍然大于1，说明n有且仅有一个大于sqrt(n)的质因子(有可能是n本身)

   ```c++
   if(n!=1){				//如果无法被根号n以内的质因子除尽
       fac[num].x=n;		//那么一定有一个大于根号n的质因子
       fac[num++].cnt=1;
   }
   ```


### 5.6 大整数运算

#### 5.6.1 大整数的存储

​	使用数组存储。整数的高位存储在数组的高位，整数的低位存储在数组的低位。把整数按字符串%s读入之后，需要在另存为至d[]数组的时候反转一下。

```c++
struct bign{      //big number
    int d[1000];
    int len;
    //初始化 构造函数
    bign(){
        memset(d,0,sizeof(d));   //对数组赋初值
        len=0;
    }
};
```

​	输入大整数时，一般先用字符串读入，然后再把字符串另存为至bign结构体。由于使用char数组进行读入时，整数的高位会变成数组的低位，而整数的低位会变成数组的高位，因此为了让整数在bign中是顺位存储，需要让字符串倒着赋给d[]数组。

```C++
bign change(char str[]){ //将整数转换为bign
    bign a;
    a.len = strlen(str);  //bign的长度就是字符串的长度
	for(int i=0;i<a.len;i++){
        a.d[i]=str[a.len-i-1]-'0';	//逆着赋值
    }    
	return a;
}
```

​	如果比较两个bign大小，先判断len大小，再从高位到低位判断

```c++
int compare(bign a,bign b){
    if(a.len>b.len) return 1;
    else if(a.len<b.len) return -1;
    else{
        for(int i=a.len-1;i>=0;i--){
            if(a.d[i]>b.d[i]) return 1;
            else if(a.d[i]<b.d[i]) return -1;
        }
        return 0;	//两数相等
    }
}
```

#### 5.6.2 大整数的四则运算

1. 高精度加法

   ```c++
   bign add(bign a,bign b){
       bign c;
       int carry=0;
       for(int i=0;i<a.len || i<b.len;i++){	//较长的为界限
           int temp=a.d[i]+b.d[i]+carry;	//两个对应位与进位相加
           c.d[c.len++]=temp%10;		//个位数为该位结果
           carrt=temp/10;				//十位数为新的进位
       }
       if(carry!=0){	//最后进位不为0，则直接赋给结果的最高位
           c.d[c.len++]=carry;
       }
       return c;
   }
   ```

2. 高精度减法

   ```C++
   bign sub(bign a,bign b){
       bign c;
       int carry=0;
       for(int i=0;i<a.len || i<b.len;i++){	//较长的为界限
           if(a.d[i]<b.d[i]){		//如果不够减
               a.d[i+1]--;			//向高位借位
               a.d[i]+=10;			//当前位加10
           }
           c.d[c.len++]=a.d[i]-b.d[i];	//减法结果为当前位结果
       }
       while(c.len-1>=1 && c.d[c.len-1]==0){
           c.len--;	//去除高位的0，同时至少保留一位最低位
       }
       return c;
   }
   ```

3. 高精度与低精度的乘法

   ```c++
   bign multi(bign a,bign b){
       bign c;
       int carry=0;				//进位
       for(int i=0;i<a.len;i++){	
           int temp=a.d[i]*b+carry;
           c.d[c.len++]=temp%10;	//个位作为该位结果
           carry=temp/10;			//高位部分作为新的进位
       }
       while(carry!=0){			//和加法不一样，乘法的进位可能不止一位，因此用while
           c.d[c.len++]=carry%10;
           carry/=10;
       }
       return c;
   }
   ```

4. 高精度与低精度的除法

   ```c++
   bign divide(bign a,bign b,int& r){
       bign c;
       c.len=a.len						//被除数的每一位和商的每一位是一一对应的，因此先令长度相等
       for(int i=a.len-1;i>=0;i--){	//从高位开始
           r=r*10+a.d[i];
           if(r<b) c.d[i]=0;
           else{
               c.d[i]=r/b;
               r=r*b;
           }
       }
       while(c.len-1>=1 && c.d[c.len-1]==0){
   		c.len--;
    }
       return c;
   }
   ```
   

### 5.7 扩展欧几里得算法

#### 5.7.1 扩展欧几里得算法

​	给定两个非零整数a和b，求一组整数解（x，y）使得ax+by=gcd（a，b）成立，其中gcd（a，b）表示a和b的最大公约数。

```c++
int gcd(int a,int b){
    if(b==0) return a;
    else return gcd(b,a%b);
}
```





## 第6章 C++标准模板库(STL)介绍

### 6.1 vector

​	向量，“变长数组”，“长度根据需要而自动改变的数组”。有时会碰到只用普通数组会超内存的情况，这种情况使用vector会便捷许多。vector还可以以邻接表的方式储存图，对**无法使用邻接矩阵**的题目（结点数太多）、又害怕**使用指针实现邻接表**的读者十分友好。

```c++
#include<vector>
using namespace std;
```

#### 6.1.1 vector定义

```c++
vector<typename> name;//等同于一维数组name[SIZE],只不过其长度可以根据需要进行变化，比较节省空间。
//typename 可以是 int、double、char、结构体等，也可以是vector、set、queue等
vector<int> name;
vector<double> name;
vector<char> name;
vector<node> name;	//结构体类型

//二维数组  二维vector数组 当作两个都可变长的二维数组
vector<vector<int> > name;	//!!!!!!!! >>之间要加空格

//vector数组
vector<typename> Arrayname[arraySize];
vector<int> vi[100];	//vi[0]~vi[100]中每一个都是一个vector容器。 一维长度已经固定为100
//与vector<vector<int> > name;不同的是  其中一维长度是否已经固定
```

#### 6.1.2 vector容器内元素的访问

1. 通过下标访问

```c++
vector<int> vi;
printf("%d %",v[0],v[99]);
```

2. 通过迭代器访问

```c++
vector<typename>::iterator it;	//it为迭代器变量
vector<int> vi;
for(int i=1;i<=5;i++){
    vi.push_back(i);	//push_back(i)在vi的末尾添加元素i，即依次添加1 2 3 4 5 
}
```

通过类似下标和指针访问数组的方式来访问容器内的元素

```c++
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
    vector<int> vi;
    for(int i=1;i<=5;i++){
        vi.push_back(i);
    }
    //vi.begin()为取vi的首元素地址，而it指向这个地址
   	vector<int>::iterator it=vi.begin();
    for(int i=0;i<5;i++){
        printf("%d ",*(it+i));			  			//1 2 3 4 5
    }
    return 0;
}
```

​	 vi[i]和*(vi.begin()+i)是等价的

​	end()取vi的尾元素地址的下一个地址。end()作为迭代器末尾标志，不储存任何元素。

```c++
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
    vector<int> vi;
    for(int i=1;i<=5;i++){
        vi.push_back(i);
    }
    //vi.begin()为取vi的首元素地址，而it指向这个地址
   	
    for(vector<int>::iterator it=vi.begin();it!=vi.end();it++){
        printf("%d ",*it);			//1 2 3 4 5 
    }
    return 0;
}
```

​	**STL容器中，只有vector和string中，允许使用vi.begin()+3这种迭代器加上整数的写法**

#### 6.1.3 vector常用函数

 1. push_back(i)

    ```C++
    //在vector后面添加元素x，世家复杂度O(1)
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=1;i<=3;i++){
            vi.push_back(i);
        }
        for(int i=0;i<vi.size();i++){
            printf("%d ",vi[i]);		// 1 2 3
        }
        return 0;
    }
    ```

 2. pop_back()

    ```c++
    //有添加就会有删除， 删除vector尾元素
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=1;i<=3;i++){
            vi.push_back(i);
        }
        vi.pop_back();	//删除vi尾部元素
        for(int i=0;i<vi.size();i++){
            printf("%d ",vi[i]);		// 1 2 
        }
        return 0;
    }
    ```

 3. size()

    ```c++
    //获取vector中元素的个数
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=1;i<=3;i++){
            vi.push_back(i);
        }
        printf("%d ",vi.size());		// 3
        return 0;
    }
    ```

 4. clear()

    ```c++
    //清空vector中所有元素
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=1;i<=3;i++){
            vi.push_back(i);
        }
        vi.clear();
        printf("%d ",vi.size());		// 0
        return 0;
    }
    ```

 5. insert(it,x)

    ```c++
    //向vector的任意迭代器it处插入一个元素x
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=1;i<=5;i++){
            vi.push_back(i);	//1 2 3 4 5 
        }
        vi.insert(vi.begin()+2,-1);	//将-1插入vi[2]的位置
        for(int i=0;i<vi.size();i++){
            printf("%d ",vi[i]);		// 1 2 -1 3 4 5
        }
        return 0;
    }
    ```

 6. erase(it)/erase(first,last)

    ```c++
    //删除迭代器为it处的元素
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=5;i<=9;i++){
            vi.push_back(i);	//5 6 7 8 9
        }
        //删除8 
        vi.insert(vi.begin()+3);
        for(int i=0;i<vi.size();i++){
            printf("%d ",vi[i]);		// 5 6 7 9 
        }
        return 0;
    }
    ```

    ```c++
    //删除一个区间[fisrt,last)内的所有元素
    #include<stdio.h>
    #incldue<vector>
    using namespace std;
    int main(){
        vector<int> vi;
        for(int i=5;i<=9;i++){
            vi.push_back(i);	//5 6 7 8 9
        }
        //删除8 
        vi.insert(vi.begin()+1，vi.begin()+4);
        for(int i=0;i<vi.size();i++){
            printf("%d ",vi[i]);		// 5 9 
        }
        return 0;
    }
    ```

#### 6.1.4 vector的常见用途

 	1. 储存数据
     * vector本身可以作为数组使用，而且一些元素个数不确定的场合可以很好的节省空间
     * 有些场合需要根据一些条件把部分数据输出在同一行，数据中间用空格隔开。由于输出数据的个数是不确定的，为了更方便地处理最后一个满足条件的数据后面不输出额外的空格，可以下用vector记录所有需要输出的数据，然后一次性输出。
     
  2. 用邻接表存储图

     使用vector实现邻接表 10.2.2

---

### 6.2 set

​	集合，是一个**内部自动有序**且**不包含重复元素**的容器。有可能出现需要去掉重读元素的情况，有可能元素比较大或者类型不是int型而不能直接开散列表，这种情况可以用set**保留元素本身而不是考虑它的个数**。	也可以再开一个数组进行下标和元素的对应来解决。

```c++
#include<set>
using namespace std;
```

#### 6.2.1 set定义

```c++
set<typename> name;	//typename 可以是 int、double、char、结构体等，也可以是vector、set、queue等
set<int> name;
set<double> name;
set<char> name;
set<node> name;	//node结构体类型

//二维数组  二维set数组
set<set<int> > name;	//!!!!!!!! >>之间要加空格

//set数组
set<typename> Arrayname[arraySize];

set<int> a[100];	//a[0]~a[100]中每一个都是一个set容器。 一维长度已经固定为100
```

---

#### 6.2.2 set容器内元素的访问

1. **只能通过迭代器访问**

```c++
set<typename>::iterator it;	//it为迭代器变量
set<int>::iterator it;	//it为迭代器变量
```

```c++
//只能通过*it方式访问
#include<stdio.h>
#include<vector>
using namespace std;
int main(){
    set<int> st;
    st.insert(3);	//将x插入set中
    st.insert(5);
    st.insert(2);
    st.insert(3);
//注意，不支持it<st.end()的写法
    for(set<int>::iterator it=st.begin();it!=st.end();it++){
        printf("%d ",*it);			//2 3 5 
    }
    return 0;
}
```

---

#### 6.2.3 set常用函数

1. insert(x)

   ```c++
   //向vector的任意迭代器it处插入一个元素x
   #include<stdio.h>
   #incldue<vector>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(2);	
       st.insert(5);
       st.insert(4);
       printf("%d ",st.size());		// 3
       return 0;
   }
   ```
   
2. find(x)

   ```c++
   //返回set中对应值为value的迭代器
   #include<stdio.h>
   #incldue<set>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(2);	
       st.insert(5);
       st.insert(4);
       set<int>::iterator it=st.find(2);//在set中查找2，返回迭代器
       printf("%d ",*it);		// 2
       return 0;
   }
   ```

3. size()

   ```c++
   //获取set中元素的个数
   #include<stdio.h>
   #incldue<set>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(2);	
       st.insert(5);
       st.insert(4);
       printf("%d ",st.size());		// 3
       return 0;
   }
   ```

4. clear()

   ```c++
   //清空set中所有元素
   #include<stdio.h>
   #incldue<vector>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(2);	
       st.insert(5);
       st.insert(4);
       st.clear();
       printf("%d ",vi.size());		// 0
       return 0;
   }
   ```

5. erase(it)/erase(first,last)

   ```c++
   //删除迭代器为it处的元素
   #include<stdio.h>
   #incldue<set>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(100);	
       st.insert(200);
       st.insert(100);
       st.insert(300);
       st.erase(st.find(100));
       st.erase(st.find(200));
      	for(set<int>::iterator it=st.begin();it!=st.end();it++){
           printf("%d ",*it);			//300
       }
       return 0;
   }
   
   //直接删除所需要删除的值
   #include<stdio.h>
   #incldue<set>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(100);	
       st.insert(200);
       st.erase(100);
       for(set<int>::iterator it=st.begin();it!=st.end();it++){
           printf("%d ",*it);			//200
       }
       return 0;
   }
   ```

   ```c++
   //删除一个区间[fisrt,last)内的所有元素
   #include<stdio.h>
   #incldue<set>
   using namespace std;
   int main(){
       set<int> st;
       st.insert(20);	
       st.insert(10);
       st.insert(40);
       st.insert(30);
       set<int>::iterator it=st.find(30);//在set中查找2，返回迭代器
       st.erase(it,st.end());
       for(set<int>::iterator it=st.begin();it!=st.end();it++){
           printf("%d ",*it);			//10 20
       }
       return 0;
   }
   ```

---

#### 6.2.4 set的常见用途

​	set最主要的作用是**自动去重**并按**升序排序**，因此碰到**需要去重但是不方便直接开数组**的情况，可以尝试用set解决。
​	**延伸**：set 中元素是唯一的，如果需要处理不唯一的情况，则需要使用multiset。增加了unordered_set，以散列代替set内部的红黑树（自平衡二叉查找树）实现，使其可以用来处理只去重但不排序的需求，速度比set要快得多

​	

### 6.3 string

​	在c语言中，一般使用字符数组char str[]来存放字符串，但是使用字符数组有时会显得操作麻烦。

```c++
#include<string>
using namespace std;
//！！！！！！！！string 和cstring不一样
```

#### 6.3.1 string定义

```c++
string str;	//str变量名

string str="abcd";
```

------

#### 6.3.2 string容器内元素的访问

1. **通过下标访问**

   ```C++
   #incldue<stdio.h>
   #include<string>
   using namespace std;
   int main(){
       string str="abcd";
       for(int i=0;i<str.length();i++){
           printf("%c",str[i]);	//abcd
       }
       return0
   }
   ```

   如果要**读入和输出**整个字符串，则只能用**cin和cout**;

   ```c++
   #include<isotream>
   #include<string>
   using namespace std;
   int main{
       string str;
       cin>>str;
       cout<<str;
       return 0;
   }
   ```

2. **通过迭代器访问**

    ```c++
    string::iterator it;	//it为迭代器变量
    ```
    
    这样就得到了迭代器it，并且可以通过*it来访问string里的每一位
    
    ```c++
    #include<isotream>
    #include<string>
    using namespace std;
    int main{
        string str="abcd";
        for(string::iterator it=st.begin();it!=st.end();it++){
            printf("%c ",*it);			//abcd
        }
        return 0;
    }
    ```

​	**STL容器中，只有vector和string中，允许使用str.begin()+3这种迭代器加上整数的写法**

------

#### 6.3.3 string常用函数

1. operator+=	string的加法 直接拼接

   ```c++
   #include<isotream>
   #include<string>
   using namespace std;
   int main{
       string str1="abc",str2="xyz",str3;
       str3=str1+str2;
       str1+=str2;
       cout<<str1<<endl;	//abcxyz
       cout<<str3<<endl;	//abcxyz
       return 0;
   }
   ```

2. compare operator

   ```c++
   //两个string类型可以直接使用== ！= 等比较大小 字典序
   #include<isotream>
   #include<string>
   using namespace std;
   int main{
       string str1="aa",str2="aaa",str3="abc",str4="xyz";
       if(str1<str2) printf("ok1\n");	//ok1
       if(str1!=str3) printf("ok2\n");	//ok2
       if(str4>=str3) printf("ok3\n");	//ok3
       return 0;
   }
   ```

3. length()/size()

   ```C++
   //返回string的长度，即存放的字符数
   #include<stdio.h>
   #include<string>
   using namespace std;
   int main(){
       string str="abcxyz";	
       printf("%d %d",str.size(),str.length());// 6 6
       return 0;
   }
   ```

4. insert(x)

   ```c++
   //insert(pos,string) 早pos号位置插入字符串string
   string str="abcxyz" ,str2="opq";
   str.insert(3,str2);	//往str[3]处插入opq，str2的位置直接写"opq"也可以
   cout<<str<<endl; //abcopqxzy
   ```

   ```c++
   //insert(it,it2,it3)，it为原字符串的欲插入位置，it2和it3为待插字符串的首尾迭代器，用来表示串[it2,it3)将被插在it的位置上。
   string str="abcxyz" ,str2="opq";
   str.insert(str.begin()+3,str2.begin(),str2.end());
   cout<<str<<endl;//abcopqxyz
   ```

5. erase()

   ```c++
   //删除单个元素
   int main(){
       string str="abcdefg";
       str.erase(str.begin()+4);	//删除4号位
      	cout<<str<<endl;	//abcdfg
       return 0;
   }
   ```

   ```c++
   //删除一个区间[fisrt,last)内的所有元素
   int main(){
        string str="abcdefg";
       str.erase(str.begin()+2,str.end()-1);	//删除cdef
      	cout<<str<<endl;	//abg
       return 0;
   }
   ```

   ```c++
   //str.erase(pos,length) pos开始删除的起始位置，length为删除的字符个数
   int main(){
       string str="abcdefg";
       str.erase(3，2);	//删除de
      	cout<<str<<endl;	//abcfg
       return 0;
   }
   ```

6. clear()

   ```c++
   //清空string中所有元素
   int main(){
       string str="abcdefg";
       str.clear();	
      	printf("%d",str.length());	//0
       return 0;
   }
   ```

7. substr()

   ```c++
   //substr(pos,len) 返回从pos号位开始、长度为len的子串
   int main(){
       string str="Thank you for your smile";
      	cout<<str.substr(0,5)<<endl;	//Thank
       cout<<str.substr(14,4)<<endl;	//your
       return 0;
   }
   ```

8. string::npos

   ```c++
   //本身的值为-1/4294967295 find函数失配时的返回值
   ```

9. find(x)

   ```c++
   //find(str2)，当str2是str的子串时，返回其在str中第一次出现的位置；如果str2不是str的子串，返回string::npos
   //find(str2,pos),从str和pos号位开始寻找str2
   int main(){
       string str="Thank you for your smile";
       string str2="you";
       string str3="me";
       if(str.find(str2)!=string::npos){
           cout<<str.find(str2)<<endl;
       }
       if(str.find(str2,7)!=string::npos){
           cout<<str.find(str2,7)<<endl;
       }
       if(str.find(str2)!=string::npos){
           cout<<str.find(str3)<<endl;
       }else{
           cout<<"i know"<<endl;
       }
       return 0;
   }
   ```

10. replace()

   ```c++
   //replace(pos,len,str2)	把str从pos号位开始，长度为len的子串替换为str2
   //replace(it1,it2,str2)把str的迭代器[it1，it2)范围的子串替换为str2
   int main(){
       string str="Maybe you will turn around";
       string str2="will not";
       string str3="surely";
       cout<<str.replace(10,4,str2)<<endl;
       //Maybe you will not turn around
       cout<<str.replace(str.begin(),str.begin()+5,str3)<<endl;
       //surely you will turn around
       return 0;
   }
   ```

------

### 6.4 map-映射

​	映射，普通数组是int型映射到其他类型。map可以将**任何基本类型**（包括STL容器）映射到**任何基本类型**（包括STL容器）.

​	情况：判断给定数字在某个文件中是否出现过。如果数字很大hashtable数组无法开。map可以把数字当作字符串建立string到int的映射。

```c++
#include<map>
using namespace std;
```

#### 6.4.1 map定义

```c++
map<typename1, typename2> mp;	//键key	值value 两个类型

//字符到整形的映射，只能string不能char数组
map<string,int> mp;

//键和值也可以是stl容器
map<set<int>,string> mp;
```

------

#### 6.4.2 map容器内元素的访问

1. 通过下标访问

   ```c++
   map<char int> mp;
   mp['c']=20;
   mp['c']=30;//20被覆盖
   printf("%d\n",mp['c'])；//输出30
   ```

2. 通过迭代器访问

   ```c++
   map<typename1,typename2>::iterator it;	//it为迭代器变量
   ```

   ```c++
   //map可以用it->first来访问键，使用it->second来访问值
   map<char int> mp;
   mp['m']=20;
   mp['r']=30;
   mp['a']=40；
   for(map<char,int>::iterator it=mp.begin();it!=mp.end();it++){
   	printf("%c %d\n",it->first,it->second);
   }
   //a 40
   //m 20
   ```

   **map会以键从小到大的顺序自动排序**，即按a<m<r的顺序排列三对映射。

------

#### 6.4.3 map常用函数

1. find()

   ```c++
   //返回键为key的映射的迭代器
   map<char int> mp;
   mp['a']=1;
   mp['b']=2;
   mp['c']=3；
   map<char,int>::iterator it=mp.find('b');
   printf("%c %d\n",it->first,it->second);
   //b 2
   ```

2. erase()

   ```c++
   //删除单个元素erase(it)   it为需要删除的元素的迭代器
   map<char int> mp;
   mp['a']=1;
   mp['b']=2;
   mp['c']=3；
   map<char,int>::iterator it=mp.find('b');
   mp.erase(it); //删除b 2
   for(map<char,int>::iterator it=mp.begin();it!=mp.end();it++){
   	printf("%c %d\n",it->first,it->second);
   }
   //a 1
   //c 3
   
   //erase(key)	key为欲删除的映射的键
   map<char int> mp;
   mp['a']=1;
   mp['b']=2;
   mp['c']=3；
   mp.erase('b'); //删除b 2
   for(map<char,int>::iterator it=mp.begin();it!=mp.end();it++){
   	printf("%c %d\n",it->first,it->second);
   }
   //a 1
   //c 3
   ```

   ```c++
   //删除一个区间内的所有元素	erase(first,last) [first,last）
   map<char int> mp;
   mp['a']=1;
   mp['b']=2;
   mp['c']=3；
   map<char,int>::iterator it=mp.find('b');
   mp.erase(it,mp.end()); //删除it之后的所有映射
   for(map<char,int>::iterator it=mp.begin();it!=mp.end();it++){
   	printf("%c %d\n",it->first,it->second);
   }
   //a 1
   ```

3. size()

   ```c++
   //获取map中映射对数
   map<char int> mp;
   mp['a']=1;
   mp['b']=2;
   mp['c']=3；
   printf("%d\n",mp.size());	//3
   ```

4. clear()

   ```c++
   //清空map中所有元素
   map<char int> mp;
   mp['a']=1;
   mp['b']=2;
   mp['c']=3；
   mp.clear();
   printf("%d\n",mp.size());	//3
   ```

------

#### 6.4.4 map的常见用途

1. 需要建立字符(或字符串)与整数之间映射的题目，使用map可以减少代码量
2. 判断大整数或者其他类型数据是否存在的题目，可以把map当作bool数组用
3. 字符串和字符串的映射可以也会用到

延伸:map的键和值是唯一的，如果一个键需要对应多个值，只能用multimap。还增加了unordered_map，以散列代替map内部红黑树，速度快

---

### 6.5 queue-队列

​	队列，实现**先进先出**的容器

```c++
#include<queue>
using namespace std;
```

#### 6.5.1 queue定义

```c++
queue<typename> name;	//typename 任意基本数据类型或容器
```

------

#### 6.5.2 queue容器内元素的访问

1. **只能通过front()来访问队首元素,或back()访问队尾元素**

```c++
queue<int> q;
for(int i=1;i<=5;i++){
    q.push(i);
}
printf("%d %d",q.front(),q.back());//1 5 
```

------

#### 6.5.3 queue常用函数

1. push()

   ```c++
   //push(x)将x压入队列
   queue<int> q;
   for(int i=1;i<=5;i++){
       q.push(i);
   }
   ```

2. front()\back()

   ```c++
   printf("%d %d",q.front(),q.back());//1 5 
   ```

3. pop()

   ```c++
   //令队首元素出队
   queue<int> q;
   for(int i=1;i<=5;i++){
       q.push(i);
   }
   printf("%d %d",q.front(),q.back());//1 5 
   for(int i=1;i<=3;i++){
       q.pop();//出队首元素三次 1 2 3 
   }
   printf("%d %d",q.front(),q.back());//4 5 
   ```

4. empty()

   ```c++
   //检测queue是否为空,true为空,false为非空
   queue<int> q;
   if(q.empty==ture){
       printf("empty");
   }else{
       printf("not empty")
   }
   q.push(1);
   if(q.empty==ture){
       printf("empty");
   }else{
       printf("not empty")
   }
   //empty
   //not empty
   ```

5. size()

   ```c++
   //返回queue内元素的个数
   queue<int> q;
   for(int i=1;i<=5;i++){
       q.push(i);
   }
   printf("%d",q.size());	//5
   ```

------

#### 6.5.4 queue的常见用途

1. 需要实现广度优先搜索时,使用queue代替
2. 使用front()和pop()函数前,必须用empty()判断队列是否为空.

延伸:双队列deque/优先队列priority_queue

------

### 6.6 priority_queue-优先队列

​	优先队列，其底层是用堆来进行实现的.优先队列中,**队首元素一定是当前队列中优先级最高**的那一个.例如在队列有如下元素,且定义好了优先级

```c++
//此处规定数字越大优先级越高
桃子	(优先级3)
梨子	(优先级4)
苹果	(优先级1)
```

那么出队的顺序为梨子(4)→桃子(3)→苹果(1).

​	当然,可以在任何时候往优先队列里push元素,而优先队列底层的数据结构堆heap会随时调整结构,使得每次的队首元素都是优先级最大的

```c++
#include<queue>
using namespace std;
```

#### 6.6.1 priority_queue定义

```c++
priority_queue<typename> name;	//typename 任意基本数据类型或容器
```

------

#### 6.6.2 priority_queue容器内元素的访问

1. **只能通过top()访问队首元素(堆顶元素)**,优先级最高的元素

```c++
priority_queue<int> q;
for(int i=1;i<=5;i++){
    q.push(i);
}
printf("%d",q.top());//5
```

------

#### 6.6.3 priority_queue常用函数

1. push()

   ```c++
   //push(x)将x压入队列
   priority_queue<int> q;
   for(int i=1;i<=5;i++){
       q.push(i);
   }
   ```

2. top()

   ```c++
   printf("%d",q.top());//5 
   ```

3. pop()

   ```c++
   //令队首元素(堆顶元素)出队
   priority_queue<int> q;
   for(int i=1;i<=5;i++){
       q.push(i);
   }
   printf("%d",q.top());//5
   q.pop();//出队首元素
   printf("%d",q.top());//4
   ```

4. empty()

   ```c++
   //检测queue是否为空,true为空,false为非空
   priority_queue<int> q;
   if(q.empty==ture){
       printf("empty");
   }else{
       printf("not empty")
   }
   q.push(1);
   if(q.empty==ture){
       printf("empty");
   }else{
       printf("not empty")
   }
   //empty
   //not empty
   ```

5. size()

   ```c++
   //返回priority_queue内元素的个数
   priority_queue<int> q;
   for(int i=1;i<=5;i++){
       q.push(i);
   }
   printf("%d",q.size());	//5
   ```

------

#### 6.6.4 priority_queue内元素元素优先级的设置

 1. 基本数据类型的优先级设置

    int型 double型 char 型,默认数字大的/字典序大的优先级高.队首元素为优先队列内元素最大的那个

    ```	c++
    //等价
    priority_queue<int> q;
    priority_queue<int,vector<int>,less<int> > q;
    //第二个参数时来承载底层数据结构堆(heap)的容器,
    //第三个参数是对第一个参数的比较累,less<int>表示数字大的优先级越大,而greater<int>表示数字小的优先级越大
    priority_queue<int,vector<int>,greater<int> > q;
    ```

 2. 结构体的优先级设置

    ```c++
    struct fruit{
        string name;
        int price;
    }
    //希望水果的价格高的为优先级高,就需要重载(overload)小于号"<".重载是指对已有的运算符进行重新定义,也就是改变小于号的功能
    struct fruit{
        string name;
        int price;
        friend bool operator < (fruit f1,fruit f2){
            return f1.price<f2.price;
        }
    }
    //fruit增加了一个函数 friend为友元
    //"bool operator <(fruit f1,fruit f2)"对fruit类型的操作符"<"进行重载
    //f1>f2   f2<f1
    //f1==f2  !(f1<f2)&&!(f2<f1)
    //"return f1.price<f2.price;" 以价格高的水果为优先级高
    ```

    ```c++
    struct fruit{
        string name;
        int price;
        friend bool operator < (fruit f1,fruit f2){
            return f1.price>f2.price;	//价格低的水果优先级高
        }
    }f1,f2,f3
    
    int main(){
    	priority_queue<fruit> q;
    	f1.name="aaa";
    	f1.price=3;
    	f2.name="bbb";
    	f2.price=4;
    	f3.name="ccc";
    	f3.price=1;
    	q.push(f1);
    	q.push(f2);
    	q.push(f3);
    	cout<<q.top().name<<""<<q.top.price<<endl;
    	return 0;
    }
    //苹果1
    ```

    ```c++
    struct fruit{
        string name;
        int price;
    }f1,f2,f3
    
    struct cmp{
        bool operator <(fruit f1,fruit f2){		//去掉friend
            return f1.price>f2.price;	//价格低的水果优先级高
        }
    }
    
    priority_queue<fruit,vector<fruit>,cmp > q;
    ```

    **即便是基本数据类型或者其他STL容器,也可以通过同样的方式来定义优先级.**

    如果结构体内的数据较为庞大(例如出现了字符串或者数组),建议使用引用来提高效率,此时比较类的参数中需要加上"const"和"&"

    ```c++
    friend bool operator < (const fruit &f1,const fruit &f2){
            return f1.price>f2.price;	//价格低的水果优先级高
    }
    
    bool operator () (const fruit &f1,const fruit &f2){
            return f1.price>f2.price;	//价格低的水果优先级高
    }
    ```

#### 6.6.5 priority_queue的常见用途

1. 可以解决一些贪心问题,也可以对dijkstra算法进行优化(因为优先队列的本质是堆)
2. 使用ftop()函数前,必须用empty()判断队列是否为空.

---

### 6.7 stack-栈

​	栈，后进先出的容器

​	当然,可以在任何时候往优先队列里push元素,而优先队列底层的数据结构堆heap会随时调整结构,使得每次的队首元素都是优先级最大的

```c++
#include<stack>
using namespace std;
```

#### 6.7.1 stack定义

```c++
stack<typename> name;	//typename 任意基本数据类型或容器
```

#### 6.7.2 stack容器内元素的访问

1. **只能通过top()访问队首元素(栈顶元素)**

```c++
stack<int> st;
for(int i=1;i<=5;i++){
    st.push(i);
}
printf("%d",st.top());//5
```

#### 6.7.3 stack常用函数

1. push()

   ```c++
   //push(x)将x入栈
   stack<int> st;
   for(int i=1;i<=5;i++){
       st.push(i);
   }
   ```

2. top()

   ```c++
   printf("%d",st.top());//5 
   ```

3. pop()

   ```c++
   //令栈顶元素出队
   stack<int> st;
   for(int i=1;i<=5;i++){
       st.push(i);
   }
   for(int i=1;i<=3;i++){
       st.pop();		//连续三次将栈顶元素出栈 5 4 3 
   }
   printf("%d",st.top());//2
   ```

4. empty()

   ```c++
   //检测stack是否为空,true为空,false为非空
   stack<int> st;
   if(st.empty==ture){
       printf("empty");
   }else{
       printf("not empty")
   }
   st.push(1);
   if(st.empty==ture){
       printf("empty");
   }else{
       printf("not empty")
   }
   //empty
   //not empty
   ```

5. size()

   ```c++
   //返回stack内元素的个数
   stack<int> st;
   for(int i=1;i<=5;i++){
       st.push(i);
   }
   printf("%d",st.size());	//5
   ```

#### 6.7.4 stack的常见用途

1. 用来模拟实现一些递归,防止程序对栈内存的限制而导致程序运行出错.

---

### 6.8 pair

​	pair,当想要将两个元素绑在一起作为一个合成元素,又不想要因此定义结构体时,使用pair可以很方便的作为一个替代品.也就是说,pair实际上可以看作一个内部有两个元素的结构体,且这两个元素的类型是可以指定的.

```c++
struct pair{
    typename1 first;
    typename2 second;
}

#include<utility>   或   #include<map>
using namespace std;
```

#### 6.8.1 pair定义

```c++
pair<typename1,typename2> name;	//typename 任意基本数据类型或容器
//定义参数为string和int类型的pair
pair<string,int> p;
//如果想在定义pair时进行初始化,只需要跟上一个小括号,里面填写两个想要初始化的元素即可
pair<string, int>p("haha",5);

//临时构建一个pair
//将类型定义写在前面,后面用小括号内两个元素的方式
pair<string,int>("haha",5);
//使用自带的make_pair函数
make_pair("haha",5);
```

#### 6.8.2 pair容器内元素的访问

1. pair中只有两个元素,分别是first和second,按正常结构体的方式去访问.

```c++
pair<string,int> p;
p.first="haha";
p.second=5;
cout<<p.first<<" "<<p.second<<endl;
p=make_pair("xixi",55);
cout<<p.first<<" "<<p.second<<endl;
p=pair<string,int>("heihei",555);
cout<<p.first<<" "<<p.second<<endl;

//haha 5
//xixi 55
//heihei 555
```

#### 6.8.3 pair常用函数

​        比较操作数,两个pair类型数据可以直接使用== !=等等比较大小,**先以first的大小作为标准,只有当first相等时才去判别second的大小**

```c++
pair<int,int> p1(5,10);
pair<int,int> p2(5,15);
pair<int,int> p3(10,5);
if(p1<p3) printf("p1<p3\n");
if(p1<=p3) printf("p1<=p3\n");
if(p1<p2) printf("p1<p2\n");
//p1<p3
//p1<=p3
//p1<p2
```

------

#### 6.8.4 pair的常见用途

1. 用来代替二元结构体及其构造函数,可以节省编码时间
2. 作为map的键值对来进行插入,例如下面的例子

```c++
map<string,int> mp;
mp.insert(make_pair("heihei",5));
mp.insert(pair<string,int>("haha",10));
for(map<string,int>::iterator it=mp.begin();it!=mp.begin();it++){
	cout<<it->first<<" "<<it->second<<endl;
}
//haha 10
//heihei 5
```

### 6.9 algorithm头文件下的常用函数

#### 6.9.1 max()、min()和abs()

​	max(x,y)和min(x,y)分别返回x和y中的最大值和最小值，且**参数必须是两个**(可以是浮点数)。如果返回三个数x、y、z的最大值，可以使用max(x,max(y,z))的写法

​	abs(x)返回x的绝对值。注意：x必须是整数，浮点型的绝对值请用math头文件下的fabs

#### 6.9.2  swap()

​	swap(x,y)用来交换x和y的值

```c++
int x=1,y=2;
swap(x,y);
printf("%d %d",x,y);
//2 1
```

#### 6.9.3 reverse()

​	reverse(it,it2)可以将数组指针在[it,it2)之间的元素或容器的迭代器在[it,it2)范围内的元素进行反转。

```c++
int a[10]={10,11,12,13,14,15};
reverse(a.a+4);	//将a[0]~a[3]反转
//printf   13 12 11 10 14 15

string str="abcdefghi";
reverse(str.begin()+2,str.begin()+6);
//printf abfedcghi
```

#### 6.9.4 next_permutation()

​	next_permutation()给出一个序列在全排列中的下一个序列

```c++
123 132 213 231 312 321
```

这样231的下一个序列就是312

```c++
int a[10]={1,2,3};
do{
    printf("%d%d%d\n",a[0],a[1],a[2]);
}while(next_permutation(a,a+3));
//	123
    132
    213
    231
    312
    321
```

#### 6.9.5 fill()	

​	fill()可以把数组或容器中的某一段区间赋为某个相同的值。和memset不同，这里可以给数组类型对应范围中任意值。

```c++
int a[5]={1,2,3,4,5};
fill(a,a+5,233);
//printf 233 233 233 233 233
```

#### 6.9.6 sort()

1. sort的函数形式

```c++
sort(首元素地址(必填),尾元素地址的*下一个地址(必填),比较函数(非必填));
//默认递增
```

 2. 比较函数cmp

    - 基本数据类型排序

      默认从小到大排序，字典序

      ```c++
      bool cmp(int a,int b){
          return a>b;	//当a>b时把a放在b前面
      }
      sort(a,a+4,cmp);//从大到小排序
      ```

    - 结构体类型排序

      ```c++
      struct node{
          int x,y;
      }ssd[10];
      
      bool cmp(node a,node b){
          return a.x>b.x;			//按x值从大到小对结构体数组ssd排序
      }
      
      bool cmp(node a,node b){
          if(a.x!=b.x)	return a.x>b.x;			
          else return a.y<b.y;
          //按x值从大到小对结构体数组ssd排序，若x相等然后再按y从小到大
      }
      
      sort(ssd,ssd+10,cmp);
      ```

    - STL容器排序

      只有**vector、string、deque**是可以用sort的，set、map这种容器都是用红黑树实现的，元素本身有序。

      ```c++
      bool cmp(int a,int b){
          return a>b;	//当a>b时把a放在b前面
      }
      int main(){
          vector<int> vi;
          vi.push_back(3);
          vi.push_back(1);
          vi.push_back(2);
          sort(vi.begin(),vi.begin+3,cmp);
          printf//3 2 1
      }
      ```

      ```c++
      string str[3]={"bbbb","cc","aaa"};
      sort(str,str+3);//将string数组按字典序从小到大输出
      printf//aaa bbbb cc
          
      bool cmp(string str1,string str2){//按string的长度从小到大排序
      	return str1.length()<str2.length();
      }
      printf//cc aaa bbbb
      ```

---

#### 6.9.7 lower_bound()和upper_bound()

​	lower_bound()和upper_bound()需要用在一个**有序**数组或容器中。		

​	lower_bound(first,last,val)用来寻找在数组或容器的[first,last)范围内**第一个值大于等于**val元素的位置，如果是数组，返回该位置的指针；如果是容器，返回该位置迭代器

​	upper_bound(first,last,val)用来寻找在数组或容器的[first,last)范围内**第一个值大于**val元素的位置，如果是数组，返回该位置的指针；如果是容器，返回该位置迭代器

​	如果数组或容器中没有需要寻找的元素，则lower_bound()和upper_bound()均返回可以插入该元素的位置的指针或迭代器(即假设存在该元素时，该元素应当在的位置)

```c++
int a[10]={1,2,2,3,3,3,5,5,5,5};
int *lowerPos=lower_bound(a,a+10,-1);
int *upperPos=upper_bound(a,a+10,-1);
printf("%d %d",lowerPos-a,upperPos-a);//0 0
int *lowerPos=lower_bound(a,a+10,1);
int *upperPos=upper_bound(a,a+10,1);
printf("%d %d",lowerPos-a,upperPos-a);//0 1
int *lowerPos=lower_bound(a,a+10,3);
int *upperPos=upper_bound(a,a+10,3);
printf("%d %d",lowerPos-a,upperPos-a);//3 6
int *lowerPos=lower_bound(a,a+10,4);
int *upperPos=upper_bound(a,a+10,4);
printf("%d %d",lowerPos-a,upperPos-a);//6 6
int *lowerPos=lower_bound(a,a+10,6);
int *upperPos=upper_bound(a,a+10,6);
printf("%d %d",lowerPos-a,upperPos-a);//10 10
```



## 第7章 提高篇(1)——数据结构专题(1)

### 7.1 栈的应用

​	栈（stack）是一种**后进先出**的数据结构。

![1564901240222](pic/1564901240222.png)

​	**后放进的书先拿出**的特点。如果不拿出3号书，就不能拿1、2号书。

​	**栈顶指针**是**始终指向栈的最上方元素**的一个标记。

 1. 当使用数组实现栈时，栈顶指针是一个int型的变量（数组下标从0开始），通常记为TOP。

 2. 而当使用链表实现栈时，则是一个int*型指针。

    栈中没有元素（空栈）时令TOP为-1。

#### 7.1.1 栈的常见操作

 1. 清空(clear)

    ```c++
    //STL中没有实现栈的清空，如果需要实现栈的清空
    while(!st.empty()){
        st.pop();
    }
    //或者直接重新定义一个栈
    ```

    ```c++
    //将栈顶指针TOP置为-1，表示空栈
    void clear(){
        TOP=-1;
    }
    ```

 2. 获取栈内元素个数(size)

    ```c++
    //栈顶指针TOP始终指向栈顶元素，而元素下标从0开始，因此栈内元素数TOP+1
    int size(){
        return TOP+1;
    }
    ```

 3. 判空(empty)

    ```c++
    bool empty(){
        if(TOP==-1) return true;
        else return false;
    }
    ```

 4. 进栈(push)

    ```c++
    //将元素x置为栈顶。TOP+1，再存
    void push(int x){
        st[++TOP]=x;
    }
    ```

 5. 出栈(pop)

    ```c++
    //将栈顶元素出栈		直接将栈顶指针减1
    void pop(){
        TOP--;
    }
    ```

 6. 取栈顶元素(top)

    ```c++
    int top(){
        return st[TOP];
    }
    ```

    **pop()和top()函数必须先使用empty()函数判断栈是否为空**

    

### 7.2 队列的应用

​	队列是一种**先进先出**的数据结构。

![1564904697873](pic/1564904697873.png)

​	队列总是从队尾加入元素，从队首移除元素。一般来说，需要一个**队首指针**front指向**队首元素的前一个位置**，**队尾指针**rear指向**队尾元素**。

1. 当使用数组实现队列时，队首指针和队尾指针是一个int型的变量（数组下标从0开始）。
2. 而当使用链表实现栈时，则是一个int*型指针。

![1564905051112](pic/1564905051112.png)

**pop()、back()和front()函数必须先使用empty()函数判断队列是否为空**

### 7.3 链表

#### 7.3.1 链表的概念

​	线性表，顺序表和链表。顺序表可以简单地理解成前面介绍的“数组”概念。

​	按正常方式定义一个数组时，计算机会从内存中取出一块连续的地址来存放给定长度的数组；而链表则由若干个结点组成（每个结点代表一个元素），且结点的存储位置不连续。

```c++
struct node{
    typename data;
    node* next;
};
```

​	链表分为**带头结点**的链表和**不带头结点**的链表。头结点head，且数据域data不存放数据，指针域next指向第一个数据域有内容的结点。尾结点，指针域next指向NULL-空地址。

#### 7.3.2 链表节点分配内存空间

1. malloc函数

   ```c++
   typename* p=(typename*)malloc(sizeof(typename));
   
   int* p=(int*)malloc(sizeof(int));//p为指向这块空间的指针变量
   ```

2. new运算符

   ```c++
   //申请动态空间的运算符,返回同变量类型的指针
   typename *p = new typename;
   
   int* p=new int;
   node *p=new node;
   ```

3. 内存泄露

   - free函数

   ```c++
   //释放指针变量p所指向的内存空间 ；将p指向空地址NULL
   //对应malloc
   free(p);
   ```

   - delete运算符

   ```c++
   //同free
   //对应new
   delete(p);
   ```

     [malloc函数域new函数的区别](https://www.cnblogs.com/shilinnpu/p/8945637.html)

#### 7.3.3 链表的基本操作

 1. 创建链表

    ```c++
    node* node1=new node;
    node* node2=new node;
    node* node3=new node;
    node* node4=new node;
    node* node5=new node;
    node1->data=5;
    node1->next=node2;
    node1->data=2;
    node1->next=node3;
    node1->data=5;
    node1->next=node4;
    node1->data=1;
    node1->next=node5;
    node1->data=4;
    node1->next=NULL;
    ```

    ```c++
    struct node{
        int data;
        node* next;
    };
    node* create(int array[]){
        node *p, *pre, *head;//pre当前结点的前驱结点  head为头结点
        head=new node;
        head->next=NULL;//初始化为null
       	pre=head;
        for(int i=0;i<5;i++){
            p= new node;
            p->data=array[i];
            p->next=null;
            pre->next=p;
            pre=p;
        }
        return head;
    }
    
    int main(){
        int array[5]={5,3,6,1,2};
        node* L=create(array);
        L=L->next;
        while(L!=NULL){
            printf("%d",L->data);
            L=L->next;
        }
    }
    ```

 2. 查找元素

    ```c++
    int search(node* head,int x){
        int count=0;
        node* p=head->next;
        while(p!=NULL){
            if(p->data == x){
                count++;
            }
            p=p->next;
        }
        return count;
    }
    ```

 3. 插入元素

    ```c++
    //将x插入以head为头结点的链表的第pos个位置上
    void insert(node* head,int pos,int x){
        node* p=head;
        for(int i=0;i<pos-1;i++){
            p=p->next;	//pos-1为了到插入位置的前一个结点
        }
        node* q=new node;
        q->data=x;
        q->next=p->next;
        p->next=q;
    }
    ```

    **必须**先把新结点的指针域next指向后继节点，才能把所在结点的指针域指向新结点的地址。

    ![1564923596958](pic/1564923596958.png)

 4. 删除元素

    ```c++
    //删除以head为头结点的链表中所有数据域为x的结点
    void delete(node* head,int x){
        node* p=head->next;
        node* pre=head;//pre始终保存p的前驱结点指针
        while(p!=NULL){
            if(p->data==x){
                pre->next=p->next;
                delete(p);
            }else{
                pre=p;
                p=p->next;
            }
        }
    }
    ```

    ![1564923749348](pic/1564923749348.png)

    ![1564923777597](pic/1564923777597.png)

#### 7.3.4 静态链表

​	对于有些问题来说，结点的地址是比较小的整数(5位数的地址)，没有必要建立动态链表，应该使用静态链表。

​	静态链表的实现原理是hash，即通过建立一个结构体数组，并令数组的下标直接表示结点的地址，来达到直接访问数组中的元素。**不需要**头结点

```c++
struct Node(){
    typename data;//数据域
    int next;//指针域
}node[size];
//结构体类型名和结构体变量名设成了不同的名字
node[11111]=22222;
node[22222]=33333;
node[33333]=-1;//-1==NULL
```

#### 7.3.5 静态链表模板

1. 定义静态链表

   ```c++
   struct Node{
       int address;	//结点地址
       typename data;	//数据域
       int next;		//指针域
       xxx;			//结点的某个性质，例如是否为链表的一个结点
   }node[100010];
   ```

2. 静态链表初始化

   ```c++
   //初始化为正常情况下达不到的数字
   for (int i = 0; i < maxn;i++) {
   		node[i].XXX = false;
   }
   ```

3. 遍历链表，进行标记

   ```c++
   int p=begin,count=0;
   while(p!=1){
   	XXX=1;
       count++;
   	p=node[p]->next;
   }
   ```

4. 可控的访问有效结点

   ```c++
   //对数组排序以把有效节点移到数组左端 这样就可以使用count
   //利用XXX的值
   bool cmp(node a,node b){
       if(a.xxx==-1 || b.xxx==-1){
           return a.xxx>b.xxx;  //从大到小 有效结点全部到数组的左端
       }else{
           //二级排序
       }
   }
   ```

5. 按照结点的性质进行排序

---

## 第8章 提高篇(2)——搜索专题

### 8.1 深度优先搜索(DFS)

​	当碰到岔路口时，总是以**“深度”**作为前进的关键词，不碰到死胡同就不回头。

​	深度优先搜索会走遍所有路径，并且每次走到死胡同就代表一条完整路径的形成。

​	深度优先搜索是一种**枚举所有完整路径以遍历所有情况**的搜索方法。

​	过程和出栈入栈的过程很相似。

​	递归实现、Fibonacci数列，递归中的**递归式**F(n+1)、F(n+2)就是岔道口，而**递归边界**F(0)、F(1)就是死胡同。

​	使用递归可以很好的实现深度优先搜索，是方法之一。

#### 案例1

```
	有n件物品，每件物品的重量为w[i]，价值为c[i]。现在需要选出若干件物品放入一个容器为V的背包中，使得在选入背包的物品重量和不超过容量V的前提下，让背包中物品的价值之和最大，求最大价值（1<=n<=20）
```

```c++
void DFS(int index,int sumW,int sumC){...}
//index 物品编号    sunW总重量 sumC总价值

//如果不放入index号物品，那么sumW和sumC不变，
//接下来处理index+1号物品，DFS(index+1,sumW,sumC);
//如果放入index号物品，那么sunW+w[index];sumC+c[index];
//接着处理index+1号物品，DFS(index+1,sumW+w[index],sumC+c[index]);
```

​	一旦index增长到了n，则说明已经把n件物品处理完毕（物品下标0到n-1），刺实记录的sumW和sumC就是所选物品的总重量和总价值。如果sumW不超过V且sumC等于一个全局的记录最大总价值的变量maxValue，sumC更新maxValue

```c++
const int maxn=30;
int n,V,maxvalue=0;
int w[maxn],c[maxn];

void DFS(int index,int sunW,int sumC){
    if(index ==n){
        if(sumW<=V && sumC >maxValue){
            maxValue=sumC;
        }
        return;
    }
    DFS(index+1,sumW,sumC);
    DFS(index+1,sumW+w[index],sumC+c[index]);
}

int main(){
    scanf("%d%d",&n,&V);
    for(int i=0;i<n;i++){
        scanf("%d",&w[i]);
    }
    for(int i=0;i<n;i++){
        scanf("%d",&c[i]);
    }
    DFS(0,0,0);
}
```

​    可以注意到，由于每件物品都有两种选择。可以通过对算法的优化，来使其在随机数据的表现上有更好的效率。可以把sumW的判断加入"岔道口"中，只有当`sumW<=V`时才进入岔道，条件放在前一岔道的末尾，即岔道口判断

```c++
void DFS(int index,int sunW,int sumC){
    if(index ==n){
    	return;
    }
    DFS(index+1,sumW,sumC);
    if(sumW+ w[index] <=V){		//加入物品后是否超过容量V
        if(sumC+c[index]>ans){
            ans=sumC+c[index];
        }
        DFS(index+1,sumW+w[index],sumC+c[index]);
    }
}
```

​	通过题目条件的限制来节省DFS计算量的方法称为**剪枝**

#### 案例2

```
给定N个整数，从中选择K个数，使得这K个数之和恰好等于一个给定的整数X；如果有多种方案，选择它们中元素平方和最大的一个
```

 ```c++
void(DFS)(int index,int nowK,int sum,int sumSqu){...}
//整数编号index  nowK记录当前已经选择的数的个数  sum和 sumsqu平方和

//序列A中n个数选k个数使得和为x，最大平方和maxsumsqu
int n,k,x,maxSumSqu=-1,A[maxn];
//temp放临时方案，ans放最优方案
vector<int> temp,ans;
//整数编号index  nowK记录当前已经选择的数的个数  sum和 sumsqu平方和
void DFS(int index,int nowK,int sum,int sumSqu){
	if(nowK==k && sum==x){		//找到k个数的和为x
        if(sumSqu>maxSumSqu){	//如果比当前找到的更优
            maxSumSqu=sumSqu;	//更新最大平方和
            ans=temp;			//更新最优方案
        }
    }
    //已经处理完n个数，或者超过k个数，或者和超过x，返回
    if(index ==n || nowK>k || sum>x ) return;
    //选index号数
    temp.push_back(A[index]);
    DFS(index+1,nowK+1,sum+A[index],sumSqu+A[index]*A[index]);
    temp.pop_back();
    //不选index号数
    DFS(index+1,nowK,sum,sumSqu);
}
 ```

​	**如果每一个数都可以被选择多次**，修改选index号数下的语句

```c++
DFS(index+1,nowK+1,sum+A[index],sumSqu+A[index]*A[index]);
DFS(index,nowK+1,sum+A[index],sumSqu+A[index]*A[index]);
```

---

### 8.2 广度优选搜索(BFS)

​	当碰到岔道口，总是**优先依次访问从该岔道口能直接到达的所有结点**，然后再按这些结点被访问的顺序去依次访问它们能**直接到达**的所有结点。

![1564974860679](pic/1564974860679.png)

​	可用**队列**入队、出队实现。

#### 模板

```c++
void BFS(int s){
    queue<int> q;
    q.push(s);//起点入队
    while(!q.empty()){
        取出队首元素top;
        访问队首元素top;
        将队首元素出队;
        将top的下一层结点中未曾入队的结点全部入队，标记为now的层号加1,并设置为已入队;
    }
}
```

#### 案例1

![1564987764366](pic/1564987764366.png)

```c++
//枚举每一个位置的元素，如果0，跳过；如果1，使用BFS查询与该位置相邻的4个位置（不出界），判断它们是否为1.
//设置bool型数组inq记录每个位置是否在BFS已入过队
对当前位置(x,y)来说，由于与其相邻的四个位置，设置增量数组
int X[]={0,0,1,-1};
int Y[]={1,-1,0,0};
//确定相邻的四个位置
for(int i=0;i<4;i++){
    newX=newX+X[i];
    newY=newY+Y[i];
}
```

```c++
const int maxn=100;
struct node{
    int x,y
}Node;

int n,m;
int matrix[maxn][maxn];
bool inq[maxn][maxn]={false};//记录位置（x，y）是否已经入队
int X[4]={0,0,1,-1};
int Y[4]={1,-1,0,0};

bool judge(int x,int y){
    //越界返回false
    if(x>n || x<0 || y>m || y<0) return false;
    //当前位置为0，或者已入队
    if(matrix[x][y] == 0 || inq[x][y] ==true) return false;
    return true;
}

//BFS函数访问位置（x,y）所在的块，将该块中所有“1”的inq置为true
void BFS(int x,int y){
    queue<node> Q;
    Node.x=x,Node.y=y;//当前结点坐标
    Q.push(Node);//入队
    inq[x][y]=true;				//设置（x，y）已入队
    while(!Q.empty()){
        node top=Q.front();   //取出队首元素
        Q.pop();			//队首元素出队
        for(int i=0;i<4;i++){
            int newX=newX+X[i];
            int newY=newY+Y[i];
            if(judge(newX,newY)){	//如果新位置需要访问
                Node.x=newX,Node.y=newY;
                Q.push(Node);
                inq[newX][newY]=true;	
            }
        }
    }
}

int main(){
    scanf("%d%d",&n,&m);
    for(int x=0;x<n;x++){
        for(int y=0;y<m;y++){
        	scanf("%d",&matrix[x][y]);	//读入01矩阵
        }
    }
    int ans=0;
    for(int x=0;x<n;x++){
        for(int y=0;y<m;y++){
        	if(matrix[x][y]==1 && inq[x][y] == false){
                ans++;
                BFS(x,y);
            }
        }
    }
    printf("%d\n",ans);
    return 0;
}
6 7
0 1 1 1 0 0 1
0 0 1 0 0 0 0
0 0 0 0 1 0 0 
0 0 0 1 1 1 0
1 1 1 0 1 0 0
1 1 1 1 0 0 0
```

#### 案例2

```
给定一个n*m大小的迷宫，其中*代表不可通过的墙壁，而“.”代表平地，S表示起点，T表示终点。移动过程中，如果当前位置是(x,y)（下标从0开始），且每次只能前往上下左右四个位置的平地，求从起点S到大终点T的最少步数
                            .....
                            .*.*.
                            .*S*.
                            .***.
                            ...T*
S(2,2)   T(4,3)
```

```c++
//BFS通过层次的顺序来遍历的
bool test(int x, int y) {
	if (x<0 || y<0 || x>n || y > m) return false;
	if (maze[x][y] == '*') return false;
	if (inq[x][y] == true) return false;
	return true;
}

int BFS() {
	queue<node> q;
	q.push(S);
	while (!q.empty()) {
		node top = q.front();
		q.pop();
		if (top.x == T.x && top.y == T.y) {
			return top.step;
		}
		for (int i = 0; i < 4; i++) {
			int newX = top.x + X[i];
			int newY = top.y + Y[i];
			if (test(newX, newY)) {
				Node.x = newX, Node.y = newY;
				Node.step = top.step;
				q.push(Node);
				inq[newX][newY] = true;
			}
		}
	}
	return -1;
}
```

​	inq数组的含义是判断结点**是否已入过队**，而不是结点是否已被访问

​	当需要对队列中的元素进行修改而不仅仅是访问时，队列中存放的元素最好不要是元素本身，而是它们的编号，或下标

```c++
struct node{
    int data
}a[10];

int main(){
    queue<int> q;
    for(int i=1;i<=3;i++){
    	a[i].data=i;
        q.push(i);
    }
    a[q.front()].data=100;
    pritnf("%d\n",a[1].data);	//100
}
```



## 第9章 提高篇(3)——数据结构专题(2)

### 9.1 树与二叉树

#### 9.1.1 树的定义与性质	

​	树是用来**概括传递关系**的一种数据结构。

​	为了简化，把树枝分叉处、树叶、树根抽象为**结点**(node)；

​	其中树根抽象为**根结点**(root)，且对一棵树来说存在一个根节点(最上方)；

​	树叶概括为**叶子结点**(leaf)，且叶子结点不再延伸新的结点(最下方)；

​	茎干和树枝称为**边**(edge)，且一条边只用来连接两个结点(一个端点一个)。

​	由若干个结点和若干条边组成的数据结构，且在树中的结点不能被边连接成环。

​	数据结构中，根结点位于最上方，向下延伸出若干条边到达**子节点**(child)（从而向下形成**子树**(subtree)），而子节点又向下延伸出边并连接一些结点，直至叶子结点

实用的概念和性质

- 树可以没有结点，**空树**(empty tree)
- 树的**层次(layer)**从根结点开始算起，即根结点为第一层，根结点子树的根结点为第二层
- 把结点的子树棵树称为结点的**度(degree)**，树中结点的最大的度称为树的度(也称为树的宽度)
- 一条边连接两个结点，树中不存在环，因此对有n个结点的树，边数一定是n-1.且**满足连通、边数等于顶点数-1的结构一定是一颗树**。
- 叶子结点被定义为度为0的结点，因此当树只有一个结点（即只有根结点）时，根结点也算叶子结点
- 结点的**深度(depth)**是指从根节点(深度为1)开始**自顶向下**逐层累加至该结点时的深度值；结点的**高度(height)**是指从最底层叶子结点(高度为1)开始**自底向上**逐层累加至该结点时的高度值。**树的深度是指树中结点的最大深度**，树的最大高度。对树而言，**深度和高度是相等的**。
- 多颗树组合在一起称为**森林(forest)**，森林是若干颗树的集合

#### 9.1.2 二叉树的递归定义

自身定义自身-递归定义

 - 要么二叉树没有根节点，是一颗空树

 - 要么二叉树由根结点、左子树、右子树组成，且左子树和右子树都是二叉树

   二叉树与度为2的树的区别：二叉树的**左右子树严格区分**

两种特殊的二叉树：

- 满二叉树：每一层的结点个数都达到了当层能达到的最大结点数。
- 完全二叉树：除了最下面一层以外，其余曾的结点个数都达到了当层能达到的最大结点数，且最下面一层只从左至右连续存在若干结点，而这些连续结点右边的结点全部不存在。

#### 9.1.3 二叉树的存储结构与基本操作

1. 二叉树的存储结构

   ```c++
   //使用链表
   struct node{
       typename data;	//数据域
       node* lchild;	//指向左子树根结点的指针
       node* rchild;	//指向右子树根节点的指针
   };
   //而二叉树建树前根结点不存在，因此其地址一般设为NULL
   node* root=NULL;
   ```

   ```c++
   //生成新结点，v为结点权值
   node* newNode(int v){
       node* Node=new node;	//申请一个node型变量的地址空间
       Node->data=v;			//结点权值为v
       Node->lchild=Node->rchild=NULL;//初始状态下没有左右孩子！！！！
       return Node;			//返回新建结点的地址
   }
   ```

2. 二叉树结点的查找、修改

   **查找**操作是指在给定数据域的条件下，在二叉树中找到所有数据域为给定数据域的结点，并将它们的数据域**修改**为给定的数据域。

   需要使用递归来完成查找修改操作。**递归式**是对当前结点的左子树和右子树分别递归，**递归边界**是当前结点为空时到达死胡同。

   ```c++
   void search(node* root,int x,int newdata){
       if(root == NULL){
           return;			//空树，死胡同(递归边界)
       }
       if(root->data == x){//找到数据域为x的结点，把他修改成newdata
           root->data=newdata;
       }
       search(root->lchild,x,newdata);//往左子树搜索x
       search(root->rchild,x,newdata);
   }
   ```

3.  二叉树结点的插入

   二叉树结点的插入位置就是数据域在二叉树中查找失败的位置。

   ```c++
   //insert函数将在二叉树中插入一个数据域为x的新结点
   //注意根结点指针root要使用引用，否则插入不会成功
   void insert(node* &root,int x){	//根结点指针node*型 root使用引用&
       if(root==NULL){		//空树，查找失败，即插入位置（递归边界）
           root=newNode(x);
           return;
       }
       if(由二叉树的性质，x应该插在左子树){
       	insert(root->lchild,x);//往左子树搜索-递归式
       }else{
           insert(root->rchild,x);//往右子树搜索-递归式
       }
   }
   //insert需要修改指针，根结点指针node*型 root使用引用& 
   //search不需要修改指针，修改指针指向的内容
   
   ```

   如果函数中需要**新建结点**，即对二叉树的**结构做出修改**，就需要**加引用**；如果只是**修改当前已有结点的内容**，或仅仅是**遍历树**，就**不用加引用**。都试一下

4. 二叉树的创建

   就是二叉树结点的插入过程，把需要插入的数据存储在数组中，然后再将它们使用insert函数一个个插入二叉树中，并最终返回根结点的指针root。

   ```c++
   //二叉树的建立
   node* Create(int data[],int n){
       node* root=NULL;	//新建空根节点root
       for(int i=0;i<n;i++){
           insert(root,data[i]);	//将data[0]~data[n-1]插入二叉树中
       }
       return root;//返回根结点
   }
   ```

5. 二叉树存储结构图示

   ​	左边**概念意义**的二叉树在使用二叉链表存储之后形成了箭头右边的图。对每个结点，第一个部分是数据域，数据域后面紧跟两个指针域，用以存放左子树根结点的地址和右子树根结点的地址。如果某棵子树是空树，那么显然也就不存在根结点，其地址就是NULL，表示不存在这个结点。

   ![1564997118826](pic/1564997118826.png)

   ​	递归时，总是往左子树根结点和右子树根结点递归。如果子树是空树，那么root一定是NULL，表示这个结点不存在。

   root==null 和*root==null的区别，也即结点**地址**为NULL与结点**内容**为NULL的区别（**结点不存在与结点存在但没有内容**的区别）

6. 完全二叉树的存储结构

   ​	对完全二叉树当中的任何一个结点(设编号为x)，其左孩子的编号一定是2x,而右孩子的编号一定是2x+1。也就是说可以通过建立一个大小为2^k的数组来存放所有结点的信息，其中k为完全二叉树的最大高度，且**1号位存放的必须是根结点**。

   ​	如果不是完全二叉树，可以将其视为完全二叉树，即把空结点也进行实际的编号工作。但是这样会使整棵树是一条链时的空间消耗巨大。

   ​	**该数组中元素存放的顺序恰好为该完全二叉树的层序遍历序列**。

   ​	判断某个结点是否为叶结点的标志为：**该结点（记下标为root）的左子结点的编号root*2大于结点总个数**；

   ​	判断某个结点是否为空结点的标志：**该结点下标root大于结点总个数n**

---

### 9.2 二叉树的遍历 

​	四种遍历：先序遍历、中序遍历、后序遍历及层次遍历。前三种一般使用深度优先搜索（DFS）实现，而层次遍历一般用广度优先搜索（BFS）实现。

​	”先中后“序遍历只针对根结点root在遍历中的位置，左子树总是一定先于右子树遍历。

```c++
//先序 根结点→左子树→右子树
//中序 左子树→根结点→右子树
//后序 左子树→右子树→根结点
```

**无论是先序遍历序列还是后序遍历序列，都必须知道中序遍历序列才能唯一的确定一棵树**

#### 9.2.1 先序遍历-根左右

 1. 先序遍历的实现

    ```C++
    void preorder(node* root){
        if(root==NULL){
            return;	//到达空树，递归边界
        }
        //访问根结点root，将其数据域输出
        printf("%d\n",root->data);
        //访问左子树
        preorder(root->lchild);
        //访问右子树
        preorder(root->rchild);
    }
    ```

    ![1565007172007](pic/1565007172007.png)

    - 首先对整棵树，根结点是A，左子树和右子树图中已经标出。按照先序遍历的定义，需要先访问根结点，因此输出A。之后，先访问左子树的所有结点，然后再去访问右子树的**所有结点**。
    - 于是访问A的左子树，即B、D、E结点。同样，对树进行先序遍历。根结点为B，因此输出B。再访问B的左右子树。
    - 访问B的左子树，此时根结点为D，因此输出D。之后访问D的左子树，D的左子树的根结点为NULL而到达递归边界(root==NULL),于是D的左子树访问完毕。接着访问D的右子树，同样到达递归边界，D的右子树访问完毕。B的左子树访问完毕
    - 接下来访问B的右子树，此时根结点为E，同D。B的右子树访问完毕，A的左子树访问完毕
    - 继续访问A的右子树
    - 最后求得先序遍历序列为ABDECF

 2. 先序遍历序列的性质

    对一颗二叉树的先序遍历序列，**序列的第一个一定是根结点**。

---

#### 9.2.2 中序遍历-左根右

1. 中序遍历的实现

   ```c++
   void inorder(node* root){
       if(root==NULL){
           return;	//到达空树，递归边界
       }
       //访问左子树
       preorder(root->lchild);
       //访问根结点root，将其数据域输出
       printf("%d\n",root->data);
       //访问右子树
       preorder(root->rchild);
   }
   ```

   中序遍历序列为DBEACF

2. 中序遍历序列的性质

   **只要知道根结点，就可以通过根结点在中序遍历序列中的位置区分出左子树和右子树**。

---

#### 9.2.3 后序遍历-左右根

1. 后序遍历的实现

   ```c++
   void postorder(node* root){
       if(root==NULL){
           return;	//到达空树，递归边界
       }
       //访问左子树
       postorder(root->lchild);
       //访问右子树
       postorder(root->rchild);
       //访问根结点root，将其数据域输出
       printf("%d\n",root->data);
       
   }
   ```

   后序遍历序列为DEBFCA

2. 后序遍历序列的性质

   - **序列的最后一个一定是根结点**

#### 9.2.4 层序遍历

​	按层次的顺序从根结点向下逐层进行遍历，且对同一层的结点为从左到右的遍历。

![1565008413057](pic/1565008413057.png)

​	层序遍历序列为ABCDEF

​	过程和BFS很像，因为BFS总是以广度为第一关键词，而对应到二叉树中广度又恰好体现在层次上，因此层次遍历就相当于是对二叉树从根结点开始的广度优先搜索。

![1565008517173](pic/1565008517173.png)

```c++
//层序遍历
void layerorder(node* root){	//队列中存放node型变量的地址，通过访问地址修改原元素
    queue<node*> q;		//注意队列里是存地址
    q.push(root);		//将根结点地址入队
    while(!q.empty()){
        node* now=q.front();	//取出队首元素
        q.pop();
        printf("%d",now->data);	//访问队首元素
        if(now->lchild!=NULL) q.push(now->lchild);//左子树非空
        if(now->rchild!=NULL) q.push(now->rchild);//右子树非空
    }
}

struct node{
    int data;
    int layer;		//层次
    node* lchild;
    node* rchild;
};
void layerorder(node* root){	//队列中存放node型变量的地址，通过访问地址修改原元素
    queue<node*> q;		//注意队列里是存地址
    root->layer=1;
    q.push(root);		//将根结点地址入队
    while(!q.empty()){
        node* now=q.front();	//取出队首元素
        q.pop();
        printf("%d",now->data);	//访问队首元素
        if(now->lchild!=NULL) {
            now->lchild->layer=now->layer+1;
            q.push(now->lchild);
        }//左子树非空
        if(now->rchild!=NULL) {
          	now->rchild->layer=now->layer+1;
            q.push(now->rchild);//右子树非空
        }
    }
}
```

#### 9.2.5 重建二叉树

​	**给定一个二叉树的先序遍历序列和中序遍历序列，重建这颗二叉树**

```c++
已知先序序列为pre1、pre2、pre3、……、pren
中序序列为in1、in2、……、inn.
那么由先序序列的性质可知，先序序列的第一个元素pre1是但前二叉树的根结点，再由中序序列的性质可知，当前二叉树的根结点将中序序列划分为左子树和右子树。

```

```c++
//当前先序序列区间为[preL,preR]，中序序列区间为[inL,inR]，返回根结点地址
node* create(int preL,int preR,int inL,int inR){
    if(preL>preR){	//先序序列长度小于等于0
        return NULL;
    }
    node* root=new node;//新建一个新的结点，用来存放当前二叉树的根结点
    root->data=pre[preL];//新结点的数据域为根结点的值
    int k;
    for(k=inL;k<=inR;k++){
        if(in[k] == pre[preL]){
            break;
        }
    }
    int numLetft=k-inL;
    
    //左子树的先序区间为[preL+1,preL+numLeft],中序为[inL,k-1]
    //返回左子树的根结点地址，赋值给root的左指针
    root->lchild=create(preL+1,preL+numLeft,inL,k-1);
    
    //右子树的先序区间为[preL+numLeft+1,preR],中序为[k+1,inR]
    //返回右子树的根结点地址，赋值给root的右指针
    root->rchild=create(preL+numLeft+1,preR,k+1,inR);
    
}
```

---

#### 9.2.6 二叉树的静态实现

​	二叉树的定义中，为了能够实时控制新生成结点的个数，结构体node中的左右指针域都使用了指针。

​	**静态二叉链表**是指，结点的左右指针使用int型代替，用来表示左右子树的根结点在数组中的下标。建立一个大小为**结点上限个数**的node型数组，所有动态生成的结点都直接使用数组中的结点，所有对指针的操作都改为对数组下标的访问。

```c++
struct node{
    typename data;	//数据域
    int lchild;		//指向左子树的指针域
    int rchild;		//指向右子树的指针域
}Node[maxn];		//结点数组，maxn为结点上限个数
```

```c++
//静态指定
int index=0;
int newNode(int v){			//分配一个Node数组中的结点给新的结点，index为下标
    Node[index].data=v;		//数据域为v
    Node[index].lchild=-1;	//以-1或maxn表示空，因为数组范围使0~maxn-1
    Node[index].rchild=-1;
    return index++;
}
```

```c++
//查找，root为根结点在数组中的下标
void search(int root,int x,int newdata){
    if(root==-1){
        return;
    }
    if(Node[root].data==x){
        Node[root].data=newdata;
    }
    search(Node[root].lchild,x,newdata);	//往左子树搜索x（递归式）
    search(Node[root].rchild,x,newdata);	//往右子树搜索x（递归式）
}

//插入，root为根结点在数组中的下标
void insert(int &root,int x){//加引用
    if(root==-1){
        root=newNode(x);
        return;
    }
    if(由二叉树的性质x应该插在左子树){
        insert(Node[root].lchild,x,newdata);//往左子树搜索x（递归式）
    }else{
        insert(Node[root].rchild,x,newdata);//往右子树搜索x（递归式）
    }
}

//二叉树的建立，函数返回根结点root的下标
int Create(int data[],int n){
    int root=-1;	//新建根结点
    for(int i=0;i<n;i++){
        insert(root,data[i]);	//将data[0]~data[n-1]插入二叉树中
    }
    return root;	//返回二叉树的根结点下标
}

```

关于二叉树的先序、中序、后序、层序遍历进行相应的转换

```c++
//先序遍历
void preorder(int root){
    if(root==-1){
        return;	//到达空树，递归边界
    }
    //访问根结点root，将其数据域输出
    printf("%d\n",Node[root].data);
    //访问左子树
    preorder(Node[root].lchild);
    //访问右子树
    preorder(Node[root].rchild);
}

//中序遍历
void inorder(int root){
    if(root==-1){
        return;	//到达空树，递归边界
    }
    //访问左子树
    preorder(Node[root].lchild);
    //访问根结点root，将其数据域输出
    printf("%d\n",Node[root].data);
    //访问右子树
    preorder(Node[root].rchild);
}

//后序遍历
void postorder(int root){
    if(root==-1){
        return;	//到达空树，递归边界
    }
    //访问左子树
    preorder(Node[root].lchild);
    //访问右子树
    preorder(Node[root].rchild);
    //访问根结点root，将其数据域输出
    printf("%d\n",Node[root].data);   
}

//层序遍历
void layerorder(int root){	//队列中存放node型变量的地址，通过访问地址修改原元素
    queue<int> q;		//注意队列里是存地址
    q.push(root);		//将根结点地址入队
    while(!q.empty()){
        int now=q.front();	//取出队首元素
        q.pop();
        printf("%d",Node[root].data);	//访问队首元素
        if(Node[root].lchild!=NULL) q.push(Node[root].lchild);//左子树非空
        if(Node[root].rchild!=NULL) q.push(Node[root].rchild);//右子树非空
    }
}
```

---

### 9.3 树的遍历

#### 9.3.1 树的静态写法

​	一般意义上的树，子结点个数不限且子结点没有先后次序的树，不是上文讨论的二叉树。

​	二叉树的结点的定义，可以注意到它是由数据域和指针域组成的。普通树，指针域存放其所有子结点的地址

```c++
struct node{
    typename data;	//数据域
    vector child;	//指针域,存放所有子结点的下标
}Node[maxn];		//结点数组，maxn为结点上限个数
```

```c++
//新建结点
int index=0;
int newNode(int v){
    Node[index].data=v;			//数据域为v
    Node[index].child.clear();	//清空子结点
    return index++;
}
```

![1565100594061](pic/1565100594061.png)

![1565100610723](pic/1565100610723.png)



#### 9.3.2 树的先根遍历

​	序列为V0145236

```c++
void preorder(int root){
    printf("%d ",Node[root].data);//访问当前结点
    for(int i=0;i<Node[root].child.seiz();i++){
        PreOrder(Node[root].child[i]);	//递归访问结点root的所有子结点
    }
}
```



#### 9.3.3 树的层序遍历

​	序列V0123456

```c++
//1
void LayerOrder(int root){
    queue<int> Q;
    q.push(root);
    while(!Q.empty()){
        int front=Q.front();
        printf("%d ",Node[root].data);
        Q.pop();
        for(int i=0;i<Node[front].child.size();i++){
            Q.push(Node[front].child[i]);
        }
    }
}
//如果需要对结点的层号进行求解，只需要在结构体node的定义中增加变量来记录层号
struct node{
    int layer;		//记录层号
    typename data;	//数据域
    vector child;	//指针域,存放所有子结点的下标
}Node[maxn];		//结点数组，maxn为结点上限个数

//更新后
void LayerOrder(int root){
    queue<int> Q;
    Q.push(root);
    Node[root].layer=0;
    while(!Q.empty()){
        int front=Q.front();
        printf("%d ",Node[root].data);
        Q.pop();
        for(int i=0;i<Node[front].child.size();i++){
            int child=Node[front].child[i];
            Node[child].layer=Node[front].layer+1;
            Q.push(child);	//将当前结点的所有子结点入队
        }
    }
}
```

---

#### 9.3.4 从树的遍历看DFS与BFS

1. 深度优先搜索与先根遍历

   ​	对**所有合法的DFS求解过程**，都可以把它**画成树的形式**，死胡同等价于树中的叶子节点，而岔道口等价于树中的非叶子结点，并且对这棵树的DFS遍历过程就是树的先根遍历的过程。

   ​	碰到一些可以用DFS做的题目，就把一些**状态**作为树的结点，问题转换为直观的对树进行**先根遍历**的问题。如果想要找到树的某些信息，可以借用DFS以**深度**作为第一关键词的思想来**对结点进行遍历**，以获得所需的结果。例如求解叶子结点的带权路径和（即从根结点到叶子结点的路径上的结点点权之和）时就可以把到达**死胡同**作为一条**路径结束的判断**。

   ​	剪枝，要**保证剪枝的正确性**。

2. 广度优先搜索与层序遍历

   ​	将迷宫的岔道口和死胡同都简化为结点，将迷宫的结构转换为树。如果模仿**层序遍历**的方法来遍历这棵树，就可以得到BFS过程得到的序列。对所有合法的**BFS求解过程**，都可以像DFS中那样画出一棵树，并且将广度优先搜索问题转换为树的层序遍历的问题。

---

### 9.4 二叉查找树(BST)

#### 9.4.1 定义

​	二叉查找树是一种特殊的二叉树，又称排序二叉树、二叉搜索树、二叉排序树。

​	递归定义：

​	1. 二叉查找树是一个颗空树

​	2. 二叉查找树由**根结点、左子树、右子树**组成，其中**左子树和右子树**都是二叉查找树，且左子树上所有结点的数据域均**小于或等于**根结点的数据域，右子树上所有结点的数据域**均大于**根结点的数据域。

​	二叉查找树实际上是一颗**数据域有序**的二叉树。

#### 9.4.2 二叉查找树的基本操作

​	二叉查找树的基本操作有查找、插入、建树、删除。

1. **查找操作**

   ​	二叉查找树的性质决定了可以只选择其中一颗子树进行遍历，因此查找将会是从树根到查找结点的一条**路径**。

   ```c++
   //查找二叉查找树中数据域为x的结点
   void search(node* root,int x){
       if(root==NULL){	//空树，查找失败
           printf("search failed\n");
           return;
       }
       if(x==root->data){
           pritnf("%d\n",root->data);
       }else if(x<root->data){	//如果x比根结点的数据域小，说明x在左子树
           search(root->lchild,x);
       }else{
           search(root->rchild,x);
       }
   }
   ```

   ​    和普通二叉树的查找函数不同,二叉查找树的查找在于对左右子树的选择递归。在普通二叉树中,无法确定需要查找的值x到底是在左子树还是右子树,但是在二叉查找树中就可以确定,因为二叉查找树中的**数据域顺序总是左子树<根结点<右子树**。

2. **插入操作**

   ​	当对某个需要查找的值在二叉查找树中查找成功，说明结点已经存在；如果需要查找的值在BFT中查找失败，则失败的地方一定是结点需要插入的地方。可以在查找的基础上，在root==NULL时新建需要插入的结点。

   ```c++
   //使用链表
   struct node{
       typename data;	//数据域
       node* lchild;	//指向左子树根结点的指针
       node* rchild;	//指向右子树根节点的指针
   };
   //而二叉树建树前根结点不存在，因此其地址一般设为NULL
   node* root=NULL;
   
   
   //生成新结点，v为结点权值
   node* newNode(int v){
       node* Node=new node;	//申请一个node型变量的地址空间
       Node->data=v;			//结点权值为v
       Node->lchild=Node->rchild=NULL;//初始状态下没有左右孩子！！！！
       return Node;			//返回新建结点的地址
   }
   
   //insert函数将在二叉树中插入一个数据域为x的新结点（注意参数root要加引用&）
   void insert(node* &root,int x)(
       if(root == NULL){//空树，说明查找失败，也即插入位置
           root=newNode(x);
           return;
       }
       if(x == root->data){ //查找成功，说明结点已存在，直接返回
      	 	return;
       }else if(x< root->data){ //如果x比根结点的数据域小，说明×需要插在左子树
       	insert(root->lchild,x);//往左子树搜索x
       }
   	else{//如果x比根结点的数据域大，说明×需要插在右子树
       	insert(root->rchild,x);//往右子树搜索x
       }
   )
   ```

3. **二叉查找树的建立**

   先后插入n个结点的过程

   ```c++
   //二叉查找树的建立
   node* Create(int data[],int n){
       node* root=NULL;		//新建根结点root
       for(int i=0;i<n;i++){
           insert(root,data[i]);	//将data[0]~data[n-1]插入二叉查找树中
       }
       return root;
   }
   ```

4. **二叉查找树的删除**

   ​	为了保证删除操作之后，仍然是一颗二叉查找树，把以二叉查找树中比结点权值小的最大结点称为该结点的**前驱**，二叉查找树中比结点权值大的最小结点称为该结点的**后继**。显然,结点的**前驱**是该结点**左子树中的最右结点**(也就是从左子树根结点开始不断沿着rchild往下直到rchild为NULL时的结点),而结点的**后继**则是该结点**右子树中的最左结点**(也就是从右子树根结点开始不断沿着lchild往下直到 lchild为NULL时 的结点)。

   ![1565146369009](pic/1565146369009.png)

   ```c++
   //寻找以root为根结点的树中的最大权值结点
   node* findMax(node* root){
       while(root->rchild!=NULL){
           root=root->rchild;
       }
       return root;
   }
   
   //寻找以root为根结点的树中的最小权值结点
   node* findMin(node* root){
       while(root->lchild!=NULL){
           root=root->lchild;
       }
       return root;
   }
   ```

   ```c++
   //删除以root为根结点的树中权值为x的结点
   void deleteNode(node* &root,int x){
       if(root==NULL) return;		//不存在权值为x的结点
       if(root->data ==x){			//找到欲删除结点
           if(root->lchild==NULL && root->child ==NULL){//叶子结点直接删除
               root=NULL;	//root地址改为NULL，父节点引用不到它
           }else if(root->data !=NULL){
               node* pre=findMax(root->lchild);
               root->data=pre->data;
               deleteNode(root->lchild,pre->data);
           }else{
               node* next=findMin(root->rchild);
               root->data=next->data;
               deleteNode(root->rchild,next->data);
           }
       }else if(root->data>x){
           deleteNode(root->lchild,x);
       }else{
           deleteNode(root->rchild,x);
       }
   }
   ```

   ​    但是也要注意,总是优先删除前驱(或者后继)容易导致树的左右子树高度极度不平衡,使得二叉查找树**退化成一条链**。解决这一问题的办法有两种:一种是每次**交替删除**前驱或后继:另一种是**记录子树高度**,总是优先在高度较高的一棵子树里删除结点.

#### 9.4.3 二叉查找树的性质

​	对二叉查找树进行中序遍历，遍历的结果是有序的。

​	

### 9.5 平衡二叉树AVL

#### 9.5.1 定义

​	对树的结构进行调整。AVL仍然是一颗二叉查找树，只是在基础上增加了“平衡"的要求.所谓平衡是指，对AVL树的任意节点来说，其**左子树和右子树的高度之差的绝对值不超过1**，左右子树的高度之差被称为该结点的**平衡因子**。

![1565163100668](pic/1565163100668.png)

```c++
//添加weight
struct node{
    typename data;	//数据域
    int weight;		//height为当前子树的高度
    node* lchild;	//指向左子树根结点的指针
    node* rchild;	//指向右子树根节点的指针
};
```

```c++
//生成一个新的结点，v为结点权值
node* newNode(int v){
    node* Node=new node;
    Node->data=v;
    Node->height=1;		//初始化为1
    Node->lchild=Node->rchild=NULL;
    return Node;
}
```

```c++
//获取以root为根结点的子树的当前weight
int getHeight(node* root){
    if(root==NULL) return 0;//空结点高度为0
    return root->height;
}
```

```c++
//计算结点root的平衡因子
int getBalanceFactor(node* root){
    return getHeight(root->lchild)-getHeight(root->rchild);
}
```

```c++
//更新结点root的height
//左子树的height与右子树的height的较大值 再加1
void updateHeight(node* root){
	root->height =max(getHeight(root->lchild),getHeight(root->rchild))+1;
}
```

#### 9.5.2 平衡二叉树的基本操作

 1. **查找操作**

    ```C++
    //与BST完全相同
    void search(node* root,int x){
        if(root==NULL){
            printf("search failed");
            return;
        }
        if(x==root->data){
            printf("%d\n",root->data);
        }else if(x<root->data){
            search(root->lchild,x);
        }else{
            search(root->rchild,x);
        }
    }
    ```

 2. **插入操作**

    ![1565164065803](pic/1565164065803.png)

    **左旋**

    ```c++
    //左旋 left ratation
    void L(node* &root){
        node* temp=root->rchild;
        root-rchild=temp->lchild;
        temp->lchild=root;
        updateHeight(root);	//更新结点A的高度
        updateHeight(temp);	//更新结点B的高度
        root= temp;			//设定根结点
    }
    ```

    ![1565164527582](pic/1565164527582.png)

    **右旋**

    ```c++
    //右旋 Right ratation
    void R(node* &root){
        node* temp=root->lchild;
        root-lchild=temp->rchild;
        temp->rchild=root;
        updateHeight(root);	//更新结点B的高度
        updateHeight(temp);	//更新结点A的高度
        root= temp;			//设定根结点
    }
    ```

    左右旋为互逆操作。left和right互换即可

    ​	AVL插入操作，平衡因子的绝对值大于1，子树就是失衡的，需要进行调整。只有在从根结点到该插入结点的路径上的结点才可能发生平衡因子变化，只需对路径上的平衡的结点进行调整。**只要把最靠近插入结点的失衡结点调整到正常**，路径上所有结点都会平衡。

    ![1565167300091](pic/1565167300091.png)

    ​	把以C为根结点的子树看作一个整体，然后以结点A为root进行**右旋**

    ![1565167287770](pic/1565167287770.png)

    ​	先忽略结点A，以结点C为root进行**左旋**，就可以把情况转化为LL型，然后按上面LL型进行一次**右旋**即可

    ![1565167375651](pic/1565167375651.png)

    ---

    ​	由于结点A的平衡因子是-2，因此右子树的高度比左子树大2，于是以结点A为根结点的子树一定是以下两种形态RR型与RL型之一。当结点A的右孩子的平衡因子是-1时为RR型，是1时为RL型。

    ![1565169448341](pic/1565169448341.png)

    ​	对RR型来说，可以把以C为根结点的子树看作一个整体，然后以结点A作为root进行左旋，可以达到平衡。

    ![1565169506710](pic/1565169506710.png)

    ​	对RL型来说，可以先忽略结点A，以结点C为root进行右旋，可以把情况转化为RR型，然后按上面RR型的做法进行一次左旋即可。

    ![1565169561718](pic/1565169561718.png)

    ​	**总结**

    ![1565169580142](pic/1565169580142.png)

    ```c++
    //插入权值为v的结点
    void insert(node* &root,int v){
        if(root==NULL){
            root=newNode(v);
            return;
        }
        if(v<root->v){
            insert(root->lchild,v);
        }else{
            insert(root->rchild,v);
        }
    }
    ```

    ​	由于需要从插入的结点开始从下往上判断结点是否失衡，因此需要在每个insert函数之后更新当前子树的高度，并在这之后根据树形时LL型、LR型、RR型、RL型之一来进行平衡操作，代码如下：

    ```c++
    //插入权值为v的结点
    void insert(node* &root,int v){
        if(root==NULL){
            root=newNode(v);
            return;
        }
        if(v< root->v){
            insert(root->lchild,v);
            updateHeight(root);
            if(getBalanceFactor(root)==2){
                if(getBalanceFactor(root->lchild)==1){	//LL型
                    R(root);
                }else if(getBalanceFactor(root->lchild)==-1){
                    L(root->lchild);
                    R(root);
                }
            }
        }else{
            insert(root->rchild,v);
            updateHeight(root);
            if(getBalanceFactor(root)==-2){
                if(getBalanceFactor(root->rchild)==1){	//LL型
                    R(root->rchild);
                    L(root);
                }else if(getBalanceFactor(root->rchild)==-1){
                    L(root);
                }
            }
        }
    }
    ```

 3. **AVL树的建立**

    ```c++
    node* Create(int data[],int n){
        node* root=NULL;
        for(int i=0;i<n;i++){
            insert(root,data[i]);
        }
        return root;
    }
    ```

---

### 9.6 并查集

#### 9.6.1 并查集的定义

​	维护集合的数据结构。”并“Union、”查“Find、”集“Set

​	支持：合并两个集合、判断两个元素是否在一个集合。

​	使用一个数组：int father[N];	实现

​	father[i]表示元素i的父亲结点，而父亲结点本身就是这个集合的元素，**对同一个集合来说只存在一个根结点，且将其作为所属集合的标示**。

```c++
father[1]=1;	//1的父亲结点是自己，1号为根结点
father[2]=1;
father[3]=2;
father[4]=2;

father[5]=5;	//5的父亲结点是自己，5号为根结点
father[6]=5;
```

![1565180156992](pic/1565180156992.png)

#### 9.6.2 并查集的基本操作

​	总体来说，并查集的使用需要先初始化father数组，然后根据需要进行查找或合并的操作。

1. **初始化**

   ```c++
   for(int i=1;i<=N;i++){
       father[i]=-1;
   }
   ```

2. **查找**

   ```c++
   //只有一个根结点，查找操作就是对给定的结点寻找根结点。
   //递推
   int findFather(int x){
       while(x!=father[x]){
           x=father[x];//获得自己的父亲结点
       }
       return x;
   }
   
   //递归
   int findFather(int x){
       if(x==father[x]) return x;
       else return findFather(father[x]);
   }
   ```

3. **合并**

   ```c++
   //先判断两个元素是否属于同一个集合
   //再把其中一个集合的根结点的父亲指向另一个集合的根结点
   void Union(int a,int b){
       int faA=findFather(a);		//a的根结点
       int faB=findFather(b);		//b的根结点
       if(faA!=faB){				//不属于同一个集合
           father[faA]=faB;//合并
       }
   }
   ```

   ​	并查集的一个性质。如果两个元素在相同的集合中，那么就不会对其进行操作.这就保证了在同一个集合中一定不会产生环,即**并查集产生的每一个集合都是一棵树**.

---

#### 9.6.3 路径压缩

 	把当前查询结点的路径上的所有结点的父亲都指向根结点,查找的时候就不用一直回溯去找父亲了.

```c++
int findFather(int x){
    //由于x在下面的while中会变成根节点,因此先把原先的x保存一下
    int a=x;
    while(x!=fahter[x]){
    	x=fahter[x];
    }
    //x存放的是根结点,下面把路径上的所有结点的father都改为根结点
    while(a!=father[a]){
        int z=a;		//因为a要被father[a]覆盖,所有先保存a的值,以修改father[a]
        a=father[a];	//a回溯父亲节点
        father[z]=x;	//将原先的节点a的父亲改为根结点x
    }
    return x;
}
```

```c++
int findFather(int v){
    if(v==father[v]) return v;
    else{
        int F=findFather(father[v]);
        father[v]=F;
        return F;
    }
}
```

---

### 9.7 堆

#### 9.7.1 定义与基本操作

​	堆是一颗**完全二叉树**,树中的每个结点的值都大于等于左右孩子结点的值(**大顶堆**),小于等于左右孩子结点的值(**小顶堆**).一般用于**优先队列**的实现.

![1565183394776](pic/1565183394776.png)

![1565183450485](pic/1565183450485.png)

![1565183487381](pic/1565183487381.png)

![1565183521253](pic/1565183521253.png)

![1565183537174](pic/1565183537174.png)

```C++
//数组存储完全二叉树
//结点按层序存储与数组中
//第一个结点将存储与数组的1号位
//数组i号位表示的结点的左孩子就是2i号位   右孩子2i+1
const int maxn=100;
//heap为堆,n为元素个数
int heap[maxn],n=10;
```

```c++
//对heap数组在[low,high]范围进行向下调整
//其中low为欲调整结点的数组下标,high一般为堆的最后一个元素的数组下标
void downAdjust(int low,int high){
    int i=low,j=i*2;	//i为欲调整结点,j为左孩子
    while(j<=high){		//存在孩子结点
        //如果右孩子存在,且右孩子的值大于左孩子
        if(j+1<=high && heap[j+1] >heap[j]){
            j=j+1;
        }
        //如果孩子中最大的权值比欲调整结点i大
        if(heap[j] > heap[i]){
            swap(heap[j], heap[i]);
            i=j;			//保持i为欲调整结点,j为i的左孩子
            j=i*2;
       }else{
            break;	//孩子的权值均比欲调整结点i小,调整结束
        }
    }
}
```

​	**建堆**,假设序列中元素的个数n,由于完全二叉树的叶子结点个数为n/2,因此数组下标在[1,n/2]范围内的结点都是非叶子结点.从n/2号位开始倒着枚举结点,.**保证每个结点都是以其为根结点的子树中的权值最大的结点**

```c++
//建堆
void createHeap(){
    for(int i=n/2;i>=1;i--){
        downAdjust(i,n);
    }
}
```

```C++
//删除堆顶元素
void deleteTop(){
    heap[1]=heap[n--];
    downAdjust(1,n);
}
```

```c++
//添加元素
//添加的元素放在数组,然后进行 向上调整,向上调整总是把欲调整结点与父亲结点比较,如果权值大,就交换其父亲结点,直到达堆顶或是父亲结点的权值较大为止.

//对heap数组在[low,high]范围进行向上调整
//其中low为一般设为1,high表示欲调整结点的数组下标
void upAdjust(int low,int high){
    int i=high,j=i/2;	//i为欲调整结点,j为父亲
    while(j>=low){		//父亲在[low,high]范围内
        //父亲权值小于欲调整结点i的权值
        if(heap[j] <heap[i]){
            swap(heap[j],heap[i]);
            i=j;
            j=j/2;
        }else{
            break;	
        }
    }
}

void insert(int x){
    heap[++n]=x;	//元素个数+1
    upAdjust(1,n);	//向上调整新加入的结点n
}
```

#### 9.7.2 堆排序

​	使用对结构堆一个序列进行排序.

​	取出堆顶元素,然后将堆的最后一个元素替换至堆顶,再进行一次针对堆顶元素的向下取整.直到堆中只有一个元素为止.

​	为了节省空间,可以**倒着遍历数组**,假设当前访问到i号位,那么将堆顶元素与i号位的元素交换,接着在[1~i-1]范围内对堆顶元素进行一次向下调整即可.

```c++
//堆排序
void heapSort(){
    createHeap();	//建堆
    for(int i=n;i>1;i--){		//倒着枚举,直到堆中只有一个元素
        swap(heap[i],heap[1]);	//交换heap[i]与堆顶
        downAdjust(1,i-1);		//调整堆顶
    }
}
```

---

### 9.8 哈夫曼树/最优二叉树

#### 9.8.1 哈夫曼树

​	经典合并果子问题

```c++
	有n堆果子,每堆果子的质量已知,现在需要把这些果子合并成一堆,但是每次只能把两堆果子合并到一起,同时会消耗与两堆果子质量之和等值的体力.显然,在进行n-1次合并之后,就只剩下一堆了.为了尽可能节省体力,请设计出合并的次序方案,使得耗费的体力最少,给出消耗的体力值
	例如有3堆果子,质量依次为1,2,9.那么可以先将质量为1和2的果摊合并,新堆质量为3.再与9合并3+(3+9)
```

​	把每堆果子都看作结点,果堆的质量视作结点的权值,这样合并两个果堆的过程就可以视作给它们生成一个父结点,且**父结点的权值**等于它们的**质量之和**,于是把n堆果子**合并成一堆**的过程可以用一棵**树来表示**.

​	消耗体力之和也可以通过把**叶子结点的权值**乘以它们各自的**路径长度**再求和来获得,其中**叶子结点的路径长度**是指**从根结点出发到达该结点所经过的边数**.

​	把叶子结点的权值乘以其路径长度的结果称为这个叶子结点的**带权路径长度**.树的带权路径长度为所有叶子节点的带权路径长度之和.

​	于是合并果子问题转换成:已知n个数,寻找一棵树,使得树的所有叶子节点的权值恰好为这n个数,并且使得这棵树的带权路径长度最小**.带权路径长度最小**的树被称为**哈夫曼树**.显然,同一组叶子节点来说,哈夫曼树可以是不唯一的,但是最小带权路径长度一定是唯一的.

​	对哈夫曼树来说**不存在度为1的结点**,并且**权值越高**的结点相对来说越**接近根**结点,

​	**核心构建思想**:反复选择两个最小的元素,合并,直到只剩下一个元素. **并不用建立一个哈夫曼树**

```c++
#include<cstdio>
#incldue<queue>
using namespace std;

//代表小顶堆的优先队列   数字越小 优先级越大
priority_queue<long long,vector<long long>,greater<long long>> q;

int main(){
    int n;
    long long  temp,x,y,ans=0;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
    	scanf("%lld",&temp);
        q.push(temp);	//将初始重量压入优先队列
    }
    while(q.size()>1){	//至少优两个元素
        x=q.top();
        q.pop();
    	y=q.top();
        q.pop();
        q.push(x+y);	//取出堆顶的两个元素,求和后压入优先队列
        ans+=x+y;		//累计求和的结果
    }
    printf("%lld",ans);
    return 0;
}
```

---

#### 9.8.2 哈夫曼编码

​	对任意一颗二叉树来说,如果把二叉树上的所有分支都进行编号,将所有左分支都标记为0\所有右分支都标记为1,那么对树上的任意一个结点,都可以根据根结点出发到达它的分支顺序得到一个编号,并且这个编号是所有结点中**唯一的**.**对于任何一个叶子结点,其编号一定不会成为其他任何一个结点编号的前缀**.

​	**前缀编码**-意义在于不产生混淆,让解码正常进行.让这些字符作为一颗二叉树的叶子结点,就能产生需要的编码.

​	尽量选择长度最短的编码方式.把A,B,C,D的出现次数作为各自叶子结点的权值,**那么字符串编码成01串后的长度实际上就是这棵树的带权路径长度**.

​	问题就转换成了:把每个字符出现的次数作为叶子结点的权值,求一棵树,使得这棵树的带权路径长度最小.

​	**哈夫曼编码能使给定字符串编码成01串后长度最短的前缀编码**.

​	哈夫曼编码是针对确定的字符串来讲的.

---

## 第10章 提高篇(4)——图算法专题

###  10.1 图的定义和相关术语







## 第11章 提高篇(5)——动态规划专题











## 第12章 提高篇(6)——字符串专题









## 第13章 专题扩展



















































