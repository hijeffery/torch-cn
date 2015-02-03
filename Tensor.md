# storage
最底层的存储结构，直接对应存储空间，跟c语言中的指针和数组相通。有longstorage 和 floatstorage 等等详细分类。Tensor可以看做是storage的特殊索引方式。

# Tensor
torch的基本数据结构，类似mat，可以进行一些矩阵操作。

## Tensor 构建
- x = torch.Tensor(3,3)
- s = torch.Longstorage(2) s[1] = 3. s[2] = 3; x = torch.Tensor(s)
- y = torch.Tensor(x)
- y = torch.Tensor(storage, [stride]) -- (share storage)
- x = torch.Tensor({{1 2  3 4},{4 3 2 1}})

tensor 可以直接赋值维数，成为多维矩阵。
也可以从其他变量赋值，或者存储空间赋值。
或者直接从table转换来，table必须是只有数字构成。

## Tensor 元素访问：
- x[2][2]
- x[{1,1}]
- x:storage()[x:storageOffset()+(2-1)*x:stride(1)+(2-1)*x:stride(2)]
可以访问某个元素或者某些元素，也可以计算物理指针的方式（类似c，较慢）。
- y = x[{{2},{}}]   matrix;
- y = x[2] dimension reduced matrix.
- y = x[{2,{}}] dimension reduced matrix.
## Tensor 赋值：
- y = x 
- y = torch.Tensor(x) -- 同上，(share storage 空间)
- y = x:clone()
- y = torch.Tensor(x:size()):copy(x)  --同clone，自己申请空间

##  Tensor 的基本查询
- x:nDimension()
- x:size()
- x:size(2)
- x:nElement()
- x:storage()
- x:storageOffset()

## share内存空间的操作
- y = x:transpose() 
- y = x:t()  -- 2D

# copy processes
- torch.reshape(x);  math() , copy space.
- x:select(2,3) ;  share space.

