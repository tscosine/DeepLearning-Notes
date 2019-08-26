### Class-Balanced Loss Based on Effective Number of Samples

###### Key words:

###### 论文链接:https://arxiv.org/abs/1901.05555

###### 核心思想:



### Introduciton

解决数据不平衡问题主要有两种方法:

+ resampling
+ cost-sensitive-weighting

缺点:

resampling包括over sampling和under sampling,over sampling的问题是样本重复,导致训练变慢和过拟合,under sampling 导致丢失有效样本  

cost-sensitive-weighting的主要问题是构造合适的损失函数比较困难,表现不佳.

本文要解决的问题是how can we design a better class-balanced loss,提出的方法是计算data overlap然后计算样本的effective number



### Effective Number of samples

#### DataSampling as Random Covering

For each class,样本特征集合$S$,容量$N$,采样越多,$S$的覆盖率越高,最多采样$N$个数据

**Definition** Effective Number:The effective number of samples is the expected volume of samples.

为了简化问题,不考虑局部重叠(partial overlapping),只考虑overlapped和not overlapped  

![](../pics/effective number of sample.png)

####  Mathematical Formulation

记Effective Number of samples为$E_n$
$$
E_n=(1-\beta^n)/(1-\beta)
$$

$$
\beta = (N-1)/N
$$

证明如下:
$$
E_1=(1-\beta^1)/(1-\beta) = 1
$$

$$
E_n=pE_{n-1}+(1-p)(E_{n-1}+1) = 1+\frac{N-1}{N}E_{n-1}
$$

数学归纳法可证(略)

显然
$$
\lim_{\beta->1}E_n = n
$$

### Class Balanced Loss

$$
CB(p,y) = 1/E_{n_y}L(p,y) = \frac{1-\beta}{1-\beta^{n_y}}L(p,y)
$$

