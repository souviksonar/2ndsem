```tikz

\usepackage{tikz}

\begin{document}

\begin{tikzpicture}[scale=1.5]
  \tikzset{every node/.style={circle, draw, fill=gray!50, inner sep=0pt, minimum size=4pt}}
  \node (1) at (90:1) {};
  \node (2) at (162:1) {};
  \node (3) at (234:1) {};
  \node (4) at (306:1) {};
  \node (5) at (18:1) {};
  \foreach \from/\to in {1/2,1/3,1/4,1/5,2/3,2/4,2/5,3/4,3/5,4/5}
    \draw (\from) -- (\to);
\end{tikzpicture}

\end{document}

```
