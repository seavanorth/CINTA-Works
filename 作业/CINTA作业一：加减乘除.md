# CINTA作业一：加减乘除

标签（空格分隔）： 作业

---

## 1.C语言实现一种迭代版本的简单乘法

```cpp
/*
Function：两非负整数的乘法
Input：非负整数number_1,number_2
Output:非负整数answer
*/
int Simple_Multiply(int number_1, int number_2)
{
	int answer = 0;
	for (int i = 0; i < number_2; ++i)
		s += number_1;
	return answer;
}
```

***

## 2.证明命题1.1(整除性)
$设a,b,c \in \mathbb{Z},若 a \mid b，b \mid c,则 a \mid c.若c \mid a,c \mid b,则对任意的m,n \in {Z},有c \mid (ma+nb)$

证明:

- 前半句:
令$a \mid b,b \mid c$，则$b = q1 \cdot a,c = q2 \cdot b.(q1,q2 \in {Z})$
则$c = q2 \cdot q1 \cdot a$
又$q1 \cdot q2 \in {Z}$
所以$a \mid c$

- 后半句:
令$c\mid a, c\mid b$,则$a = q1\cdot c, b = q2\cdot c.(q1,q2 \in {Z})$
则$ma + nb = m\cdot q1\cdot c +n\cdot q2\cdot c = c(m\cdot q1+n\cdot q2).(m,n\in {Z})$
所以$(m\cdot q1+n\cdot q2) \in {Z}$
所以$c \mid (ma + nb)$
***

## 3.证明定理1.1(除法定理)
除法定理:
令$ a,b \in \mathbb{Z}, b > 0.存在特定的整数q和r,使得 a = bq + r,(0 \leq r < b)$
证明:

- $q,r$的存在性的证明：
令 ${S} = \{a - bk:k \in \mathbb{Z} 且a - bk \geq 0 \} $
1. $若 0 \in {S},那么b能整除a. 则 q = a/b， r  = 0$
2. $若0 \not\in {S}$,则利用良序定理，证明${S} \not= \varnothing$
    1)$若a>0,那么a - b \cdot 0 > 0 \in {S}$
    2)$若a<0,令k=2,那么a - b \cdot (2a) = a(1-2b) > 0,即a(1-2b) \in {S}$
    $所以{S} \not= \varnothing$
由良序原则可得,${S}$中一定存在一个最小元素,令$r=a-bq$，因此存在$a=bq+r,r \geq 0$

- $r < b$的证明:
假设$r > b$,那么有
    $a - b(q+1) = a-bq-b = r-b > 0$
那么又有$a-b(q+1) \in {S}$
但$a-b(q+1)<a-bq$,与$r = a-bq$是${S}$中最小的元素相悖
所以$r \leq b$
又$0 \not\in {S},r \not= b$,所以$r<b$

- $q,r$唯一性的证明:
假设存在整数$r,r',q,q'$使得
    $a=bq+r,0 \leq r <b 且 a=bq' + r',0 \leq r' < b$
那么有$bq+r = bq'+r'$,假设$r' \geq r$,从上式变形得$b(q-q')=r'-r$
因此$b必须整除(r'-r) 且 0 \leq r'-r \leq r' <b,当且仅当r'-r=0时成立$
所以$r=r'且q=q'$

***
