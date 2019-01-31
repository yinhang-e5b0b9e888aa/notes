# pytorch

在facebook, PyTorch用于研究，Caffe2用于生产环境

Deep learning frameworks within Facebook

Internally at Facebook, we have a unified strategy. We say PyTorch is used for all of research and Caffe 2 is used for all of production. This makes it easier for us to separate out which team does what and which tools do what. What we are seeing is, users first create a PyTorch model. When they are ready to deploy their model into production, they just convert it into a Caffe 2 model, then ship into either mobile or another platform.

  ```python
  np.random.seed(999)

  torch.manual_seed(999)
  if torch.cuda.is_available():
    torch.cuda.manual_seed_all(999)
    
  torch.bmm #  一串矩阵分别和另一串矩阵相乘
  ```
  
register_forward_hook

每一次forward计算出output之后都会被调用，实现时这个函数不应该去修改input和output的值

batch normalization一般用于conv layer或者fc layer之后

generator network的输入是一个固定维度的随机向量，然后对其进行transposed convolutions,

batch normalization, relu, 最后生成一张指定大小的图片

transposed convolution 把一个向量转换成一个指定维度的tensor，通过back propagation来学习kernel的weight

nn.Module    apply(func)    # 递归地对sub module进行func

一般用于weight initialization,    def func(module):  ....


# Pytorch 环境搭建
## conda create -n 环境名 python=3.6 matplotlib numpy
## https://developer.nvidia.com/cuda-downloads
