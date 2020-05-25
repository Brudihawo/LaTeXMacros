# LatexMacros for TexStudio

Just a couple of macros for TexStudio to increase quality of life. The aim is to reduce the ammount of special characters typed and therefore increase typing speed.  

## List of Macros
### Figure - #fimg
  Replaces the #fimg with a figure blank. Markers are set for width and filepath. By default, the image path is assumed as "img/...".  
  **Inserted LaTeX:**  
  ```
  \begin{figure}[H]
    \centering
    \includegraphics[width=%<Breite%>\textwidth]{img/%<Speicherort%>}
  \end{figure}
  ```
### Textwidth variable Shorthand #tw
  Shorthand for the LaTeX variable for textwidth.  
  **Inserted LaTeX:**  
  ``` \textwidth ```
 
### Math Text (Alt + Shift + I)  
  Inserts math text mode  
  **Inserted LaTeX:**  
  ```\text{%<Text%>}```
  
### Itemize - #itm#  
  Inserts itemize with "-" as label.  
  **Inserted LaTeX:**  
  ```
  \begin{itemize}[label=-]
	  %<Content..%>
  \end{itemize}
  ```
