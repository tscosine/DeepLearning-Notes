### PCA降维

参考链接:https://zhuanlan.zhihu.com/p/77151308

#### 最大可分性

##### 方差

$$
Var(a) = \frac{1}{m}\sum_{i=1}^{m}(a_i-\mu)^2
$$

均值归一化为0之后
$$
Var(a)=\frac{1}{m}\sum_{i=1}^{m}a_i^2
$$
PCA的目标为,寻找一个一维基,使所有数据变换为这个基上的坐标表示后,方差值最大.



##### 协方差

由于均值为零,m很大m-1约等于m,协方差公式为
$$
Cov(a,b)=\frac{1}{m-1}\sum_{i=1}^{m}ab=\frac{1}{m}\sum_{i=1}^{m}a_ib_i
$$
**优化目标:将一组 N 维向量降为 K 维，其目标是选择 K 个单位正交基，使得原始数据变换到这组基上后，各变量两两间协方差为 0，而变量方差则尽可能大（在正交的约束下，取最大的 K 个方差）**



##### 协方差矩阵

假设只有ab两个变量
$$
X=\left[\begin{matrix}
a_1&a_2&...&a_m \\
b_1&b_2&...&b_m \\
\end{matrix}\right]_{n*m}
$$

$$
\frac{1}{m}XX^T=\left[\begin{matrix}
Cov(a,a)&Cov(a,b) \\
Cov(b,a)&Cov(b,b)
\end{matrix}\right]_{n*n}=C
$$



##### 矩阵对角化

**优化目标:我们需要将除对角线外的其它元素化为 0，并且在对角线上将元素按大小从上到下排列（变量方差尽可能大）**

假设进行基变换之后的矩阵为$Y,Y=PX$

$D$ 为 $Y$ 的协方差矩阵
$$
D = \frac{1}{m}YY^T = \frac{1}{m}(PX)(PX)^T = \frac{1}{m}PXX^TP^T=PCP^T
$$
**优化目标:寻找一个矩阵 P，满足** ![[公式]](https://www.zhihu.com/equation?tex=PCP%5ET) **是一个对角矩阵，并且对角元素按从大到小依次排列，那么 P 的前 K 行就是要寻找的基，用 P 的前 K 行组成的矩阵乘以 X 就使得 X 从 N 维降到了 K 维并满足上述优化条件**

#### 实现

