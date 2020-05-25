# LatexMacros for TexStudio

Just a couple of macros for TexStudio to increase quality of life. The aim is to reduce the ammount of special characters typed and therefore increase typing speed.

## List of Macros
### Figure - #fimg
  Replaces the #fimg with a figure blank. Markers are set for width and filepath. By default, the image path is assumed as "img/...".
  LaTeX Code:
  ´´´
  \begin{figure}[H]
    \centering
    \includegraphics[width=%<Breite%>\textwidth]{img/%<Speicherort%>}
  \end{figure}
  ´´´
