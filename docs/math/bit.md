
位运算就是把整数转换为二进制后，每位进行相应的运算得到结果。

常用的运算符共 6 种

分别为与（`&`）、或（`|`）、异或（`^`）、取反（`~`）、左移（`<<`） 和右移（`>>`）。

## 与、或、异或
与（`&`）或（`|`）和异或（`^`）这三者都是两者间的运算，因此在这里一起讲解

表示把两个整数分别转换为二进制后各位逐一比较

<table><tr>
<td style="text-align:center;">`&`</td><td>只有在两个（对应位数中）都为 1 时才为 1</td>
</tr><tr>
<td style="text-align:center;">`|`</td><td>只要在两个（对应位数中）有一个 1 时就为 1</td>
</tr><tr>
<td style="text-align:center;">`^`</td><td>只有两个（对应位数）不同时才为 1</td>
</tr></table>
* `^` 运算的逆运算是它本身，也就是说两次异或同一个数最后结果不变，即 `(a ^ b) ^ b = a`。

> 举例

$$
\begin{aligned}
&5&=&&(101)_2\\
&6&=&&(110)_2\\
&5\text{\tt\,\&\,}6&=&&(100)_2&=\ 4\\
&5\text{\tt\,|\,}6&=&&(111)_2&=\ 7\\
&5\texttt{\ \!\^{}\ }6&=&&(011)_2&=\ 3\\
\end{aligned}
$$

#### 取反

取反是对 1 个数 num 进行的计算

`~`  把 num 的补码中的 0 和 1 全部取反（ 0 变为 1，1 变为 0）

* 补码——正数的补码为其（二进制）本身，负数的补码是其（二进制）取反后加一。

> 举例

$$
\begin{aligned}
5=(0000\ 0101)_2\\
5\ 的补码=(1111\ 1010)_2\\
\text{\tiny{～}\ }5=(1111\ 1010)_2
\end{aligned}
$$

## 左移和右移
与前面的4种运算相似，这两种运算仍是把整数转换为二进制后进行操作

左移（`<<`） 将转化为二进制后的数字整体向左移动
> `num<<i`  //表示将 num 转换为二进制后向左移动 i 位（所得的值）

右移（`>>`） 将转化为二进制后的数字整体向右移动
> `num>>i`  //表示将 num 转换为二进制后向左移动 i 位（所得的值）

> 举例

$$
\begin{aligned}
&5&&=&&(101)_2\\
&5\text{\tt\,<<\,}2&&=&&(10100)_2\!\!\!&=&&\!\!\!20\\
&5\text{\tt\,>>\,}1&&=&&(10)_2&=&&2
\end{aligned}
$$

* 如上图，右移操作中末尾多余的“1”将会被舍弃

* 注意，左移和右移是有返回值的，并非对 num 本身进行操作

***

## 位运算的应用

> num<<<seperator style="font-size:0;margin:0;padding:0;"></seperator> i 相当于 num 乘以 2 的 i 次方，而 num>>i 相当于 num/2 的 i 次方(位运算比"%"和"/"操作快得多
(据说效率可以提高60%)(据2018JSOI夏令营课件)

> num*10=(num<<1)+(num<<3)

> `num&1`相当于取 num 二进制的最末位，可用于判断 num 的奇偶性，二进制的最末位为 0 表示该数为偶数，最末位为 1 表示该数为奇数。

> 
```cpp
//利用位运算的快捷的 swap 代码
void swap(int a, int b){
	a = a ^ b;   
	b = a ^ b;  
	a = a ^ b;
}

```
---

## 位运算的常用方法

- 乘以 2 运算
```cpp
int mulTwo(int n){//计算n*2
    return n << 1;
}
```

- 除以 2 运算
```cpp
int divTwo(int n){//负奇数的运算不可用
    return n >> 1;//除以2
}
```

- 乘以 2 的 $m$ 次方
```cpp
int mulTwoPower(int n,int m){//计算n*(2^m)
    return n << m;
}
```

- 除以 2 的 $m$ 次方
```cpp
int divTwoPower(int n,int m){//计算n/(2^m)
    return n >> m;
}
```

- 判断一个数的奇偶性
```cpp
boolean isOddNumber(int n){
    return (n & 1) == 1;
}
```

- 取绝对值（某些机器上，效率比 `n>0 ? n:-n` 高）
```cpp
int abs(int n){
return (n ^ (n >> 31)) - (n >> 31);
/* n>>31 取得n的符号，若n为正数，n>>31等于0，若n为负数，n>>31等于-1
若n为正数 n^0=0,数不变，若n为负数有n^-1 需要计算n和-1的补码，然后进行异或运算，
结果n变号并且为n的绝对值减1，再减去-1就是绝对值 */
}
```

- 取两个数的最大值（某些机器上，效率比 ` a>b ? a:b` 高）
```cpp
int max(int a,int b){
    return b & ((a-b) >> 31) | a & (~(a-b) >> 31);
    /*如果a>=b,(a-b)>>31为0，否则为-1*/
}
```

- 取两个数的最小值（某些机器上，效率比 `a>b ? b:a` 高）
```cpp
int min(int a,int b){
    return a & ((a-b) >> 31) | b & (~(a-b) >> 31);
    /*如果a>=b,(a-b)>>31为0，否则为-1*/
}
```

- 判断符号是否相同
```cpp
boolean isSameSign(int x, int y){ //有0的情况例外
    return (x ^ y) >= 0; // true 表示 x和y有相同的符号， false表示x，y有相反的符号。
}
```

- 计算 2 的 $n$ 次方
```cpp
int getFactorialofTwo(int n){//n > 0
    return 2 << (n-1);//2的n次方
}
```

- 判断一个数是不是 2 的幂
```cpp
boolean isFactorialofTwo(int n){
    return n > 0 ? (n & (n - 1)) == 0 : false;
    /*如果是2的幂，n一定是100... n-1就是1111....
       所以做与运算结果为0*/
}
```

- 对 2 的 $n$ 次方取余
```cpp
int quyu(int m,int n){//n为2的次方
    return m & (n - 1);
    /*如果是2的幂，n一定是100... n-1就是1111....
     所以做与运算结果保留m在n范围的非0的位*/
}
```

- 求两个整数的平均值
```cpp
int getAverage(int x, int y){
        return (x + y) >> 1;
｝
```

#### 题目推荐

[CODE[VS] 2743 黑白棋游戏 ](http://codevs.cn/problem/2743/)
