## 基本的格式
\documentclass{article}
\usepackage{makecell}
%导言区
\begin{document}
%正文内容
…………
\end{document}
%此后内容会被忽略
## PLUS
1. 注释
	%来表示注释，生成pdf格式后不会显示
2. 命令
	”\“反斜杠表示这是一个命令或者特殊符号，即能把特殊符号的特殊意义给注释掉
3. 普通文本
	标题、摘要、正文、图标标题都是普通文本
4. 在输入的时候\be，按Tab可以直接补全
## 导言区
一、\documentclass\[<options\>\]{\<class-name>}
- options是排版的参数：
	以全局地规定一些排版的参数，如字号，纸张大小，单双面等。如调用article类a4纸，基本字号是11pt,双面排版：
	
```
\documentclass[11pt,twoside,a4paper]{article}
```

- class-name:
>1. article 文章，广泛应用于科技论文、报告、说明文档
>2. report 长篇报告，具有章节结构，用于综述、长篇论文、简单的书籍
>3. book 书籍文档类，包括章节结构、前言、正文、后记
>***以上三个是“标准文档类”***
>4. proc 基于article文档类的简单学术文档模板
>5. slides 幻灯片式
>6. minimal 及其精简的文档类

二、导言区还可以用usepackage来导入宏包
```latex
\usepackage[<options>]{<package-name>}
```
在调用时可以一次性调用多个宏包，但是这种用法不要指定选项，即options不能指定：
```latex
\usepackage{tabularx,makecell,multirow}
%tabularx用于表格自适应宽度
%makecell用于更灵活地格式化单元格内容
%multirow用于合并多个行的单元格
```
三、文件的组织方式
编写长片文档的时候，将一个大的源文件分成若干小文件
1. include{\<filename\>},在读入\<filename\>前会另起一页
```latex
\documentclass{article}
\begin{document}%正文内容
\LaTeX
\include{chapter1}
\include{chapter2}
\end{document}
```
```
chapter1.tex
\section{cha1}
I love you
```
```
chapter2.tex
\section{cha2}
I love singsing
```
2. input{\<filename\>}可以直接在后面加上而不另起一页，和include往往相同
3. includeonly用于**导言区**，指定只载入某些文件，即在正文区再导入的文件不起效
4. 宏包syntonly，导言区使用\syntaxonly来不生成pdf，只检查编译错误
```latex
\usepackage{syntonly}
\syntaxonly
```

## 正文区
#### 文字、章节、引用
1. 中文排版使用ctexart来进行，支持中英混排
```latex
\documentclass{ctexart}
\begin{document}
你好English
\end{document}
```
2. 空格、分段、分页
	- 空格键和Tab键和enter键输入的空白字符视为“一个空格”，一行开头的空格忽略不计。
	- 行末的换行符视为空格，两个换行符视为空行，将文字分段。多个空行被视为一个空行，多个换行被视为一个换行。
3. 分段
	-  ==\par分段==（par前后空格）,等价于两个换行键，另起一段换行
	- ==\\\表示断行==，另起一行而不空两格。可以带参数
	- ==\hspace在文中手动插入空格==
	- ==\vspace{ } 增加段落间的垂直间距==
	- \newline也可以断行，但是不能带参数
4. 断页
	- \newpage在双栏排版中起到另一栏
	- \clearpage在双栏排版中起到下一页
5. 断词：\\-来在行的最后加上断词符号，一般来讲是自动生成的
6.  ==\verb| \par |== 两个竖线之间的东西会被原封不动的打印出来
7. 转义字符：除了上面的verb命令外，还可以用转义字符\ .   ==\textbackslash==表示反斜杠
8. 加粗字体：\textbf{ }
9. 其他字符：
	\-\-\-表示短的破折号
	\ldots{}表示省略号
	\\^{}输出^
	\\~{}输出~
#### 排版
```latex
\chapter{}  \\(sub(sub))section{}  \\paragraph   \\part
```
- 排版
	article：section、subsection、subsubsection
	report、book：chapter、section、subsection
	1. 带可选参数的变体：\\section\[< short  title>\]{\< title>}
		标题是title，目录和页眉页脚中使用< short title>参数
	2. 带星号的变体：\section*{< title >} 
		标题不带编号，不生成目录项和页眉页脚
		对于\paragraph 和 \subparagraph ，不用带星号的，生成的标题也没有编号
- **目录**
	- 在合适的地方使用==\\tableofcontents==，并且这个命令需要编译两次
	- 有时用了\chapter*{}这种不生成目录的章节标题，又想手动生成目录时，在标题后面使用：\addcontentsline{toc}{< level >}{< title >},其中level是章节层次chapter或section,< title >是出现在目录的标题
	- 目录要编译两次
- **附录**
	- ==\appendix==使用后，最高一级章节使用拉丁字母编号，从A开始
		```latex
		\appendix
		\section{标题一}
		%结果是：显示   A 标题一
		```
	- book还提供了前言、正文、后记结构的划分
		\frontmatter 前言部分，页码用小写罗马汉字，其后的\chapter不编号
		\mainmatter 正文部分，页码用阿拉伯数字，从1开始，其后的章节正常编号
		\backmatter 后记部分，页码格式不变，正常计数，其后的\chapter 不编号
