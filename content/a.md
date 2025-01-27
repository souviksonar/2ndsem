```tikz
\documentclass{article}
\usepackage{tikz}
\usetikzlibrary{positioning}

\begin{figure}[h]
\centering
\begin{tikzpicture}[
    node distance=1cm,
    proc/.style={rectangle, draw, minimum size=0.8cm},
    mem/.style={rectangle, draw, minimum size=0.8cm},
    disk/.style={cylinder, draw, shape aspect=0.5, minimum size=0.8cm},
    net/.style={rectangle, draw, minimum width=3cm, minimum height=0.5cm}
]

% Shared Nothing
\node[net] (sn-net) {Interconnection Network};
\node[proc, below left=0.5cm and 1cm of sn-net] (sn-p1) {P};
\node[proc, below=of sn-p1] (sn-p2) {P};
\node[proc, below right=0.5cm and 1cm of sn-net] (sn-p3) {P};
\node[mem, left=of sn-p1] (sn-m1) {M};
\node[mem, left=of sn-p3] (sn-m3) {M};
\node[disk, below=of sn-p2] (sn-d2) {D};
\node[disk, left=of sn-d2] (sn-d1) {D};
\node[disk, right=of sn-d2] (sn-d3) {D};
\draw (sn-p1) -- (sn-net);
\draw (sn-p2) -- (sn-net);
\draw (sn-p3) -- (sn-net);
\node[below=of sn-d2, yshift=-0.5cm] {SHARED NOTHING};

% Shared Memory
\node[net, right=3cm of sn-net] (sm-net) {Interconnection Network};
\node[proc, below left=0.5cm and 1cm of sm-net] (sm-p1) {P};
\node[proc, below=of sm-p1] (sm-p2) {P};
\node[proc, below right=0.5cm and 1cm of sm-net] (sm-p3) {P};
\node[mem, below=2cm of sm-net] (sm-m) {Global Shared Memory};
\node[disk, below=of sm-p2] (sm-d2) {D};
\node[disk, left=of sm-d2] (sm-d1) {D};
\node[disk, right=of sm-d2] (sm-d3) {D};
\draw (sm-p1) -- (sm-net);
\draw (sm-p2) -- (sm-net);
\draw (sm-p3) -- (sm-net);
\draw (sm-p1) -- (sm-m);
\draw (sm-p2) -- (sm-m);
\draw (sm-p3) -- (sm-m);
\node[below=of sm-d2, yshift=-0.5cm] {SHARED MEMORY};

% Shared Disk
\node[net, right=3cm of sm-net] (sd-net) {Interconnection Network};
\node[proc, below left=0.5cm and 1cm of sd-net] (sd-p1) {P};
\node[proc, below=of sd-p1] (sd-p2) {P};
\node[proc, below right=0.5cm and 1cm of sd-net] (sd-p3) {P};
\node[mem, left=of sd-p1] (sd-m1) {M};
\node[mem, left=of sd-p3] (sd-m3) {M};
\node[disk, below=of sd-p2] (sd-d2) {D};
\node[disk, left=of sd-d2] (sd-d1) {D};
\node[disk, right=of sd-d2] (sd-d3) {D};
\draw (sd-p1) -- (sd-net);
\draw (sd-p2) -- (sd-net);
\draw (sd-p3) -- (sd-net);
\draw (sd-d1) -- (sd-net);
\draw (sd-d2) -- (sd-net);
\draw (sd-d3) -- (sd-net);
\node[below=of sd-d2, yshift=-0.5cm] {SHARED DISK};

\end{tikzpicture}
\caption{Architectures for Parallel Databases}
\end{figure}

```
