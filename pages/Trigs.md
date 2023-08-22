- 和角公式
	- $$ \sin(\alpha + \beta) = \sin{\alpha} \cdot \cos{\beta} + \cos{\alpha} \cdot \sin{\beta} $$
	- mnemonics
		- 撒口尬口撒
	- 衍生（2 倍角公式）
		- #+BEGIN_EXPORT latex
		  \begin{align*}
		  \sin(2\theta) &= \sin(\theta + \theta) \\
		  \sin(\theta + \theta) &= \sin{\theta} \cdot \cos{\theta} + \cos{\theta}\cdot \sin{\theta}   \\
		  \sin(\theta + \theta) &= 2(\sin{\theta} \cdot \cos{\theta}) \\
		  \end{align*}
		  #+END_EXPORT
- 奇變偶不變，正負看象限
	- #+BEGIN_EXPORT latex
	  \begin{align*}
	  &\sin(90*1 + 50) = &\cos(50) \\
	  &\sin(90*2 + 20) = &-\sin(20) \\
	  &\sin(90*3 + 30) = &-\cos(30) \\
	  &cos \rightarrow x 座標 \\
	  &sin \rightarrow y 座標 \\
	  &正負轉換看左式
	  \end{align*}
	  #+END_EXPORT
		- \begin{align*}
		  &\sin(90*1 + 50) = &\cos(50) \\
		  &\sin(90*2 + 20) = &-\sin(20) \\
		  &\sin(90*3 + 30) = &-\cos(30) \\
		  &cos \rightarrow x 座標 \\
		  &sin \rightarrow y 座標 \\
		  &正負轉換看左式
		  \end{align*}
		  #+END_EXPORT
- 餘弦定理
	- $$ c^2 = a^2 + b^2 -2ab \cdot \cos{\theta} $$
- 基礎定義
	- #+BEGIN_EXPORT latex
	  \begin{align*}
	  &\boxed{sin = \frac{對邊}{斜邊}} \\
	  &\boxed{cos = \frac{鄰邊}{斜邊}}\\
	  &\boxed{tan = \frac{對邊}{鄰邊}}
	  \end{align*}
	  #+END_EXPORT
- #+BEGIN_EXPORT latex
  \begin{document}
  
  \begin{figure}
  \centering
  \begin{subfigure}{.5\textwidth}
    \centering
    \includegraphics[width=.4\linewidth]{image1}
    \caption{A subfigure}
    \label{fig:sub1}
  \end{subfigure}%
  \begin{subfigure}{.5\textwidth}
    \centering
    \includegraphics[width=.4\linewidth]{image1}
    \caption{A subfigure}
    \label{fig:sub2}
  \end{subfigure}
  \caption{A figure with two subfigures}
  \label{fig:test}
  \end{figure}
  
  \begin{figure}
  \centering
  \begin{minipage}{.5\textwidth}
    \centering
    \includegraphics[width=.4\linewidth]{image1}
    \captionof{figure}{A figure}
    \label{fig:test1}
  \end{minipage}%
  \begin{minipage}{.5\textwidth}
    \centering
    \includegraphics[width=.4\linewidth]{image1}
    \captionof{figure}{Another figure}
    \label{fig:test2}
  \end{minipage}
  \end{figure}
  #+END_EXPORT