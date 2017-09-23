
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

