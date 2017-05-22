# 基于并行BP神经网络的人脸识别系统

## 使用说明

### 配置路径

解压 `data` 文件夹中的数据集，使解压后 `faces` 在 `data` 文件夹下。

修改 `src/face-recognizer` 下的 `*.list` 文件，使文件内各图片路径正确。

### 编译

在终端进入 `src/face-recognizer` 进行编译：

	make
	

### 训练并测试

在终端进入 `src/face-recognizer` 进行运行（训练并测试）：

	./facetrain -n shades.net -t all_train.list -1 all_test2.list -2 all_test2.list -e 100
	
### 测试

	./facetrain -n shades.net -1 all_test2.list -2 all_test2.list
	
	
## 模块说明

* pgmimage.c, pgmimage.h
	* 处理图片的模块
	* 支持读写 PGM 文件和像素的存取/赋值
	* 提供了 IMAGE 数据结构和 IMAGELIST 数据结构（图片的数组，在处理许多图片时有用）

* backprop.c, backprop.h
	* 神经网络模块
	* 支持三层全连接前馈神经网络
	* 使用 backpropagation 算法来调整权值
	* 提供高等级的程序来创造、训练和使用神经网络
	
* iamgenet.c
	* 用于装载图片到网络的输入单元，和设置训练的目标向量的接口程序
	* 当实现 face recognizer 的时候，需要修改 load_target，根据你选择的输入编码设置合适的目标向量

* facetrain.c
	* 顶层程序，使用以上所有模块来实现一个“TA”识别器
	* 修改这个代码来改变神经网络的大小和学习参数，这两个是无关紧要的改变
	* 表现评估程序 performance_on_imagelist() 和 evaluate_performance() 都在此模块中，修改他们来实现 face recognizer。
	
* hidtopgm.c
	* 隐藏单元权值可视化程序

## 参数说明

facetrain 参数的一些说明
* -n \<network file>
	* 装载一个已存在的网络文件，或用所给的名字创建一个新的网络文件
	* 在训练最后，神经网络会被保存砸这个文件中
	
* -e \<number of epochs>	* 训练次数
	* 默认为 100

* -s \<seed>
	* 随机数产生器的种子
	* 默认为 102194
	* 围边种子尝试不同的随机数序列来重新实验

* -S \<number of epochs between saves>
	* 保存网络所需要的最小训练次数
	
* -t \<training image list>	* 指定训练集	* 如果没有这个参数，意味着没有训练（训练集都是0），网络直接在测试集上跑
* -1 \<test set 1 list>
	* 指定测试集1
	* 如果没有这个参数，测试集1都是0

* -2 \<test set 2 list>	* 指定测试集2
	* 如果没有这个参数，测试集2都是0

## 数据集

[Neural Networks for Face Recognition](http://www.cs.cmu.edu/afs/cs.cmu.edu/user/mitchell/ftp/faces.html)

## Thanks

[Github . yanshengjia/artificial-intelligence](https://github.com/yanshengjia/artificial-intelligence)
