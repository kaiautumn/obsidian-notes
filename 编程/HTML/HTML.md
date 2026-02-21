# 一、标签
在代码中形如\<xxx\>的就是标签。
>[!note] HTML基本骨架
>
>\<html>
>  \<head>
>     \<title>标题</title>
>    \</head>
>    \<body>
>      网页主体
>    \</body>
>\</html>
>
>head部分给浏览器看，如CSS
>body主体给用户看，如图片文字
>在VSCode里，按英文!+回车键
- 快速输入标签：输入标签内部名称后回车
- 标签关系
	嵌套关系
	并列关系

```html
<开始标签> </结束标签>,结束标签多个/
```
1. 注释
```html
<!--  --\>里的内容都是注释
```
2. 标题标签、段落标签
```HTML
<h1>~<h6>共6种标签
h1一般一个网页只用一次，其他的没有限制

<p>段落内容</p>
```
3. 换行、水平线
```html
<br>单标签
<hr>水平线
```
4. 文本格式化标签（加粗、倾斜、下划线、删除线）
```html
加粗    strong b
倾斜     em    i
下划线   ins   u
删除线   del   s
```
5. 图像标签
```html
<img src="图片的URL" alt="图片无法显示时显示的文字" title="鼠标悬停时显示的文字" width="数字" height="数字">
```
6. 路径-相对路径和绝对路径
```html
相对路径：
.表示当前文件夹
..表示上一级文件夹
/表示进入某个文件夹里

绝对路径：
从盘符出发或从根目录出发
<img src="C:\Users\19220\Desktop\vscode">
斜线和反斜线都可以
```
7. 超链接标签
```html
<a href="https:www.baidu.com">跳转到百度</a>

<a href="https:www.baidu.com" target="_blank">跳转到百度</a>  实现在新窗口打开
```
> 也可以超链接到本地的路径，用相对路径
> 在开发初期，不知道超链接跳转的地址时，herf值写#表示空链接，不会跳转
```html
<a href="https://baidu.com" target="_blank">
 <img src="图片.jpg" alt="">
</a>
实现图片的超链接
```
8. 多媒体标签-音频与视频
```html
<audio src="音频的URL"> </audio>
```
> controls 显示音频控制面板
> loop 循环播放
> autoplay 自动播放
```html
<video src="视频的URL"> </video>
```
> controls 显示音频控制面板
> loop 循环播放
> muted 静音播放
> autoplay 自动播放 (仅支持在静音状态下自动播放)

# 二、列表、表格、表单
![[列表表格表单.png]]

#### 列表
分类：无序、有序、定义列表
1. 无序列表 \<ul\>、\<li\>
```html
<ul>
  <li>  </li>
  <li>  </li>
  <li>  </li>
</ul>
```
>ul标签里只能有li标签，li标签里可以包括其他的

2. 有序列表 \<ol\>、\<li\>，实现有顺序的列表
```html
<ol>
  <li>  </li>
  <li>  </li>
  <li>  </li>
</ol>
```
3. 定义列表\<dl\>嵌套\<dt\>、\<dd\>
```html
<dl>
  <dt>列表标题</dt>
  <dd>列表详情</dd>
</dl>
```