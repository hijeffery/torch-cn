# 说明：
module是nn的基本功能单元，对于新的计算方法，或者网络层，可以在继承module的基础上进行功能设计。

## 函数：
forward()
    - updateoutput()
backward()
    - updategradInput()
    - accGradparameters()