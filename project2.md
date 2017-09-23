
#   css揭秘之第二章   #
date: 2017-09-18 20:55:34


>这是自己看《css揭秘》过程的学习及总结.有些地方可能有理解偏差。

<!--more-->

###   一、  背景与边框   ###

####    涉及到知识点：    ###

#####  rgba   #####

RGBA(R,G,B,A)

R：红色值。正整数 | 百分数

G：绿色值。正整数 | 百分数

B：蓝色值。正整数 | 百分数

A：Alpha透明度。取值0~1之间。

######  hsla   #####

H：Hue(色调)。0(或360)表示红色，120表示绿色，240表示蓝色，也可取其他数值来指定颜色。		  取值为：0 - 360

S：Saturation(饱和度)。取值为：0.0% - 100.0%

L：Lightness(亮度)。取值为：0.0% - 100.0%

A：Alpha透明度。取值0~1之间。


本次样例

给容器设置为白色背景和半透明白色边框。

    border:10px  solid hsla(0,0%,100%,.5);
    background: white;

效果：
	![](https://i.imgur.com/ti7rknl.png)
	[demo](https://huanranc.github.io/CSS.Secrets/project2-1)

为什么会这样呢？这涉及到css2.2的背景和边框的工作原理。[浏览器渲染原理资料](http://gomefe.github.io/2016/02/22/%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93%E5%8E%9F%E7%90%86/)

在为边框设定半透明时候，需要加上background-clip:padding-box;
因为根据浏览器渲染原理，背景颜色会优先被渲染。即我们想到的效果是边框可以透过body颜色。事实上，它透过的是它自己的背景颜色。这是无法避免的，是默认效果。所以我们需要借助background-clip的属性padding-box，这样浏览器就会用内边距的外沿来把背景裁切掉。

background-clip是用来确定背景的剪裁区域，它常用属性值有三个，分别为border-box、padding-box、content-box。

background-clip:border-box     从border（不含border）区域向外剪裁背景，默认情况下

background-clip:padding-box     从padding（不含padding）区域向外剪裁背景

background-clip:content-box     从content（不含content）区域向外剪裁背景

本次[demo](https://huanranc.github.io/CSS.Secrets/project2-1 "demo")

###   二、 多重边框   ###

####    涉及到知识点：    ###

#####  box-shadow   #####

取值：

none：无阴影

<length>①：第1个长度值用来设置对象的阴影水平偏移值。可以为负值

<length>②：第2个长度值用来设置对象的阴影垂直偏移值。可以为负值

<length>③：如果提供了第3个长度值则用来设置对象的阴影模糊值。不允许负值

<length>④：如果提供了第4个长度值则用来设置对象的阴影外延值。可以为负值

<color>：设置对象的阴影的颜色。

inset：设置对象的阴影类型为内阴影。该值为空时，则对象的阴影类型为外阴影

本次样例

box-shadow的第四参数（“扩张半径”），通过指定正值或者负值，可以让投影面积加大或者减少。一个正值的扩张半径加两个为零的偏移量及为零的模糊值，得到的投影就像一条实线的边框。

    .box-shadow {
          width: 100px;
          height: 100px;
          background: yellowgreen;
          box-shadow: 0 0 0 10px #655;
        }

box-shadow还允许用逗号分隔语法，可以创建任意数量的投影。但是，box-shadow是层层的叠加的，第一层位于最顶层，因此需要有规律的调整扩张半径。

    .box-shadow {
        width: 100px;
        height: 100px;
        background: yellowgreen;
        box-shadow: 0 0 0 10px #655,
					0 0 0 15px tomato,
					0 2px 5px 15px rgba(0, 0, 0, .6);
      }
效果图：![](https://i.imgur.com/UHn1iqb.png)

注意：

- 投影的行为和边框完全不一致，它不会影响布局，而且不会受到box-sizing的影响。不过，你还是可以通过内边距或者外边距（这取决于投影是内嵌还是外扩）来额外模拟出边框所占据的空间。

- box-shadow来模拟边框，它们并不会影响鼠标事件，比如悬停和点击效果。这时候可以给box-shadow加上个inset关键字，来使投影绘制在内圈。所以需要额外的内边距来腾出足够的空隙。


#####  outline   #####

复合属性。设置或检索对象外的线条轮廓。outline画在 <' border '> 外面
outlines相关属性不占据布局空间，不会影响元素的尺寸；
outlines可能是非矩形；
不允许类似 <' border '> 属性那样能将自身拆分为 <' border-top '> , <' border-right '> , <' border-bottom '> , <' border-left '>
对应的脚本特性为outline。

如果是只需要两层边框，可以一层常规边框，一层outline（描边）。

    background: yellowgreen;
	border: 10px solid #655;
	outline: 5px solid deeppink;

描边的还有一个属性outline-offset,这个属性允许正值和负值，它用来控制它和元素边缘之间的距离。

    background: yellowgreen;
	border-radius: 5px;
	outline: 1px dashed #ffffff;
	outline-offset: -10px;
效果图：
![](https://i.imgur.com/OWzwW2t.png)


注意：

- outline不支持逗号分隔属性，因此它只适用于双层边框。

- 边框不一定贴合border-radius属性产生的圆角，因此它的元素是圆角，但是描边还可能是直角。

本次[demo](https://huanranc.github.io/CSS.Secrets/project2-2 "demo")


###   三、 灵活的背景地位   ###

####    涉及到知识点：    ###

#####  background-position   #####

background-position它允许我们指定的背景图片距离任意角的偏移量，只要我们在偏移量前指定关键字。

    background: url(test.jpg) no-repeat #58a;
    background-position: right 10px bottom 10px;

在默认情况下，background-position是相对padding box进行偏移的，但是可以使用background-origin来改变这个情况。它默认值是padding-box，你可以修改为content-box，相对内容框偏移。

     background: url(test.jpg) no-repeat #58a;
     background-position: right 10px bottom 10px;
     background-origin: content-box;

![](https://i.imgur.com/tnoA1a7.png)

#####  calc()   #####

首先，我们是想要背景图相对于容器偏移，把背景图片定位到距离底边10px 且
距离右边20px 的位置，即希望它有一个100% - 20px 的水平偏移量，以及100% - 10px 的垂直
偏移量。我们就可以同过calc()属性来为background-position设置值。

    background: url(test.jpg) no-repeat #58a;
    background-position: calc(100% - 10px) calc(100% - 10px);

注意：

请不要忘记在calc() 函数内部的- 和+ 运算符的两侧各加一个空白符，否则会产生解析错误！这个规则如此怪异，是为了向前兼容：未来，在calc() 内部可能会允许使用关键字，而这些关键字可能会包含连字符（即减号）。


本次[demo](https://huanranc.github.io/CSS.Secrets/project2-3 "demo")