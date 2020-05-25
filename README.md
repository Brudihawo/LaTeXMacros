# LatexMacros for TexStudio
  Just a couple of macros for TexStudio to increase quality of life. The aim is to reduce the ammount of special characters typed and therefore increase typing speed.  

## List of Macros
### Environment-Style Macros
Macros for creating a LaTeX environment of some sort.
#### Figure - #fimg
Replaces the #fimg with a figure blank. Markers are set for width and filepath. By default, the image path is assumed as "img/...".  
```
\begin{figure}[H]
  \centering
  \includegraphics[width=%<Breite%>\textwidth]{img/%<Speicherort%>}
\end{figure}
```

#### Math Text (Alt + Shift + I)  
Inserts math text mode  
```
\text{%<Text%>}
```

#### Itemize - #itm#  
Inserts itemize with "-" as label.  
```
\begin{itemize}[label=-]
  %<Content..%>
\end{itemize}
```

#### Table - #tab
Inserts a tabulary table environment with jump markers.
```
\begin{tabulary}{%<Width%>}{%<Column Config%>}
	%<Content%>
\end{tabulary}
```

### Insert-Style Macros
Macros that insert a piece of latex code as a shorthand.
#### Initialization - #init
Some frequently used packages for quickly initializing documents.  
**Inserted LaTeX:**
```
\documentclass[12pt, reqno]{article}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}

\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{mathtools}

\usepackage[hidelinks]{hyperref}	

\usepackage{enumitem}
\usepackage{xcolor}
\usepackage{graphicx}

\graphicspath{{img/}}
\usepackage[textwidth=16cm,textheight=22cm]{geometry}
\usepackage[justification=centering]{caption}
```

#### Textwidth variable Shorthand #tw
Shorthand for the LaTeX variable for textwidth.  
```
\textwidth
```



