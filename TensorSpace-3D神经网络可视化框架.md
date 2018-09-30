---
title: TensorSpace-3D神经网络可视化框架
date: 2018-09-28 16:00:20
tags:
- Visualization
- Machine Learning
categories:
- Machine Learning
---

【阅读时间】文档介绍类文章
【阅读内容】TensorSpace - 是一款3D模型可视化框架，支持多种模型，帮助你可视化层间输出，更直观的展示模型的输入输出，帮助理解模型结构，输出方法

<!-- more -->

# Conv2d ![#FFFF2E](https://placehold.it/15/FFFF2E/000000?text=+) 

## 构造器
```JavaScript
TSP.layers.Conv2d( { fileter : Int } )  
```

### 参数列表

#### ⭐️ 必要参数

> 使用时必须提供，不能为空
> 只要提供了这些参数，就能正常创建实例，控制参数使用`默认值`

[filters]() : `Int` 特征提取过滤器的数量

#### 🔧 推荐参数

> 使用时推荐给定，未给定可以运行，但在体验和易用性上有隐患

[name]() : `string` 层的命名，强烈建议添加

[padding]() : `string` 是否使用padding
- `valid`(default) 不使用padding，丢弃无法提取特征的部分，会改变输出的形状
- `same` 使用padding，在不够的位置补零 ，输出的形状不变

#### ⚙️可选参数

> 根据模型配置参数**选择性添加**
> 这里的参数对于层的结构（3D可视化外观）没有影响

[shape]() : `[Int]` 
- 有此参数，会覆盖除了`filters`的其他参数的影响，Dataformat默认通道值在最后
- 例如，令`shape = [ 28, 28, 6 ]`，则表示输出为6个特征图，每幅图大小`28*28` 

[kernelSize]() : `Int` 卷积核的尺寸，2d卷积核为正方形

[strides]() : `Int` 卷积移动框的移动步长，在不同方向的步长相等

#### 🎨 外观参数

> 可覆盖`TSP.model.Sequential`下的属性进行细调，[详情点击]()

[color]() : `color format` 层的颜色，默认颜色是**亮黄色** #FFFF2E

`closeButton` : `Dict` 层关闭按钮外观控制列表
- [display]() : `Bool` `true` 显示按钮 | `false` 隐藏按钮
- [ratio]() : `Int` 为正常大小的几倍.例如，设为2为正常大小的2倍大
```javascript
closeButton {
    display: false,
    ratio: 2,
}
```

#### 🎦 动画控制参数

> 可覆盖`TSP.model.Sequential`下的属性进行细调，[详情点击]()

[initStatus]() : `string` 初始化时，本层是否收缩
- `close`(default) : 收缩
- `open` : 展开

[animationTimeRatio]() : `Int` 张开和伸缩的调整速度，呈倍速关系，例如2就是2倍，**数字越大速度越快**

### 参数列表

|        参数名<br />标签         |      类型      |               简介               |                      具体用法细节和例子                      |
| :-----------------------------: | :------------: | :------------------------------: | :----------------------------------------------------------: |
|      [filters]() <br />⭐️📦       |     `Int`      |       特征提取过滤器的数量       |                        `filters: 16`                         |
|        [name]() <br />🔧         |    `String`    |      层的命名，强烈建议添加      |                     `name: "layerName" `                     |
|      [padding]() <br />🔧📦       |    `String`    |         是否使用padding          | `valid`[default] 不使用padding，丢弃无法提取特征的部分，会改变输出的形状<br />`same` 使用padding，在不够的位置补零 ，输出的形状不变 |
|       [shape]() <br />⚙️📦        |    `[Int]`     |         当前层的输出形状         | 有此参数，会覆盖除了`filters`的其他参数的影响<br />Dataformat默认通道值在最后<br />例如，`shape = [ 28, 28, 6 ]`，则表示输出为6个特征图，每幅图大小`28*28` |
|     [kernelSize]() <br />⚙️📦     |     `Int`      |           卷积核的尺寸           |               2d卷积核为正方形 `kernelSize: 3`               |
|      [strides]() <br />⚙️📦       |    `[Int]`     |       卷积移动框的移动步长       |  在不同方向的步长相等，默认情况自动推断 `strides = [1, 1]`   |
|       [color]() <br />⚙️🎨        | `color format` |             层的颜色             | `Conv2d`默认颜色是**亮黄色** #FFFF2E![#FFFF2E](https://placehold.it/15/FFFF2E/000000?text=+) |
|     `closeButton`* <br />⚙️🎨      |     `Dict`     |    层关闭按钮外观控制**列表**    | [display]() : `Bool`  `true` [default] 显示按钮 `false` 隐藏按钮<br />[ratio]() : `Int` 为正常大小的几倍，默认为1倍<br />例如，设为2为正常大小的2倍大 |
|     [initStatus]() <br />⚙️🎦     |    `String`    |      初始化时，本层是否收缩      |           `close`[default] : 收缩 | `open` : 展开            |
| [animationTimeRatio]() <br />⚙️🎦 |     `Int`      | 张开和伸缩的调整速度，呈倍速关系 |              例如2就是2倍，**数字越大速度越快**              |

