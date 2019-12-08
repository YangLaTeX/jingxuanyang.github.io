---
layout: post
title:  "Operations Research Homework 1"
date:   2019-11-27
categories: operations research
tags: operations research homework
excerpt: solutions to operations research homework1
mathjax: true
---

This is operations research homework 1, [repo link]: https://github.com/JingXuan-Yang/Operations-Research-Solutions/blob/master/Homework1.

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
  \item The Primo Insurance Company is introducing two new product lines: special risk insurance and mortgages. The expected profit is \$5 per unit on special risk insurance and \$2 per unit on mortgages. Management wishes to establish sales quotas for the new product lines to maximize total expected profit. The work requirements are as follows:
  \begin{figure}[htbp]
  	\centering
  	\includegraphics[width = 0.5\textwidth]{fig3-1-9}
  \end{figure}

    \begin{enumerate}
    \item Formulate a linear programming model for this problem.
     \begin{enumerate}
     	\item Decision variables:
     	\begin{equation*}
     	\begin{aligned}
     	x_1&=\text{number of special risk insurances}\\
     	x_2&=\text{number of mortgages}\\
     	\end{aligned}
     	\end{equation*}
     	\item Objective function:
     	\begin{equation*}
     		\max\quad Z=5x_1+2x_2
     	\end{equation*}
     	\item Constraints:
     	\begin{equation*}
     	\begin{aligned}
     	3x_1+2x_2&\ls 2400\\
     	x_2&\ls 800\\
     	2x_1&\ls 1200\\
     	x_1,\ x_2&\gs 0\\
     	\end{aligned}
     	\end{equation*}
     \end{enumerate} 
    \item Use the graphical method to solve this model.
    
    \hspace{2em} First draw the feasible region, which is the shaded area shown in Fig.\ref{gra1}. Then use the slope-intercept form of the objective function to find the optimal solution, which passes through the CPF $(600,300)$.
               \begin{figure}[htbp]
              	\centering
              	\includegraphics[width = 0.3\textwidth]{graph1}
              	\caption{graphical solution}
              	\label{gra1}
              \end{figure}  
          
          Therefore, the optimal solution is $x_1=600,\ x_2=300$, with $Z=3600$.
    \end{enumerate}

% second excerise
  \item A cargo plane has three compartments for storing cargo: front, center, and back. These compartments have capacity limits on both weight and space, as summarized below:
   \begin{figure}[htbp]
  	\centering
  	\includegraphics[width = 0.5\textwidth]{fig3-4-14}
  \end{figure}  

Furthermore, the weight of the cargo in the respective compartments must be the same proportion of that compartment's weight capacity to maintain the balance of the airplane. 

\hspace{2em} The following four cargoes have been offered for shipment on an upcoming flight as space is available:
   \begin{figure}[htbp]
	\centering
	\includegraphics[width = 0.5\textwidth]{fig3-4-14-2}
\end{figure}  

Any portion of these cargoes can be accepted. The objective is to determine how much (if any) of each cargo should be accepted and how to distribute each among the compartments to maximize the total profit for the flight.
\begin{enumerate}
	\item Formulate a linear programming model for this problem.
	\begin{enumerate}
		\item Decision variables:
		
		$x_{ij}:=$ tons of cargo $i$ in compartment $j$, $i=1,2,3,4,\ j=1,2,3$, listed in Tab.\ref{tab1}.
			\begin{table}[h]
				\centering
				\caption{Decision variables}
				\label{tab1}
				\begin{tabular}{cccc}
					\toprule[1.5pt]
					Cargo&Front&Center&Back\\
					\midrule[0.5pt]
					1&$x_{11}$&$x_{12}$&$x_{13}$\\
					2&$x_{21}$&$x_{22}$&$x_{23}$\\
					3&$x_{31}$&$x_{32}$&$x_{33}$\\
					4&$x_{41}$&$x_{42}$&$x_{43}$\\
					\bottomrule[1.5pt]
				\end{tabular}
			\end{table}
		\item Objective function:
		\begin{equation*}
		\max \quad	Z=320\sum_{k=1}^{3}x_{1k}+400\sum_{k=1}^{3}x_{2k}+360\sum_{k=1}^{3}x_{3k}+290\sum_{k=1}^{3}x_{4k}
		\end{equation*}
		\item Constraints:
		
		1. Usable weight in each compartment:
		\begin{equation*}
		\sum_{j=1}^{4}x_{j1}\ls 12,\ \sum_{j=1}^{4}x_{j2}\ls 18,\ \sum_{j=1}^{4}x_{j3}\ls 10
		\end{equation*}
		
		2. Available space in each compartment:
		\begin{equation*}
		\begin{aligned}
		500 x_{11}+700x_{21}+600x_{31}+400x_{41}&\ls 7000\\
		500 x_{12}+700x_{22}+600x_{32}+400x_{42}&\ls 9000\\
		500 x_{13}+700x_{23}+600x_{33}+400x_{43}&\ls 5000\\
		\end{aligned}
		\end{equation*}
		
		3. Total cargoes of each kind:
		\begin{equation*}		
			\sum_{k=1}^{3}x_{1k}\ls 20,\ 
			\sum_{k=1}^{3}x_{2k}\ls 16,\ 
			\sum_{k=1}^{3}x_{3k}\ls 25,\ 
			\sum_{k=1}^{3}x_{4k}\ls 13			
		\end{equation*}
		
		4. Equal weight proportion of cargoes in each compartment:
		\begin{equation*}
		\begin{aligned}
		\dfrac{\sum_{j=1}^{4}x_{j1}}{12}
		=\dfrac{\sum_{j=1}^{4}x_{j2}}{18}
		=\dfrac{\sum_{j=1}^{4}x_{j3}}{10}
		\end{aligned}
		\end{equation*}
		
		5. Nonnegativity:
		\begin{equation*}
		x_{ij}\gs 0,\ i=1,2,3,4,\ j=1,2,3.
		\end{equation*}
	\end{enumerate}
	
\end{enumerate}

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

