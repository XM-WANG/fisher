# 摸鱼儿

——由废青王小明开发的没什么暖用的程序。

## 简介

这是一个**上班摸鱼程序**，terminal运行fisher.py之后会模拟CNN训练的过程，看起来你好像真的在训练什么很牛逼的model。

## 适用场景

1. 当你上班的时候想发一会呆的时候，你可以运行他，然后往椅子上一靠，开始放空自己。当同事路过的时候看到你的电脑屏幕，会以为你在训练一个model。然，你并没有，嘻嘻嘻。


2. 当你工作较为弱智，与周边视觉大佬相差太大而感到格格不入的时候，你可以运行他，然后往椅子上一靠，当大佬路过的时候看到你的电脑屏幕，会以为你在训练一个model而对你刮目相看。然，你并没有，嘻嘻嘻。


3. 当6点以后你本该下班但大家都没走你也不好意思走的时候，你可以运行他，然后往椅子上一靠，塞上耳机听听德云社。当同事路过的时候看到你的电脑屏，他们惊讶大家都在混时间你居然真的在加班。然，你并没有，嘻嘻嘻。

## 环境

有个屁环境...但是我们是个很认真的readme，所以：
1. random
2. time
3. argparse
4. numpy

看到random会心一笑 :)

## 快速开始

感觉写到这readme已经要比代码多了...

```
python3 fisher.py
```
## 进阶

### gen_line()

1. 简介： 根据四个参数生成一些线性的离散点，我们假设一条线的表达式为：

   > y = k·x + init

   通过以上公式生成的（x，y）点应当全在一条线上，为了使他们有一些波动，我们引入一个噪声`bias`，和噪声的强度参数`amp`，公式变成如下形式：

   > y = k·x + init + amp·bias

   `bias` 是一个随机数，影响强度由参数`amp`控制

2. 参数介绍与返回值：

   - init：float，第一个点的y值。

   - target：float，最后一个点的y值。

   - amp：float，振幅，代表每个点距离线的距离，这个值越大生成的点就离线越远，取0时将没有偏差，所有点均位于线上。

   - iter：int，生成的x点个数。

   - 返回值：返回这条线上生成的所有x和所有y，x和y均为shape=(iter,)的numpy.array。

3. 例子：

    我们模拟cnn训练时候的precision生成，我们假设初始的precision是0.3，经过400次迭代，预期最终得到的precision是0.8，那我们可以如下设置参数：

    ```python
    x, y = gen_line(init=0.3, target=0.8, amp=0.05, iter=400)
    ```

    y就是我们最后得到的precision的值，可以用`matplotlib`将x，y画出来查看。

### 程序参数介绍：

```
python3 fisher.py -i=20 -mi=400 -ir=0.2 -tr=0.5 -ar=0.05 -ip=0.3 -tp=0.7 -ap=0.05 -il=0.7 -tl=0.1 -al=0.05
```

缩写一览：

 - i：iters，模拟每个epoch里有多少个iter

 - mx：max_iter，迭代多少次达到预期的target值

 - r：recall

 - p：precision

 - l：loss

 - i：init

 - t：target
