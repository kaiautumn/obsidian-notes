[[1HTML]]
# 一、基础选择器、文字控制属性
书写：head标签里，title标签下，添加style双标签里写CSS代码
```html
<title>CSS体验</title>
<style>
	/*选择器{CSS属性}*/
	p {
	color:red;
	}
</style>

<p>体验CSS</p>
```
CSS引入方式
>- 内部样式表：CSS写在style标签里，适合学习
>- 外部样式表：CSS的全部写在单独的CSS文件中( .css )，不需要写style标签，在HTML使用 link 标签引入，适合开发
> \<link rel="stylesheet" href="./my.css">，link 标签放在head里
>- 行内样式：配合 javascript 使用：CSS写在标签的 style 属性里
>\<div style="color : red ; font-size:20px;">这是div标签\</div>

# 二、基础选择器
#### 标签选择器
如上：使用标签名作为选择器，使得同名选择器被设置为一样的样式，无法差异化同名标签的样式。
#### 类选择器
查找标签，差异化同名标签的显示效果
>1. 定义类选择器->.类名
>2. 使用类选择器->标签加 class="类名"

```html
<style>
	.red {
		color:red;
	}
</style>

<div class="red">这是div红色标签</div>
```
 一个标签不能加多个class，想要的话只能一个class后加多个属性值，中间用空格隔开
 ```html
 <div class="red size">这是改后的div标签</div>
 ```

#### id标签
 作用：查找标签，差异化设置标签的显示效果
 场景：id选择器一般配合js使用，很少用来设置CSS样式
 ```html
<style>
	#red {
		color:red;
	}
</style>

<div id="red">这是div红色标签</div>
 ```
 同一个id选择器在一个页面里只能用一次
#### 通配符选择器
作用：查找页面所有标签，设置相同样式
```html
*{
	color: red;
}
```
# 三、画盒子
使用合适的选择器画盒子

| 属性名               | 作用  |
| ----------------- | --- |
| width             | 宽度  |
| height            | 高度  |
| backcground-color | 背景色 |
```html
<style>
.div1 {
    color:lightgreen;
    width: 200px;
    height: 100px;
    background-color: lightblue;
}
</style>
<div class="div1"></div>
```
# 文字控制属性
- 字体大小：font-size
font-size: 30px
- 字体粗细：font-weight
font-weight: 400(或normal，正常)/700(或bold，加粗)
- 字体倾斜：font-style
font-style: italic(倾斜)/normal(强行掰正)
- 行高，用于控制两行之间的距离：line-height
line-height: 20px/20(当前属性值的倍数)