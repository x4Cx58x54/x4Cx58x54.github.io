---
title: LaTeX Cheatsheet
---

# $\LaTeX$ Cheatsheet

## 源文件结构
```tex
% Preamble 导言
\documentclass{article} % 短篇论文文类。 若是中长篇，则使用book文类。

% Packages
\usepackage{amsmath}        % Advanced maths typesetting
\usepackage[utf8]{inputenc} % UTF-8 support
\usepackage{hyperref}       % Link
\usepackage{graphicx}       % Picture

% Information
\title{Title}
\author{Name}
\date{\today{}}

% Main Document 正文
\begin{document}
\maketitle{}
\tebleofcontents{}
\\ % Linebreak
\newpage{}
Hello World!
\end{document}
```

```tex
\section{title}
content
\subsection{title}
content
\subsubsection{title}
Sections above are automatically numbered.
\paragraph{title}
content
\subparagraph{title}
content
```

### 主字号
```tex
\documentclass[12pt, ...]...
```

### 双面排版

`book` 类型，和奇偶数页不同处理有关
```tex
\documentclass[twoside, ...]...
```

## 主要元素

### 图片
```tex
\usepackage{graphicx}

\begin{figure}[!h]
    \centering
    \includegraphics[totalheight=50px]{img/1.png}
    \caption{标题}
    \label{1png}
\end{figure}
```

#### 子图

```tex
\begin{figure}[htb]
    \centering
    \begin{minipage}[t]{0.45\linewidth}
        \centering
        \includegraphics[totalheight=50px]{img/1.png}
        \caption{fig1}
        \label{fig1}
    \end{minipage}
    \begin{minipage}[t]{0.45\linewidth}
        \centering
        \includegraphics[totalheight=50px]{img/2.png}
        \caption{fig2}
        \label{fig2}
    \end{minipage}
    \centering
\end{figure}
```

带单独标题子图
```tex
\begin{figure}[htb]
    \centering
    \subfigure[title1]{
        \centering
        \includegraphics[totalheight=50px]{img/1.png}
    }
    \subfigure[title2]{
        \centering
        \includegraphics[totalheight=50px]{img/1.png}
    }
    \centering
    \caption{caption}
    \label{fig:1}
\end{figure}
```

#### 并列图

```tex
\begin{figure}[htb]
    \centering
    \subfigure[fig1 title]{
        \centering
        \includegraphics[totalheight=50px]{img/1.jpg}
    }
    \subfigure[fig1 title]{
        \centering
        \includegraphics[totalheight=50px]{img/2.jpg}
    }
    \subfigure[fig1 title]{
        \centering
        \includegraphics[totalheight=50px]{img/3.jpg}
    }
    \centering
    \caption{title}
\end{figure}
```

### 表格

