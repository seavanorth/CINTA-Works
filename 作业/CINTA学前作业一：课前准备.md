# CINTA学前作业一：课前准备

标签（空格分隔）： 作业

***
## 作业原文:
> 本作业可视为开学前的学习准备，也作为我了解大家的一次测试。任务包括如下：
>1、建立自己的个人博客，根据自己 的喜好和习惯进行选择。

>2、完成以下C语言代码，贴在自己的博客，并返回链接给我。
>   a、写一个插入排序的函数，即输入一个数组，完成排序；

>  b、完成一个函数，输入值为整数，输出该值的二进制。

> c、完成一个判断整数是否素数的函数，即，输入一个整数，判断其是否素数。

>3、编辑一个数学公式：a的立方 + b的立方 = c的立方

***

## 解答:

### 1.之前在cdsn写过一段时间([Ryancell](https://blog.csdn.net/weixin_51966728?spm=1011.2124.3001.5343), ~~有点水~~)，后来leetcode也写过些题解([CODERYAN](https://leetcode-cn.com/u/roycec/), ~~非常菜~~),Github上啥也没有[seavenorth](https://github.com/seavanorth), ~~一直在白嫖别人的~~，不过也准备传一点东西上去了.
***
### 2.a:插入排序

```C++
void insertsort(vector<int> &nums)
{
    int n = nums.size();
    for (int i = 1; i < n; i++) //假设data[1]已经排好序，则后续元素只需判断插入其左/右侧
    //若data[k]>data[k+1/2/3...target-1/target],则data[k]...data[target-1]全部右移一位，data[target]移动到data[k]
    {
        int j;
        if (nums[i] < nums[i - 1]) //需要将data[i]插入有序子表
        {
            int tmp = nums[i]; //设置哨兵
            for (j = i - 1; j >= 0 && tmp < nums[i]; j--)//设置判断元素nums[i]--当前循环的判断依据
            {
                nums[j + 1] = nums[j];//若data[j]>哨兵，则记录(判断元素)后移一位
            }                               
            nums[j + 1] = tmp; //插入到正确位置
        }
    }
}
```

### 2.b:进制转换
**1.使用库函数**
```C++
#include <iostream>
using namespace std;
#define MaxSize 80
void num_sys_converse();
void num_sys_converse()
{
	int isradix, osradix;
	char input[MaxSize], output[MaxSize];
	int tmp = 0;
	char *stop;
	do
	{
		cout << "The number system of input:";
		cin >> isradix;
		if (isradix == 0)
			return;
			cout << "The number to be conversed:";
		cin >> input;
		cout << "The number system to converse to:";
		cin >> osradix;
		tmp = strtol(input, &stop, isradix);
		_itoa_s(tmp, output, osradix);
		cout << "Result:" << output << endl;
	} while (true);
}
```
**2.手写**
```C++
#include <sstream>
//数转字符串
string num2str(double i)
{
    stringstream ss;
    ss << i;
    return ss.str();
}
//任意2-36进制转换为10进制
int Atoi(string str, int radix)
{
	int ans = 0;
	for (int i = 0; i < str.size(); i++)
	{
		char tmp = str[i];
		if (tmp >= '0'&&tmp <= '9')
			ans = ans * radix + tmp - '0';
		else
			ans = ans * radix + tmp - 'a' + 10;
	}
	return ans;
}
//10进制转换为任意n进制
string Itoa(int n, int radix)//(10进制数，转换成的进制)
{
	string ans = "";
	while (n != 0)
	{
		int tmp = n % radix;
		if (tmp >= 0 && tmp <= 9)
			ans += tmp + '0';
		else
			ans += tmp - 10 + 'a';
		n /= radix;
	}
	reverse(ans.begin(), ans.end());
	return ans;
}
```

### 2.c:质数判断
**1.线性筛**

```C++
bool isprime(int num)
{
    if (num <= 1)
        return false;
    for (int i = 2; i <= sqrt(num); i++)
        if (num % i == 0)
            return false;
    return true;
}
```

**2.线性筛优化**
```C++
bool isprime_optimize(int n)
{
    if (n <= 1)
        return false;
    if (n == 2 || n == 3)
        return true;
    if (n % 6 != 1 && n % 6 != 5)   //6n+1或6n+56
        return false;
    for (int i = 5; i * i <= n; i += 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
    return true;
}
```
***

### 3.a的立方 + b的立方 = c的立方
$$a^3 + b^3 = c^3$$




