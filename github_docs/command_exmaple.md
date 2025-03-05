
下载本仓库，将会得到`附件2：本科毕业设计（论文）格式范例（工科、理科类专业).doc`该文件的$\LaTeX$版本，下面是command 演示。

## `main.tex`

```tex
\documentclass{scutthesis} % 不填充空白页。如果需要双面打印版，请注释掉本行并启用下一行
%\documentclass[print-both-sides]{scutthesis} % 使用双面打印版（填充额外空白页以保证每一章开头都在奇数页）
% 开始使用该模板请修改以下文件
\input{docs/info}     % 在这里填写论文相关信息
\input{docs/abstract}     % 在这里填写摘要内容注意华工要求关键词用分号分隔
\begin{document}
% 论文前置部分
\frontmatter
\pagenumbering{Roman}
\makeUndergraduateCover    % 生成封面
\makedisclaim
%\makedisclaim[title.png]            % 生成学位论文原创性声明
% 将title.png替换为自己的签名文件，如果不需要签名的话，可以直接使用\makedisclaim命令
\makeabstract       % 生成中英文摘要
\maketableofcontents        % 生成目录
\makelistoffiguretable % 生成图表目录
% 论文主体部分
\mainmatter
% 引言
% 正文
\include{docs/chap01} % 使用include导入章节tex文件
\newclearpage
\include{docs/chap02}
\newclearpage
\include{docs/chap03}
\newclearpage
\include{docs/chap04}
\newclearpage
% 论文后置部分
\backmatter
\include{docs/conclusion} % 制作结论章节
\newclearpage
% 参考文献
\makereferences % 制作参考文献
% 致谢
\include{docs/ack} % 制作致谢
\newclearpage
% 附录部分
% 附录
{
    \appendix
    \include{docs/appendix1} % 导入附录
    \newclearpage
}
\end{document}
```

## 字体字号等格式设置

### 字号设置

```tex
\zihao{#1}
```

`#1`参数为字号，例如`\zihao{2}`为二号，使用负数表示小号，如`zihao{-4}`为小四号。

### 字体设置

```tex
\heiti % 使用黑体
\songti % 使用宋体
\textbf % 加粗字体（为满足学校规范，加粗均为使用描边伪粗体）
```

## 表格

```tex
\begin{table}[htbp]
    \centering
    \caption{ABCvsA数字识别实验结果}
    \label{tab:1}
    \begin{tabular}{@{}cccc@{}}
        \toprule
        训练样本 & ABC & 样本个数    & 3000    \\ \midrule
        测试样本 & A   & 样本个数    & 1000    \\
        训练次数 & —   & 单次训练样本数 & 10      \\
        学习率  & 1   & 正确率     & 99.50\% \\ \bottomrule
    \end{tabular}
\end{table}
```

表格均使用三线表，使用示例如上。

## 图片

### 导入图片

```tex
\begin{figure}[htbp] % image examples
    \centering
    \includegraphics[height=6.54cm]{image/chap04/1.jpg}
    \caption{ABCvsA数字识别实验集}
    \label{fig:fig1}
\end{figure}
```

图片均需要将标题置于图片下方

### 图片并列

使用`subfigure`环境画子图

![image-20230410163713231](https://raw.githubusercontent.com/ShevonKuan/images/main/image-20230410163713231.png)

```tex
\begin{figure}[htbp] % image examples & compare
    \begin{subfigure}{0.5\textwidth}
        \centering
        \includegraphics[height=6.54cm]{image/chap04/1.jpg}
        \caption{实验训练集}
        \label{fig:compare1}
    \end{subfigure}
    \begin{subfigure}{0.5\textwidth}
        \centering
        \includegraphics[height=6.54cm]{image/chap04/2.jpg}
        \caption{实验测试集}
        \label{fig:compare2}
    \end{subfigure}
    \caption{ABCvsA数字识别实验集}
    \label{fig:complex}
\end{figure}
```

## 交叉引用和参考文献引用

### 参考文献

参考文献均使用 bibtex 的形式记录在`main.bib`文件中，当需要引用时可使用`\cite`和`\overcite\`两个命令引用，前者为引用符号处于文本基线，后者为上标形式。如图

![image-20230410163327424](https://raw.githubusercontent.com/ShevonKuan/images/main/image-20230410163327424.png)

对应代码

```tex
\section{研究现状}
笔迹获取的方式有两种，所以鉴别方式也分为离线鉴别和在线鉴别\overcite{ref2,ref3}。在线鉴别是采用专用的数字板来实时收集书写信号。由文献\cite{ref4,ref5,ref6,ref7}可知，因为信号是实时采集的，所以能采集的数据不仅包括笔迹序列，而且可以采集到书写时的加速度、压力、速度等丰富有用的动态信息。
```

### 引用

已定义自动引用格式，所有引用图片、公式、表格等内容均使用同一个命令`\autoref{}`进行引用，该命令将会自动产生例如` 式``图 `等前置词语。

![image-20230410163611171](https://raw.githubusercontent.com/ShevonKuan/images/main/image-20230410163611171.png)

```tex
\subsection{前向传播}
如果用$l$来表示当前的网络层，那么当前网络层的输出如\autoref{eq:fp}所示：
\begin{equation}
    \label{eq:fp}
    {x^l} = f({u^l}),\text{其中}{u^l} = {W^l}{x^{l - 1}} + {b^l}
\end{equation}
```

## 代码和代码片段

### 行内代码

```tex
\code{#1}{#2}
```

`#1`为高亮语言，`#2`为代码内容

### 导入代码文件并显示

```tex
\inputcode{#1}{#2}
```

`#1`为高亮语言，`#2`为代码文件位置

### 代码片段环境（不推荐使用）

```tex
\begin{codeblock}{#1}
<代码内容>
\end{codeblock}
```

`#1`为高亮语言

### 示例

![image-20230410164319048](https://raw.githubusercontent.com/ShevonKuan/images/main/image-20230410164319048.png)![image-20230410164327185](https://raw.githubusercontent.com/ShevonKuan/images/main/image-20230410164327185.png)

```tex
\begin{codeblock}{python}
#从图片检测公式部分
#输入：图片 输出：公式列表
import sys
sys.path.append("ocr")

import cv2
import copy
import numpy as np
import time
import logging
from PIL import Image
import tools.infer.utility as utility
import tools.infer.predict_rec as predict_rec
import tools.infer.predict_det as predict_det
import tools.infer.predict_cls as predict_cls
from ppocr.utils.utility import get_image_file_list, check_and_read_gif
from ppocr.utils.logging import get_logger
from tools.infer.utility import draw_ocr_box_txt, get_rotate_crop_image
import os
import subprocess
import predict_function

#通过args控制参数
args = utility.parse_args()
args.image_dir = "./img/test13.jpg"
formula = predict_function.detect_formula_from_img(args)
print("图片包含的公式为：")
print(formula)
\end{codeblock}
也可在行内插入代码片段，例如：Python中重载加法运算符的函数为\code{python}{__add__}，类的标识符为\code{python}{class}。
% 此外，还可直接插入代码文件，例如插入\texttt{./code/demo.cpp}的效果为：
\inputcode{cpp}{code/demo.cpp}
```