[表格生成器](http://www.tablesgenerator.com/)


#### 三线表
```tex
\usepackage{booktabs}

\begin{table}[htbp]
    \centering
    \caption{标题}
    \begin{tabular}{列对齐}
        \toprule
        a & b & c & d \\
        \midrule
        1 & 2 & 3 & 4 \\
        10 & 20 & 30 & 40 \\
        \bottomrule
    \end{tabular}
\end{table}
```
`htbp` 强制位置。`列对齐`用一组字母表示，字母数为列数。`l` 表示左对齐，`c` 表示居中，`r` 表示右对齐。如`cccc`。

#### 并列表

```tex
\begin{table}[htb]
\begin{minipage}{0.48\linewidth}
    \centering
    \caption{table1}
    \label{table1}
    \begin{tabular}{rccccr}

    \end{tabular}
\end{minipage}
\begin{minipage}{0.48\linewidth}
    \centering
    \caption{table2}
    \label{table2}
    \begin{tabular}{rccccr}

    \end{tabular}
\end{minipage}
\end{table}
```


#### 表格行高调整
```tex
\renewcommand\arraystretch{1.2}
```
在 tabular 环境开始之前使用。

### 列表

#### 有序列表
```tex
\begin{enumerate}
\item
\end{enumerate}
```
#### 无序列表
```tex
\begin{itemize}
\item
\end{itemize}
```

#### 列表间距调整
```tex
\usepackage{enumitem}

\begin{enumerate}[itemsep= 0pt, topsep = 0pt, parsep = 0pt, listparindent = 24pt, leftmargin = 24pt]
...

\begin{itemize}[itemsep= 0pt, topsep = 0pt, parsep = 0pt, listparindent = 24pt, leftmargin = 24pt]
...
```

#### 列表序号设置
```tex
\usepackage{enumerate}

\begin{enumerate}[1)]
...

\begin{itemize}[1)]
...
```

### 目录
```tex
\setcounter{tocdepth}{2}
\tableofcontents
```
默认目录深度就是2。

### 摘要
```tex
\begin{abstract}

\end{abstract}
```

### 参考文献
```tex
\begin{thebibliography}{0}
\addcontentsline{toc}{section}{参考文献}
\bibitem{标签名} 参考文献信息
\end{thebibliography}

\cite{标签名}
```

一种模板为
```tex
\clearpage
\kaishu\zihao{-4}
\begin{flushleft}
\begin{thebibliography}{0}
\addcontentsline{toc}{section}{参考文献}
%\bibitem{1} 唐朔飞. 计算机组成原理（第2版）. 北京：高等教育出版社, 2008.
\end{thebibliography}
\end{flushleft}
```

### 附录
```tex
\begin{appendix}
\ctexset{section={name={附录~,~},format={\center\heiti\zihao{3}}}}
% appendices
\end{appendix}
```

### 源代码与字体设置
```tex
\usepackage{listings}
\usepackage{fontspec}
\newfontfamily\monaco{Monaco}

\setmonofont[Mapping={}]{Monaco}

\begin{lstlisting}[breaklines=true,frame=single,basicstyle=\small\monaco,numbers=left,numberstyle=\tiny\monaco]
% code
\end{lstlisting}
```

The language is specified as `[Dialect]Language`.

### Reference
```tex
\label{标签名}

%...

\ref{标签名}
```


## 次要元素

### 横线

```tex
\noindent\rule[0.25\baselineskip]{\textwidth}{0.4pt}
```


### 插入PDF
```tex
\usepackage{pdfpages}

\includepdf{文件名}
```

### 插入 TeX 代码
不换页
```tex
\input{filename}
```

换页
```tex
\include{filename}
```

### 页码
```tex
\thispagestyle{empty}   % 该页无页码

\setcounter{page}{1}    % 设置此页从1开始
```

#### 页码编号方式
```tex
\pagenumbering{Roman}
```

#### Page n of N
```tex
\usepackage{lastpage}

\footnotesize Page \thepage\ of \pageref{LastPage}
```

### 页眉与页脚
```tex
\usepackage{fancyhdr}

\pagestyle{plain}
% 仅在底部显示页码
```

```tex
\pagestyle{fancy}                                      
\fancyhead{}
\fancyfoot{}
\renewcommand{\headrulewidth}{0.3pt}
\renewcommand{\footrulewidth}{0.3pt}     
\fancyhead[LE]{设计报告}                           
\fancyhead[RO]{\leftmark}
\fancyfoot[LE, RO]{\thepage}
```

```tex
\cfoot{}
\lhead{}
\rhead{}
```

### 空页
```tex
\clearpage
\phantom{this page was intentionally left blank.}
\clearpage
```


## 中文支持
```tex
\documentclass[UTF8]{ctexart}
\zihao{0} % 设置之后文本字号为一号
\zihao{-4} % 设置之后字号为小四号
```


### 中文标题
```tex
\usepackage{ctexcap}

\ctexset{section={name={第~,~章},format={\center\heiti\zihao{4}}}} 
\ctexset{subsection={format={\songti\zihao{-4}\textbf}}}
\ctexset{subsubsection={format={\songti\zihao{-4}\textbf}}}
\renewcommand{\abstractname}{\zihao{-4}\textbf{摘要}}
```


## 布局设置

### 页边距
```tex
\usepackage{geometry}

\geometry{top=2.54cm, bottom=2.54cm, left=3.18cm, right=3.18cm}
```

## 格式设置

### 定义新命令
```tex
\newcommand{\di}{\mathrm{d}}
```

### 章节换页并清零图片列表序号
```tex
\clearpage
\setcounter{table}{0}
\setcounter{figure}{0}
\section{总结}
```

定义新的换页章节，带序号清零
```tex
\newcommand{\sectionp}[1]{\clearpage\setcounter{table}{0}\setcounter{figure}{0}\section{#1}}
```

### 设置图片与列表编号方式
```tex
\renewcommand{\thefigure}{\thesection{}.\arabic{figure}}
\renewcommand{\thetable}{\thesection{}.\arabic{table}}
```

### 更改目录、参考文献、图片、表格名称
```tex
\renewcommand{\contentsname}{Contents}
\renewcommand{\refname}{References}
\renewcommand{\figurename}{Fig.}
\renewcommand{\tablename}{Table}
```

### 引用参考文献格式改为上标
```tex
\newcommand{\upcite}[1]{\textsuperscript{\cite{#1}}}
```