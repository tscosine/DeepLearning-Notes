### On Class Imbalance and Background Filtering in Visual Relationship Detection

###### Key words:data imbalance,loss func

###### 论文链接:https://arxiv.org/abs/1903.08456

###### 核心思想:cost-sensitive loss

#### Related work

[25]S. H. Khan, M. Hayat, M. Bennamoun, F. A. Sohel, and R. Togneri, “Cost-sensitive learning of deep feature representations from imbalanced data,” IEEE transactions on neural networks and learning systems, 2017.

[31]Q. Dong, S. Gong, and X. Zhu, “Class rectification hard mining for imbalanced deep learning,” 2017.

[32]Y.-A. Chung, H.-T. Lin, and S.-W. Yang, “Cost-aware pretraining for multiclass cost-sensitive deep learning,” arXiv preprint arXiv:1511.09337, 2015.

[33]S. Wang, W. Liu, J. Wu, L. Cao, Q. Meng, and P. J. Kennedy, “Training deep neural networks on imbalanced data sets,” in Neural Networks (IJCNN), 2016 International Joint Conference on, pp. 4368–4374, IEEE,2016.

[34]Y.-X. Wang, D. Ramanan, and M. Hebert, “Learning to model the tail,”
in Advances in Neural Information Processing Systems, pp. 7029–7039,2017.

[35]C. Huang, Y. Li, C. C. Loy, and X. Tang, “Deep Imbalanced Learning for Face Recognition and Attribute Prediction,” arXiv preprint arXiv:1806.00194, 2018.

#### Proposed Methodology

cost-sensitive loss
$$
L(Z,T)=-\frac{1}{N}\sum_{i=1}^{N}\sum_{j=1}^{C}l(z_{ij},t_{ij})
$$

$$
l(z_{ij},t_{ij})=u_jt_{ij}log(z_{ij})+v_j(1-t_{ij})log(1-z_{ij})
$$

计算过程
$$
w_{jk}=(1-\delta_{jk})max(1,log_2\frac{N_k}{N_j})
$$

$$
P_j=N_j/N_.
$$


$$
v=W_{c(i)}
$$

$$
u_j=\frac{1}{1-P_j}\sum_{k!=j}P_kw_{jk}
$$

**基于样本数量赋权,i类样本数量越多,错分为i类的惩罚越大**