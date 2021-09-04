# WeChat-CanvasToHaiBao
微信小程序canvas生成海报，轮播图形式展现

<br>

[详细介绍请戳这里](https://www.cnblogs.com/Jlay/p/WeChat-CanvasToHaiBao.html)


<br>

## ⭐小程序canvas生成海报

<br>

由于 `wx.createCanvasContext()` 接口不再维护，因此，我们将记录新旧接口生成海报的两种方法。

<br>

先上效果图

<br>


![](https://img2020.cnblogs.com/blog/2109948/202109/2109948-20210904224101190-244746775.png)

<br>


目前展现的是图片等元素组成、以轮播图形式展示的页面。为提高性能，采用按下保存海报按钮，再执行canvas生成海报，保存到本地相册这样一个操作。话不多说，来干！

<br>

## ⭐旧接口 `wx.createCanvasContext`

<br>

[接口文档](https://developers.weixin.qq.com/miniprogram/dev/api/canvas/CanvasContext.html)

<br>

### ①  写一个canvas对象

<br>

```html
<canvas class="hide" canvas-id="share" style="width:480px;height:854px;"></canvas>
```

<br>

注意，这里只需给他加上 `canvas-id` 等下即可获取到该对象。 hide类主要是将 此画布隐掉，让他不要出现在我们的页面中。由于canvas的特殊性，我们采用最最最简单的办法，将它定位到屏幕之外即可。

<br>

```css
.hide{
  position:fixed;
  left:9000px;
}
```

<br>

### ② 图片临时地址准备

<br>

接下来，我们就可以着手准备在画布上画上我们的海报。
<br>

首先、海报上有图片。注意，网络图片地址是不能直接被画上去的，要先转为临时地址。
<br>

当然若是本地图片，直接采用该地址即可，无需进行临时地址获取。

<br>

**ImgUrlToTmp方法** 

<br>

利用微信的 `getImageInfo` 接口，实现临时地址获取。

<br>


###  ③ canvas画布

<br>

等我们将图片地址准备好后，接下来，就正式进入我们的绘画阶段，调用 `createNewImg` 方法

<br>

之后再调用 toSave方法获取canvas地址以便于保存


### ④ 保存到本地相册

<br>

saveShareImg方法

<br>

## ⭐新接口 `createSelectorQuery`

<br>

[接口文档](https://developers.weixin.qq.com/miniprogram/dev/api/canvas/Canvas.html)
<br>


### ① 挂载一个canvas 对象

<br>

其实是类似的。 首先也是 挂载一个canvas 对象，注意，这里需要 指定 `type` 属性以及id

<br>

```html
<canvas type="2d" class="hide" id="share" style="width:480px;height:854px;"></canvas>
```

<br>

下一步也是同旧接口，就不重复阐述了。

<br>

### 画布方法改变

<br>

见代码

<br>


### 画布保存转为地址

<br>

基本一致，就是多加了个 `canvas` 属性， 也就是将 canvas 对象传进去即可

<br>

利用像素点转化，可以提升海报的高清度


<br>

来看一下保存海报的效果图

<br>

![](https://img2020.cnblogs.com/blog/2109948/202109/2109948-20210904224115425-871643926.png)


<br>




### 轮播图实现

<br>

接下来来看一下轮播图实现， 微信开发者工具中直接有个组件 `swiper`

<br>

[接口文档](https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html)

<br>

> 这里 利用 `currentIndex == index` 判断当前选中项，从而改变选中的样式再加个滑动的动画即可

<br>
