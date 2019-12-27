---
layout: post
title:  "Operations Research Homework 6"
date:   2019-12-20
categories: operations-research
tags: operations-research homework
author: Jingxuan Yang
---

* content
{:toc}


## Introduction


This is operations research homework 6, [original repo link](https://github.com/JingXuan-Yang/Operations-Research-Solutions/blob/master/Homework6). Corresponding textbook: Introduction to Operations Research, 10th edition, Frederick S. Hillier & Gerald J. Lieberman. The style used is Tsinghua coursework.




## Main file

```latex
% !Mode:: "TeX:UTF-8"
% !TEX program  = pdflatex
\documentclass[a4paper]{article}

% import settings, modify the number of homework in this file
\input{settings.tex}

\begin{document}
\courseheader
\name{JingXuan Yang, SZ160310217}

\begin{enumerate}
  \setlength{\itemsep}{3\parskip}

% first exercise
  \item A college student has 7 days remaining before final examinations begin in her four courses, and she wants to allocate this study time as effectively as possible. She needs at least 1 day on each course, and she likes to concentrate on just one course each day, so she wants to allocate 1, 2, 3, or 4 days to each course. Having recently taken an OR course, she decides to use dynamic programming to make these allocations to maximize the total grade points to be obtained from the four courses. She estimates that the alternative allocations for each course would yield the number of grade points shown in the following table:
  \begin{table}[h]
  	\centering
  	\begin{tabular}{ccccc}
  		\toprule[1.5pt]
  		&\multicolumn{4}{c}{Estimated Grade Points}\\
  		\cmidrule{2-5}
  		&\multicolumn{4}{c}{Course}\\
  		\cmidrule{2-5}
  		Study Days&\hspace*{0.3cm}1\hspace*{0.3cm} &\hspace*{0.3cm}2\hspace*{0.3cm}&\hspace*{0.3cm}3\hspace*{0.3cm}&\hspace*{0.3cm}4\hspace*{0.3cm}\\
  		\midrule
  		1&3& 5& 2&6\\
  		2&5&5&4&7\\
  		3&6&6&7&9\\
  		4&7&9&8&9\\
  		\bottomrule[1.5pt]
  	\end{tabular}
  \end{table}
  
Solve this problem by dynamic programming.

\begin{solution}
	
	A dynamic programming formulation for this problem is
	\begin{equation*}\left\{
		\begin{aligned}
			\text{Stage } n&=\text{course }n\\
			x_n&=\text{study days for course }n\\
			\text{State } s_n&=\text{number of study days still available to remaining courses}\\
		\end{aligned}\right.
	\end{equation*}
	Let $p_i(x_i)$ be the estimated grade points from allocating $x_i$ study days to course $i$. Then the objective function is
	
	Maximize $$Z=\sum_{i=1}^4 p_i(x_i),$$
	
	subject to
	\begin{equation*}
		\begin{aligned}
			\sum_{i=1}^4x_i&=7,\\		
			x_i \text{ are positive integers},\ i&=1,2,3,4.
		\end{aligned}
	\end{equation*}
	The recursive relationship for this problem is
	\begin{equation*}
		f_n^*(s_n)=\max\limits_{x_n}\{p_n(x_n)+f_{n+1}^*(s_n-x_n)\},
		\quad \text{for } n=1,2,3.
	\end{equation*}
	For the last stage $(n=4)$,
	\begin{equation*}
		f_4^*(s_4)=\max\limits_{x_4} \{p_4(x_4)\}.
	\end{equation*}
	Beginning with the last stage $(n=4)$,
	\begin{equation*}
		x_4^*=s_4,\quad f_4^*(s_4)=p_4(s_4),
	\end{equation*}
	which is shown in Tab.\ref{tabn4}.
	  \begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=4$}
	  	\label{tabn4}
	  	\begin{tabular}{ccc}
	  		\toprule[1.5pt]
	  		$s_4$&$f_4^*(s_4)$&$x_4^*$\\
	  		\midrule
			1&6&1\\
			2&7&2\\
			3&9&3\\
			4&9&4\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
	
	We now move backward to start from the next-to-last stage $n=3$, which is shown in Tab.\ref{tabn3}.
	\begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=3$}
	  	\label{tabn3}
	  	\begin{tabular}{ccccccc}
	  		\toprule[1.5pt]
	  		&\multicolumn{4}{c}{$f_3(s_3,x_3)=p_3(x_3)+f_4^*(s_3-x_3)$}&\\
	  		\cmidrule{2-5}
	  		\diagbox[width=3em]{$s_3$}{$x_3$}&\hspace*{0.4cm}1\hspace*{0.4cm}&\hspace*{0.4cm}2\hspace*{0.4cm}&\hspace*{0.4cm}3\hspace*{0.4cm}&\hspace*{0.4cm}4\hspace*{0.4cm}&$f_3^*(s_3)$&$x_3^*$\\
	  		\midrule
			2&8&&&&8&1\\
			3&9&10&&&10&2\\
			4&11&11&13&&13&3\\
			5&11&13&14&14&14&3 or 4\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
  	
  	We go on moving to the former stage $n=2$, which is shown in Tab.\ref{tabn2}.
  	\begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=2$}
	  	\label{tabn2}
	  	\begin{tabular}{ccccccc}
	  		\toprule[1.5pt]
	  		&\multicolumn{4}{c}{$f_2(s_2,x_2)=p_2(x_2)+f_3^*(s_2-x_2)$}&\\
	  		\cmidrule{2-5}
	  		\diagbox[width=3em]{$s_2$}{$x_2$}&\hspace*{0.4cm}1\hspace*{0.4cm}&\hspace*{0.4cm}2\hspace*{0.4cm}&\hspace*{0.4cm}3\hspace*{0.4cm}&\hspace*{0.4cm}4\hspace*{0.3cm}&$f_2^*(s_2)$&$x_2^*$\\
	  		\midrule
			3&13&&&&13&1\\
			4&15&13&&&15&1\\
			5&18&15&14&&18&1\\
			6&19&18&16&17&19&1\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
  	We now are ready to move backward to solve the original problem where we are starting from stage $(n=1)$, which is shown in Tab.\ref{tabn1}.
  	\begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=1$}
	  	\label{tabn1}
	  	\begin{tabular}{ccccccc}
	  		\toprule[1.5pt]
	  		~&\multicolumn{4}{c}{$f_1(s_1,x_1)=p_1(x_1)+f_2^*(s_1-x_1)$}&\\
	  		\cmidrule{2-5}
	  		\diagbox[width=3em]{$s_1$}{$x_1$}&\hspace*{0.4cm}1\hspace*{0.4cm}&\hspace*{0.4cm}2\hspace*{0.4cm}&\hspace*{0.4cm}3\hspace*{0.4cm}&\hspace*{0.4cm}4\hspace*{0.4cm}&$f_1^*(s_1)$&$x_1^*$\\
	  		\midrule
			7&22&23&21&20&23&2\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
  	Thus the optimal solution has $x_1^*=2$, which makes $s_2=5$, so $x_2^*=1$. Then $s_3=4$, so $x_3^*=3$, which makes $s_4=x_4^*=1$. Since $f_1^*=23$, this (2, 1, 3, 1) allocation of study days will yield an estimated total of 23 grade points.
\end{solution}

\item A company will soon be introducing a new product into a very competitive market and is currently planning its marketing strategy. The decision has been made to introduce the product in three phases. Phase 1 will feature making a special introductory offer of the product to the public at a greatly reduced price to attract first-time buyers. Phase 2 will involve an intensive advertising campaign to persuade these first-time buyers to continue purchasing the product at a regular price. It is known that another company will be introducing a new competitive product at about the time that phase 2 will end. Therefore, phase 3 will involve a follow-up advertising and promotion campaign to try to keep the regular purchasers from switching to the competitive product.

\hspace*{4ex}A total of \$4 million has been budgeted for this marketing campaign. The problem now is to determine how to allocate this money most effectively to the three phases. Let $m$ denote the initial share of the market (expressed as a percentage) attained in phase 1, $f_2$ the fraction of this market share that is retained in phase 2, and $f_3$ the fraction of the remaining market share that is retained in phase 3. Use dynamic programming to determine how to allocate the \$4 million to maximize the final share of the market for the new product, i.e., to maximize $mf_2f_3$.

\hspace*{4ex}Assume that \textit{any} amount within the total budget can be spent in each phase, where the estimated effect of spending an amount $x_i$ (in units of millions of dollars) in phase $i\ (i = 1, 2, 3)$ is
\begin{equation*}
\left\{\begin{aligned}
m&=10x_1-x_1^2\\
f_2&=0.40+0.10x_2\\
f_3&=0.60+0.07x_3\\
\end{aligned}
\right.
\end{equation*}
[\textit{Hint}: After solving for the $f_2^*(s)$ and $f_3^*(s)$ functions analytically, solve for $x_1^*$ graphically.]

\begin{solution}
	
	A dynamic programming formulation for this problem is
	\begin{equation*}\left\{
		\begin{aligned}
			\text{Stage } n&=\text{phase }n\\
			x_n&=\text{money allocated to phase }n\\
			\text{State } s_n&=\text{amount of money still available to remaining phases}\\
		\end{aligned}\right.
	\end{equation*}
	The objective function of this problem is
	
	Maximize $$Z=mf_2f_3=(10x_1-x_1^2)(0.40+0.10x_2)(0.60+0.07x_3),$$
	
	subject to
	\begin{equation*}
		\begin{aligned}
			\sum_{i=1}^3x_i&=4,\\		
			x_i&\gs0,\ i=1,2,3.
		\end{aligned}
	\end{equation*}
	
	Let $f_1=m$, the recursive relationship is
	\begin{equation*}	
		f_n^*(s_n)=\max\limits_{0\ls x_n\ls s_n}\{f_n(x_n) \cdot f_{n+1}^*(s_n-x_n)\},
		\quad \text{for } n=1,2.
	\end{equation*}
	
	For $n=3$,
	\begin{equation*}
		f_3^*(s_3)=\max\limits_{0\ls x_3\ls s_3}\{f_3(x_3)\}
	\end{equation*}
	
	Beginning with the last stage $(n=3)$, since $f_3(s_3)=0.60+0.07s_3$ is a monotonically increasing function of $s_3$, $x_3=s_3$ is the desired maximizing value. The corresponding table is shown in Tab.\ref{tab2n3}.
	\begin{table}[h]
	  	\centering
	  	\caption{Dynamic programming for $n=3$}
	  	\label{tab2n3}
	  	\begin{tabular}{ccc}
	  		\toprule[1.5pt]
	  		$s_3$&$f_3^*(s_3)$&$x_3^*$\\
	  		\midrule
			$0\ls s_3\ls4$&$0.60+0.07s_3$&$s_3$\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
  	
	We now move backward to start from the next-to-last stage $n=2$,
	\begin{equation*}
	\begin{aligned}
		f_2(s_2,x_2)&=(0.40+0.10x_2)(0.60+0.07s_3)\\
					    &=(0.40+0.10x_2)[0.60+0.07(s_2-x_2)]
		\end{aligned}
	\end{equation*}
	Let
	\begin{equation*}
	\begin{aligned}
		\frac{\partial}{\partial x_2}f_2(s_2,x_2)
		&=0.10[0.60+0.07(s_2-x_2)]-0.07(0.40+0.10x_2)\\
		&=0.06+0.007(s_2-x_2)-0.028-0.007x_2\\
		&=0.032+0.007s_2-0.014x_2\\
		&=0,\\
		\end{aligned}
	\end{equation*}
	
	which yields
	\begin{equation*}
		x_2^*=\frac{0.032+0.007s_2}{0.014}=\frac{32+7s_2}{14}.
	\end{equation*}
	
	Let $$s_2<\frac{32+7s_2}{14},$$ which yields $$s_2<\frac{32}{7}.$$
	Since $0\ls s_2\ls4$, the above inequality always holds. Therefore,
	\begin{equation*}
		\frac{\partial}{\partial x_2}f_2(s_2,x_2)>0,\quad \text{for} \ 0\ls x_2\ls s_2,
	\end{equation*}
	so that $x_2=s_2$ is the desired maximizing value. The above analysis is shown in Tab.\ref{tab2n2}.
	\begin{table}[h]
	  	\centering
	  	\caption{Dynamic programming for $n=2$}
	  	\label{tab2n2}
	  	\begin{tabular}{ccc}
	  		\toprule[1.5pt]
	  		$s_2$&$f_2^*(s_2)$&$x_2^*$\\
	  		\midrule
	  		$0\ls s_2\ls4$&$0.24+0.06s_2$&$s_2$\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
	
	For the first-stage problem $(n=1)$,
	\begin{equation*}
	\begin{aligned}
		f_1(4,x_1)&=(10x_1-x_1^2)f_2^*(s_2)\\
		&=(10x_1-x_1^2)f_2^*(4-x_1)\\
		&=(10x_1-x_1^2)[0.24+0.06(4-x_1)]\\
		&=(10x_1-x_1^2)(0.48-0.06x_1)\\
	\end{aligned}	
	\end{equation*}
	
	Let
	\begin{equation*}
	\begin{aligned}
		\frac{\partial}{\partial x_1}f_1(4,x_1)
		&=(10-2x_1)(0.48-0.06x_1)-0.06(10x_1-x_1^2)\\
		&=4.8-0.6x_1-0.96x_1+0.12x_1^2-0.6x_1+0.06x_1^2\\
		&=4.8-2.16x_1+0.18x_1^2\\
		&=0,\\
		\end{aligned}
	\end{equation*}
	
	which yields
	\begin{equation*}
		x_1^*=\frac{2.16\pm\sqrt{2.16^2-4\times0.18\times4.8}}{2\times0.18}=2.945\ \text{or}\ 9.055
	\end{equation*}
	
	The graph of $f_1(4,x_1)$ is shown in Fig.\ref{f1}. Since $0<2.945<4<9.055$, $x_1=2.945$ is the desired maximizing value, with $Z=f_1^*(4,2.945)=6.302.$
	\begin{figure}[htbp]
		\centering
		\includegraphics[width = 0.65\textwidth]{HW6}
		\caption{Graph of $f_1(4,x_1)$}
		\label{f1}
	\end{figure}
	
	The results are summarized as follows:
	\begin{table}[h]
	  	\centering
	  	\caption{Dynamic programming for $n=1$}
	  	\label{tab2n1}
	  	\begin{tabular}{ccc}
	  		\toprule[1.5pt]
	  		$s_1$&$f_1^*(s_1)$&$x_1^*$\\
	  		\midrule
	  		$4$&$6.302$&$2.945$\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
  	
	Therefore, by tracing back through the tables for $n=2,\ n=3$, respectively, and setting $s_n=x_{n-1}^*$ each time, the resulting optimal solution is $x_1^*=2.945,\ x_2^*=1.055,\ x_3^*=0,$ with a total estimated market share of 6.302\%.
\end{solution}

\item Imagine that you have \$5000 to invest and that you will have an opportunity to invest that amount in either of two investments ($A$ or $B$) at the beginning of each of the next 3 years. Both investments have uncertain returns. For investment $A$ you will either lose your money entirely or (with higher probability) get back \$10000 (a profit of \$5000) at the end of the year. For investment $B$ you will get back either just your \$5000 or (with low probability) \$10000 at the end of the year. The probabilities for these events are as follows:
  \begin{table}[h]
	\centering
	\begin{tabular}{ccc}
		\toprule[1.5pt]
		Investment&Amount Returned (\$)&Probability\\
		\midrule
		\multirow{2}*{$A$}&0&0.3\\
		&10000&0.7\\
		\multirow{2}*{$B$}&5000&0.9\\
		&10000&0.1\\
		\bottomrule[1.5pt]
	\end{tabular}
\end{table}

\hspace*{4ex}You are allowed to make at most \textit{one} investment each year, and you can invest only \$5,000 each time. (Any additional money accumulated is left idle.)

\hspace*{4ex}Use dynamic programming to find the investment policy that maximizes the expected amount of money you will have after 3 years.

\begin{solution}
	
	A dynamic programming formulation for this problem is
	\begin{equation*}\left\{
		\begin{aligned}
			\text{Stage } n&=n\text{th year}\\
			x_n&=\text{investment made at stage }n,\ x_n\in\{0,A,B\}\\
			\text{State } s_n&=\text{amount of money in hand to begin stage }n\\
		\end{aligned}\right.
	\end{equation*}
	Since the objective of this problem is to maximize the expected amount of money after 3 years,
	\begin{equation*}\left\{
		\begin{aligned}
			f_n(s_n,x_n)&=\text{total expected amount of money for stages }n,\cdots,3\ \\
			 &\quad\ \text{if system starts in state }s_n \text{ at stage }n,\ \text{immediate decision is }x_n,\ \\
			 &\quad\ \text{and optimal decisions are made }\text{thereafter,}\\
			f_n^*(s_n)&=\max\limits_{x_n}\{f_n(s_n,x_n)\}\\
		\end{aligned}\right.
	\end{equation*}
	
	Since one can not invest less than \$5000, for $0\ls s_n< 5000$, $$f_n(s_n,x_n)=f_{n+1}^*(s_n), \quad x_n^*=0$$
	
	For $s_n\gs5000,$
	\begin{equation*}f_n(s_n,x_n)=\left\{
		\begin{aligned}	
		&f_{n+1}^*(s_n), &\text{ if}\ x_n=0\, \\
		&0.3f_{n+1}^*(s_n-5000)+0.7f_{n+1}^*(s_n+5000), &\text{if}\ x_n=A\\
		&0.9f_{n+1}^*(s_n)+0.1f_{n+1}^*(s_n+5000), &\text{if}\ x_n=B\\
		\end{aligned}\right.
	\end{equation*}
	Beginning with the last stage $(n=3)$, the calculations are shown in Tab.\ref{tab33}.
	\begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=3$}
	  	\label{tab33}
	  	\begin{tabular}{cccccc}
	  		\toprule[1.5pt]
	  		&\multicolumn{3}{c}{$f_3(s_3,x_3)$}&\\
	  		\cmidrule{2-4}
	  		\diagbox[width=7em]{$s_3$}{$x_3$}&\hspace*{0.4cm}0\hspace*{0.4cm}&\hspace*{0.4cm}$A$\hspace*{0.4cm}&\hspace*{0.4cm}$B$\hspace*{0.4cm}&$f_3^*(s_3)$&$x_3^*$\\
	  		\midrule
			$0\ls s_3<5000$&$s_3$&&&$s_3$&0\\
			$s_3\gs5000$&$s_3$&$s_3+2000$&$s_3+500$&$s_3+2000$&$A$\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
	
	We now move backward to start from the next-to-last stage $n=2$, the results obtained are shown in Tab.\ref{tab32}.
	\begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=2$}
	  	\label{tab32}
	  	\begin{tabular}{cccccc}
	  		\toprule[1.5pt]
	  		&\multicolumn{3}{c}{$f_2(s_2,x_2)$}&\\
	  		\cmidrule{2-4}
	  		\diagbox[width=9em]{$s_2$}{$x_2$}&\hspace*{0.4cm}0\hspace*{0.4cm}&\hspace*{0.4cm}$A$\hspace*{0.4cm}&\hspace*{0.4cm}$B$\hspace*{0.4cm}&$f_2^*(s_2)$&$x_2^*$\\
	  		\midrule
			$0\ls s_2<5000$&$s_2$&&&$s_2$&0\\
			$5000\ls s_2<10000$&$s_2+2000$&$s_2+3400$&$s_2+2500$&$s_2+3400$&$A$\\
			$ s_2\gs10000$&$s_2+2000$&$s_2+4000$&$s_2+2500$&$s_2+4000$&$A$\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
	We now are ready to move backward to solve the original problem where we are starting from stage $(n=1)$, which is shown in Tab.\ref{tab31}.
	\begin{table}[H]
	  	\centering
	  	\caption{Dynamic programming for $n=1$}
	  	\label{tab31}
	  	\begin{tabular}{cccccc}
	  		\toprule[1.5pt]
	  		&\multicolumn{3}{c}{$f_1(s_1,x_1)$}&\\
	  		\cmidrule{2-4}
	  		\diagbox[width=5em]{$s_1$}{$x_1$}&\hspace*{0.4cm}0\hspace*{0.4cm}&\hspace*{0.4cm}$A$\hspace*{0.4cm}&\hspace*{0.4cm}$B$\hspace*{0.4cm}&$f_1^*(s_1)$&$x_1^*$\\
	  		\midrule
			$5000$&8400&9800&8960&9800&$A$\\
	  		\bottomrule[1.5pt]
	  	\end{tabular}
  	\end{table}
  	
  	Therefore, the optimal investment policy is to invest in $A$ if the money in hand is greater than or equal to \$5000, with a total expected amount of money after 3 years of \$9800.
\end{solution}

% w.r.t the external
\end{enumerate}
%  The source code to plot Figure \ref{fig:1} could be found in Appendix \ref{sec:a:code}. Here are the core codes:
%  \lstinputlisting[firstline=6,lastline=7, firstnumber=6]{matlabscript.m}

%  \newpage
%  \appendix
%  \section{Source code}
%  \label{sec:a:code}
%  % \lstlistoflistings
%  Source code for plotting Figure \ref{fig:1} is shown as follows.
%  \lstinputlisting[caption=FigurePlot]{matlabscript.m}
  
\end{document}

```

## Setting file

Associated settings file is:

```latex
\usepackage[T1]{fontenc}
\usepackage{amsmath, amssymb, amsthm}
% amsmath: equation*, amssymb: mathbb, amsthm: proof
\usepackage{moreenum}
\usepackage{multirow}
\usepackage{mathtools}
\usepackage{float}
\usepackage{url}
\usepackage{graphicx}
\usepackage{subcaption}
\usepackage{booktabs} 
\usepackage[mathcal]{eucal}
\usepackage{dsfont}
\usepackage{geometry}
\usepackage{diagbox}
\geometry{left=30mm,right=30mm,	top=42mm, bottom=33mm}

\usepackage[numbered,framed]{matlab-prettifier}
\lstset{
	style              = Matlab-editor,
	captionpos         =b,
	basicstyle         = \mlttfamily,
	escapechar         = ",
	mlshowsectionrules = true,
}

% set the homework count number
\usepackage[thehwcnt = 6]{iidef}

\newcommand\dif{\text{d}}
\newcommand\no{\noindent}
\newcommand\dis{\displaystyle}
\newcommand\ls{\leqslant}
\newcommand\gs{\geqslant}

\newcommand\limit{\dis\lim\limits}
\newcommand\limn{\dis\lim\limits_{n\to\infty}}
\newcommand\limxz{\dis\lim\limits_{x\to0}}
\newcommand\limxi{\dis\lim\limits_{x\to\infty}}
\newcommand\limxpi{\dis\lim\limits_{x\to+\infty}}
\newcommand\limxni{\dis\lim\limits_{x\to-\infty}}
\newcommand\limtpi{\dis\lim\limits_{t\to+\infty}}
\newcommand\limtni{\dis\lim\limits_{t\to-\infty}}

\newcommand\sumn{\dis\sum\limits_{n=1}^{\infty}}
\newcommand\sumnz{\dis\sum\limits_{n=0}^{\infty}}

\newcommand\sumi{\dis\sum\limits_{i=1}^{\infty}}
\newcommand\sumiz{\dis\sum\limits_{i=0}^{\infty}}
\newcommand\sumin{\dis\sum\limits_{i=1}^{n}}
\newcommand\sumizn{\dis\sum\limits_{i=0}^{n}}

\newcommand\sumk{\dis\sum\limits_{k=1}^{\infty}}
\newcommand\sumkz{\dis\sum\limits_{k=0}^{\infty}}
\newcommand\sumkn{\dis\sum\limits_{k=0}^n}
\newcommand\sumkfn{\dis\sum\limits_{k=1}^n}

\newcommand\pzx{\dis\frac{\partial z}{\partial x}}
\newcommand\pzy{\dis\frac{\partial z}{\partial y}}

\newcommand\pfx{\dis\frac{\partial f}{\partial x}}
\newcommand\pfy{\dis\frac{\partial f}{\partial y}}

\newcommand\pzxx{\dis\frac{\partial^2 z}{\partial x^2}}
\newcommand\pzxy{\dis\frac{\partial^2 z}{\partial x\partial y}}
\newcommand\pzyx{\dis\frac{\partial^2 z}{\partial y\partial x}}
\newcommand\pzyy{\dis\frac{\partial^2 z}{\partial y^2}}

\newcommand\pfxx{\dis\frac{\partial^2 f}{\partial x^2}}
\newcommand\pfxy{\dis\frac{\partial^2 f}{\partial x\partial y}}
\newcommand\pfyx{\dis\frac{\partial^2 f}{\partial y\partial x}}
\newcommand\pfyy{\dis\frac{\partial^2 f}{\partial y^2}}

\newcommand\intzi{\dis\int_{0}^{+\infty}}
\newcommand\intd{\dis\int}
\newcommand\intab{\dis\int_a^b}

\newcommand{\degree}{^\circ}

\newcommand\ma{\mathcal{A}}
\newcommand\mc{\mathbf{c}}
\newcommand\me{\mathcal{E}}
\newcommand\mg{\mathcal{g}}

\newcommand\mcc{\mathbb{C}}
\newcommand\mrr{\mathbb{R}}
\newcommand\mzz{\mathbb{Z}}

\newcommand\mx{\bf{x}}
\newcommand\mX{\bf{X}}
\newcommand\my{\mathbf{y}}
\newcommand\mY{\bf{Y}}
\newcommand\mS{\mathbf{S}}
\newcommand\mb{\mathbf{b}}
\newcommand\mz{\mathbf{z}}
\newcommand\mA{\mathbf{A}}
%%=============================================

%%=====定义新数学符号===============================
\DeclareMathOperator{\sgn}{sgn}
\DeclareMathOperator{\arccot}{arccot}
\DeclareMathOperator{\arccosh}{arccosh}
\DeclareMathOperator{\arcsinh}{arcsinh}
\DeclareMathOperator{\arctanh}{arctanh}
\DeclareMathOperator{\arccoth}{arccoth}
\DeclareMathOperator{\grad}{\bf{grad}}
%\DeclareMathOperator{\argmax}{argmax}
%\DeclareMathOperator{\argmin}{argmin}
%\DeclareMathOperator{\diag}{diag}
\DeclareMathOperator{\csign}{csign}
%===============================================

\thecourseinstitute{Harbin Institute of Technology, ShenZhen}
\thecoursename{Operations Research}
\theterm{Fall 2019}
\hwname{Homework}
```
