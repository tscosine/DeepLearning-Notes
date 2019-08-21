### Looking for the Devil in the Details: Learning Trilinear Attention Sampling Network for Fine-grained Image Recognition

#### 摘要

###### Key words:超分辨率分类

###### 核心思想:Attention

###### 论文链接:https://arxiv.org/abs/1903.06150v1

#### 论文内容

![](/home/wangrunzhe/workspace/CV-paper-notes/pics/Looking for the Devil in the Details.png)

TASN包括三个部分

+ Trilinear attention module : Details localization
+ Attention-based sampler : Details extraction 
+ Feature distiller : Details optimization

##### Trilinear Attention 

输入：conv feature map

输出：attention map

*we transform feature maps into attention maps by integrating feature channels according to their spatial relationship*

![](/home/wangrunzhe/workspace/CV-paper-notes/pics/Trilinear Attention.png)

**Step**:

$input img : (c,h,w)$

$reshape : (c,h*w)$
$$
M_b(X)=(XX^T)X
$$
add normalization
$$
M(X)=N_2(N_1(X)X^T)X
$$
$N$是$softmax$操作，$N1$和$N2$意义不同

+ $N1$: keeps each channel of feature maps within the same scale
+ $N2$: conducted over each relationship vector $N(X)X^T$



##### Attention Sampling

![](/home/wangrunzhe/workspace/CV-paper-notes/pics/attention sampling.png)

**Input**

Given image : $I$

Attentimg Map : $M$

**Output**

Structure-preserved image :  $I_s$

detail-preserved image : $I_d$
$$
I_s=S(I,A(M))
$$

$$
I_d=S(I,R(M))
$$

$A(.):average pooling,R(.):random selectiong a channel,S(.):nonuniform sampling function$



Sampling

将attention矩阵在两个维度上进行采样
$$
F_x(n) = \sum_{j=1}^{n}\max_{0<i<w}A(M)_{i,j}
$$

$$
F_y(n) = \sum_{j=1}^{n}\max_{0<j<h}A(M)_{i,j}
$$

类似于求边缘密度,区别是这个用的是$max(.)$而不是$sum(.)$,原因作者说是因为$\max(.)$更robust和alternative

过程如下图所示

![](/home/wangrunzhe/workspace/CV-paper-notes/pics/attention sampling 2.png)



##### Detail Distilling

1. 把之前给出的两张图片$I_s,I_d$ 传入backbone CNN(resnet-50),得到FC输出$Z_s,Z_d$ , 加$softmax$得到$(q_s,q_d)$ 

$$
q_s^{(i)}=\frac{\exp(z_s^{i}/T)}{\sum_j\exp(z_s^{(j)}/T)}
$$

这里的参数$T$是$Temperature$,正常的$softmax$中$T=1$.在DIstilling过程中T设置的较大有利于获得"soft probability distribution over class"

**soft target cross entropy**
$$
L_{soft}(q_s,q_d)=-\sum_{i=1}^{N}q_d^{(i)}log(q_s^{(i)})
$$
最终的损失函数的形式为
$$
L(I_s) = L_{cls}(q_s,y) + \lambda L_{soft}(q_s,q_d)
$$
