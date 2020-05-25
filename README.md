# LatexMacros for TexStudio

Just a couple of macros for TexStudio to increase quality of life. The aim is to reduce the ammount of special characters typed and therefore increase typing speed.  

## List of Macros
### Environment-Style Macros
#### Figure - #fimg
  Replaces the #fimg with a figure blank. Markers are set for width and filepath. By default, the image path is assumed as "img/...".  
  **Inserted LaTeX:**  
  ```
  \begin{figure}[H]
    \centering
    \includegraphics[width=%<Breite%>\textwidth]{img/%<Speicherort%>}
  \end{figure}
  ```
#### Textwidth variable Shorthand #tw
  Shorthand for the LaTeX variable for textwidth.  
  **Inserted LaTeX:**  
  ``` \textwidth ```
 
#### Math Text (Alt + Shift + I)  
  Inserts math text mode  
  **Inserted LaTeX:**  
  ```\text{%<Text%>}```
  
#### Itemize - #itm#  
  Inserts itemize with "-" as label.  
  **Inserted LaTeX:**  
  ```
  \begin{itemize}[label=-]
	  %<Content..%>
  \end{itemize}
  ```
  
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
  