*`closeButton` 例子
```javascript
closeButton {
    display: false,
    ratio: 2,
}
```
### 标签详情

| 符号 | 参数性质 |                             说明                             |
| :--: | :------: | :----------------------------------------------------------: |
|  ⭐️   |   必要   | 使用时必须提供，不能为空<br/>只要提供了这些参数，就能正常创建实例，控制参数使用`默认值` |
|  🔧   |   推荐   |  使用时推荐给定，未给定也可以运行，但在体验和易用性上有隐患  |
|  ⚙️   |   可选   | 根据模型配置参数**选择性添加**<br/>这里的参数对于层的结构（3D可视化外观）没有影响 |
|  📦   |   模型   |        配置卷积层的相关属性，并对输出特征图形状有影响        |
|  🎨   |   外观   |  可覆盖`TSP.model.Sequential`下的属性进行细调，[详情点击]()  |
|  🎦   | 动画控制 |  可覆盖`TSP.model.Sequential`下的属性进行细调，[详情点击]()  |

### 调用结果

- 创建一个新的对象，往3D场景中添加一个新的**3D可视化卷积层**
- 默认颜色: #FFFF2E  ![#FFFF2E](https://placehold.it/15/FFFF2E/000000?text=+) 

<div align="left"><img src="https://github.com/zchholmes/tsp_image/blob/master/Document/Conv2D.png" alt="" width="700"></div>


## 属性

### [.inputShape]() : [Int]

> 在 `model.init()` 后才可拿到数据，否则为`undefined`

本层**输入Tensor**的形状，Dataformat默认通道值在最后，例如`inputShape = [ 28, 28, 2 ]` 表示输入为`3`个特征图，每个图大小为`28*28`

### [.outputShape]() : [Int]

> 在 `model.init()` 后才可拿到数据，否则为`undefined`

本层**输出Tensor**的形状，Dataformat默认通道值在最后，例如`outputShape = [ 32, 32, 4 ]`  表示经过此层处理后，有`4`个特征图，每个图大小为`32*32`

### [.neuralValue]() : [float32]

> 载入模型，在 `model.predict()` 后才可以拿到数据，否则为`undefined`

本层的**层间输出**值数组

### [.name]() : string

> 创建后即可取到

本层的自定义名称

### [.layerType]() : string

> 创建后即可取到

本层的类型，返回一个定值，字符串`Conv2d`

## 方法

### [.openLayer()]() : void

（1）通过直接和3d场景中物体交互`直接点击层`打开

<div align="left"><img src="https://github.com/zchholmes/tsp_image/blob/master/Document/Conv2d-open.gif" alt="" width="400"></div>

（2）代码中通过调用方法打开

```javascript
model.init();
TSP.layers.Conv2d.openLayer()
```

### [.closeLayer()]() : void

（1）通过直接和3d场景中物体交互`点击按钮`关闭

<div align="left"><img src="https://github.com/zchholmes/tsp_image/blob/master/Document/Conv2d-close.gif" alt="" width="400"></div>

（2）代码中通过调用方法打开

```javascript
model.init();
// if this layer already opened
TSP.layers.Conv2d.closeLayer()
```

## 使用样例

### 添加层

（1）声明一个`Conv2D`的实例，方便复用

```javascript
let convLayer = new TSP.layers.Conv2d({
    kernelSize: 5,
    filters: 6,
    strides: 1,
    animationTimeRatio: 2,
    name: "conv2d1",
    initStatus: "open",
});
model.add(convLayer);
```

（2）直接添加`Conv2D`

```javascript
model.add(new TSP.layers.Conv2d({
    kernelSize: 5,
    filters: 16,
    strides: 1,
    name: "conv2d2"
}));
```

### 什么时候用

如果你是`Keras` | `TensorFlow` | `tfjs` 框架的使用者，构建模型时使用了**卷积层**`Conv2D`（下表列出了可能的使用情景）。一一对应的，在`TensorSpace`中，你应该使用此API

| 框架名称 | 文档格式 | 样例代码段 |
| :---: | :---: | :---: |
| [Keras](https://keras.io/layers/convolutional/) | keras.layers.Conv2D([filters](), [kernel_size](), [strides]()=(1, 1)) | model.add(Conv2D(32, (3, 3))) |
| [TensorFlow](https://www.tensorflow.org/api_docs/python/tf/nn/conv2d) | tf.nn.conv2d(input, [filter](), [strides](), [padding]()) | x = tf.nn.conv2d(x, W, strides=[1, strides, strides, 1], padding='SAME') |
| [TensorFlow.js](https://js.tensorflow.org/api/0.13.0/#layers.conv2d) | tf.layers.conv2d ([filters](), [kernelSize]()) | model.add(tf.layers.conv2d({kernelSize: 3, filters: 32, activation: 'relu'})); |

### 源码

[tensorspace/src/layer/intemediate/Conv2d.js](https://github.com/syt123450/tensorspace/blob/master/src/layer/intemediate/Conv2d.js)