- **标题页**
	- 给定标题、作者、日期
	- \title{< title >}、\author{< author >}、\date{< date >}写在导言区
	- \maketitle写在正文区
- **交叉引用**
	- \label{< label-name >}
	- 之后可在别处使用 \ref{< label-name >} 或 \pageref{< label-name >} 命令，生成交叉引用的编号和页码
- **脚注和边注**
	- \footnote{< footnote >}，大括号里的就是脚注的内容
	- \marginpar\[\]{< 边注 >}，大括号里的就是边注的内容
- **列表**
	不是表格，而是中药柜
	有序列表环境enumerate 和无序列表环境 itemize，且列表可以嵌套
	\item 可以自带一个参数，将有序列表的计数换成自定义的符号
```latex
\begin{enumerate}
	\item An item
	\begin{enumerate}
		\item A  nested item
		\item[*] A starred item
	\end{enumerate}
	\item 
\end{enumerate}
```
对于itemize，中药柜用 **·** 开头
对于description，没有任何开头


#### 表格与图片
- **对齐环境**
```latex
中对齐左对齐右对齐
\begin{center}……\end{center}
\begin{flushleft}……\end{flushleft}
\begin{flushright}……\end{flushright}
以下会涉及整个环境，直到遇到新的对齐命令或新的环境
\centering
\raggedright
\raggedleft
```

- **引用**
	quote用于引用较短的文字，首航不缩进
	quotation用于引用若干段文字，首行缩进
```latex
\begin{quote}
\end{quote}
```
- **摘要**
	只能在article和report中使用
	一般紧跟\maketitle后
```latex
\begin{abstract}
	
\end{abstract}
```
- **代码环境**
```latex
\appendix
\begin{verbatim}
	#include<iostream>
	using namespace std;
	int main(){
		return 0;
	}
\end{verbatim}
```
- **表格**
	环境：tabular
```latex
\begin{tabular}[<align>]{<column-spec>}  %<column-spec>是列格式标记   <align>控制对齐：t、b为按表格顶部、底部对齐，默认为居中对齐
<item1>&<item2>&<item3>\\                %&分隔单元格   \\来换行
\hine                                    %&在行与行之间画横线
<item1>&<item2>&<item3>\\
\end{tabular}
```

| 列格式      | 说明                  |     |
| -------- | ------------------- | --- |
| l/c/r    | 单元格左/中/右对齐，不折行      |     |
| p{width} | 单元格宽度固定为 width，自动折行 |     |
| \|       | 绘制竖线                |     |
 其中，l c r p都指的是顺延的位置的列格式
 
- **横线(三线表)**
	需要用到 usepackage{booktabs}
	\toprule、\midrule、\bootomrule绘制三线表三条线

>[!note]
>latex-tables.com  绘制表格

- **图片**
	调用 graphicx 包，使用\includegraphics命令加载图片
```latex
\includegraphics[options]{filename}
%options里有设置图片的长宽
可以直接将图片放到路径中
而图片在其他路径下时
\graphicspath{Desektop/} %更改路径
```

### 盒子与浮动体
- **浮动体**
	两种浮动体，习惯figure放图片，table放表格。可以在任何一个浮动体里放文字、公式、表格、图片等任意内容
```latex
\begin{table}[placement]


\end{table}
```
- **盒子**
```latex
\mbox{}  %生成一个基本的水平盒子
\makebox[width]{align}
```

#### 格式与参考文献
- **数学公式排版**
```latex
\usepackage{amsmath}
%行内公式
The theorem is:$a^2+b^2=c^2$ .
%行间公式
The theorem is:
\begin{equation (*)}                     %*可以不带编号
a^2+b^2=c^2 \label{pythagorean}          %既然在行间出现，那说明要在后面被引用
\end{equation}
Equation \eqref{pythagorean} is called … %eqref命令能自动为引用的公式加上圆括号

%还可以用\tag{}命令修改公式编号
\begin{equation}
a^2+b^2=c^2 \tag{*}
\end{equation}
```

- **高级数学公式与符号**
	使用Axmath转换

- **字体和字号**
	呃

- **段落格式与间距**
	\newlength{\<length command>}  %表示段落间距
	\linespread{<\factor>}                   %表示行距
	\setlength{\\leftskip}{<\length>}     %左缩进
	\setlength{\\rightskip}{<\length>}   %右缩进
	\setlength{\\parindent}{<\length>} %首行缩进
- **水平间距**
	==\hspace{ }在文中手动插入空格==
- **垂直间距**
	==\vspace{ } 增加段落间的垂直间距==
- **参考文献**
	BIBTEX
	在导言区使用 \bibliographystyle{<\bst-name>} 命令
	- 第一步：准备一份BIBTEX数据库，假设文件名为books.bib，和源代码位于同一个目录下
		即：复制文献的bibtex代码，挨个粘贴到books.txt的文件中，然后后缀改为bib
	- 第二步：在源代码添加必要的命令。设源代码名为demo.tex
		1. 使用命令\bibliographystyle设定参考文献的格式，即在导言区\bibliographystyle{plain}
		2. 其次，在正文中引用参考文献，即\cite{10623438}
		3. 后，在需要列出参考文献的位置使用\bibliography命令，即\bibliography{books}
- **绘图**
	使用AxGlyph

