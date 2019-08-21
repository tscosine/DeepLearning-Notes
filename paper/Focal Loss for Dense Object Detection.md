### Focal Loss for Dense Object Detection

###### Key words:loss func,data imbalance

###### 论文链接:https://arxiv.org/abs/1708.02002

###### 核心思想:数据不平衡导致了容易分类的class dominate了grad,需要降低这部分权重.

提出一个损失函数$FL$

$FL(p_t)=-\alpha(1-p_t)^\gamma log(p_t)$

其中$\gamma$ 是可调整的,$\gamma=0$损失函数即为CE,作者给出的最优取值$\gamma=2$ ,$\alpha$是补偿因子

