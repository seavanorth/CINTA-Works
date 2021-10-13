# CINTA作业二：GCD与EGCD

标签（空格分隔）： 作业

***

## 题目

> 1、给出Bezout定理的完整证明。
2、实现GCD算法的迭代版本。
3、实现EGCD算法。输入：a、b两个整数，输出：r、s、d三个整数，满足ar + bs =d。
4、实现一种批处理版本的GCD算法，即，给定一个整数数组，输出其中所有整数的最大公因子。输入：一个整数数组a；输出：一个整数d，是a数组中所有整数的最大公因子。

***

## 1.给出Bezout定理的完整证明。
> Bezout定理:
设 a 和 b 为非零整数，存在整数 r 和 s 使得：
$ gcd(a, b) = ar + bs $
而且，a 与 b 的最大公因子是惟一的。称 r 和 s 为 Bézout 系数。

证明:
令集合
     $${s} = \{am + bn : m,n \in \mathbb{Z} 且 am + bn > 0 \}$$
显然地，集合${S}$是非空集。因此，由良序原则得，${S}$中一定存在最小元素.
不妨令该最小元素为$d = ar + bs$.我们说$d = gcd(a,b)$.使$a = dq + r'(0 \leq r' < d)$.
若$r' > 0$,那么
$$
r' = a - dq\\
= a - (ar + bs)q\\
= a - arq - bsq\\
= a(1-rq) + b(-sq)
$$
$r' \in {S}$
与$d$是${S}$的最小元素相悖，因此$r' = 0 且 d $整除 $a$.同理，$d$整除$b$.因此，$d$是一个$a$和$b$的公因子

假设$d'$是$a$和$b$的另一个公因子，想要证明$d' |d$.
若令$a = d'h 且 b = d'k$,那么
$$ d = ar + bs = d'hr + d'ks = d'(hr+ks)$$
因此$d'$必定整除d.
因此，$d$必定是$a$和$b$唯一的最大公因子

***

## 2.实现GCD算法的迭代版本。

```c++
//Iteration
//Input: intergers a and b
//Output: d = gcd(a,b)
unsigned int gcd(unsigned int num1, unsigned int num2)
{
	unsigned int a = num1 > num2 ? num1 : num2;
	unsigned int b = num1 > num2 ? num2 : num1;//确保a>=b
	while (b != 0)
	{
		unsigned int mod = a % b;
		a = b;
		b = mod;
	}
	return a;
}
```

***

## 3.实现EGCD算法。输入：a、b两个整数，输出：r、s、d三个整数，满足ar + bs =d。

```c++
//Iteration
//Input: integers a and b, with a > b
//Output: d=gcd(a,b), and r and s  d = a*r + b*s
vector<unsigned int> egcd(unsigned int num1, unsigned int num2)
{
	vector<unsigned int> res(3);
	unsigned int r1 = 1, s1 = 0, a = num1 > num2 ? num1 : num2;
	unsigned int r2 = 0, s2 = 1, b = num1 > num2 ? num2 : num1;
	while (b != 0)
	{
		unsigned int q = a / b;

		unsigned int tmp = a % b;
		a = b;
		b = tmp;

		tmp = r1 - q * r2;
		r1 = r2;
		r2 = tmp;

		tmp = s1 - q * s2;
		s1 = s2;
		s2 = tmp;
	}
	res = { a, r1, s1 };
	return res;
}
```

***

## 4.实现一种批处理版本的GCD算法，即，给定一个整数数组，输出其中所有整数的最大公因子。输入：一个整数数组a；输出：一个整数d，是a数组中所有整数的最大公因子。

```c++
//GCD Algorithm Batch Version
//Input: a group of integers nums, with "nums" have more than 2 integers
//Output:the greatest common divisor of all integers in "nums" 
unsigned int bgcd(vector<unsigned int>& nums)
{
	size_t size = nums.size();
	if (size < 1)//只有一个元素或没有元素
		return -1;
	unsigned int tmp_gcd = gcd(nums[0], nums[1]);
	for (int i = 2; i < size; ++i)
	{
		tmp_gcd = gcd(tmp_gcd,nums[i]);
	}
	return tmp_gcd;
}
```

***
## 5.上述三种算法的测试
```c++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
	//gcd测试
	unsigned int a, b;
	cin >> a >> b;
	unsigned int res_gcd = gcd(a, b);
	cout << a << "和" << b << "的最大公因数:" << res_gcd << endl;

	//egcd测试
	cin >> a >> b;
	vector<unsigned int> res_egcd = egcd(a,b);
	cout <<"a*r + b*s = d : d = " << res_egcd[0] << ",r = " << res_egcd[1]<<",s = "<<res_egcd[2] << endl;


	//bgcd测试
	vector<unsigned int> test_bgcd = {};
	unsigned int res_bgcd = bgcd(test_bgcd);
	cout << "该组数最大公因数为:" << res_bgcd << endl;
}
```


