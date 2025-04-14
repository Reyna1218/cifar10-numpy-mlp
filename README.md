

# CIFAR-10 图像分类（基于 Numpy 的三层神经网络）

本项目使用 Numpy 从零构建一个三层前馈神经网络，用于对 CIFAR-10 图像数据集进行分类。该实现不依赖任何深度学习框架（如 PyTorch、TensorFlow），旨在帮助理解神经网络底层计算原理。
## 模型结构
	•	输入层：3072（32x32x3）
	•	隐藏层：128 个神经元（ReLU 或 Sigmoid 激活）
	•	输出层：10 个类别（使用 Softmax 输出概率）
	•	损失函数：交叉熵损失 + L2 正则项
	•	优化器：随机梯度下降（SGD）
	•	学习率衰减策略：支持起始 epoch 后逐步衰减

## 项目依赖

运行此项目需安装以下 Python 库：
pip install numpy matplotlib

## 数据集准备
	1.	下载 CIFAR-10 数据集（Python 版本）：
https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz
	2.	解压后，将路径设置为代码中指定路径。

## 训练模型
运行 main 逻辑（位于文件底部 if __name__ == '__main__' 部分），即可开始训练模型。

训练参数说明如下：
	•	num_epochs=40：训练轮数
	•	learning_rate=0.07：初始学习率
	•	lr_decay=0.95：每轮学习率衰减系数
	•	decay_start_epoch=8：从第 8 轮开始衰减学习率
	•	reg=1e-3：L2 正则系数
可以根据需求自行调整。

## 测试模型
训练完成后，会在测试集上评估准确率，代码如下：
test(model, X_test, y_test)


## 训练过程可视化

训练结束后会绘制以下图表：
	•	训练损失曲线（plot_training 函数）
	•	验证准确率变化曲线
	•	第一层权重可视化图像（visualize_weights 函数）


## 保存与加载模型

可以通过 numpy.savez 来保存模型参数：

np.savez("model_weights.npz", **model.params)

之后再加载：

weights = np.load("model_weights.npz")
model.params = {k: weights[k] for k in weights}



## 超参数搜索

运行 hyperparameter_search 函数，可以测试不同超参数组合在验证集上的效果，帮助选择最优配置。
项目文件结构
.
├── your_script.py               # 主程序，包括模型定义、训练、测试等
├── cifar-10-batches-py/        # CIFAR-10 原始数据目录
└── model_weights.npz           # 训练后保存的模型权重文件


## 示例结果

Epoch 40/40, Val Acc: 0.5200, LR: 0.03076
Test Accuracy: 0.5054



模型权重下载：https://drive.google.com/file/d/1640404gMIbD-MFiF1Y6ZekADDhbKsAFx/view?usp=sharing
