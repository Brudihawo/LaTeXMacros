# LatexMacros for TexStudio
A couple of TexStudio macros to improve workflow. The aim is to reduce the ammount of special characters typed and therefore increase typing speed.

## How-To
**THIS PROCESS OVERRIDES THE MACROS THAT ARE CURRENTLY IN USE.**
1. Back up your current Profile by clicking ```Options->Save Profile...``` and saving your current TexStudio profile.
2. Click ```Options->Load Profile...``` Select the ```.txsprofile``` you want to import and click ```open```.  
If you want to continue using your own macros, you can also export your own macros beforehand and reimport them afterwards or edit the ```.txsprofile``` to include your own macros. Just make sure there are no conflicts between the macros, or you might encounter unexpected behaviour.

## List of Macros
How To Read This: Macros are grouped by their style and actions: environment creation macros, code insertion macros (shorthands) and script macros for advanced editing.  
**Title Formatting:** Macro Name - Trigger, may be a regular expression (Hotkey)
Non existing triggers or Hotkeys will be ommitted


### Environment-Style Macros
Macros for creating a LaTeX environment of some sort.
#### Figure - #fimg
Replaces the #fimg with a figure blank. Markers are set for width and filepath. By default, the image path is assumed as "img/...".  

    \begin{figure}[H]
      \centering
      \includegraphics[width=%<Breite%>\textwidth]{img/%<Speicherort%>}
    \end{figure}


#### Math Text (Alt + Shift + I)  
Inserts math text mode  

    \text{%<Text%>}


#### Itemize - #itm#  
Inserts itemize with "-" as label.  

    \begin{itemize}[label=-]
      %<Content..%>
    \end{itemize}


#### Table - #tab
Inserts a tabulary table environment with jump markers.

    \begin{tabulary}{%<Width%>}{%<Column Config%>}
      %<Content%>
    \end{tabulary}


### Insert-Style Macros
Macros that insert a piece of latex code as a shorthand.

#### Initialization - #init
Some frequently used packages for quickly initializing documents.  

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


#### Textwidth variable Shorthand #tw
Shorthand for the LaTeX variable for textwidth.  

    \textwidth


#### Degree Symbol - °
Inserts degree symbol. For use in math mode.

    ^{\circ}


#### pdf_tex Input - #pdftex
Inserts the standard code for inserting pdf_tex files (usually inside figures for vector graphics illustrations). The image path is assumed as img/....

    \centering
    \def\svgwidth{%<size%>\textwidth}
    \input{img/%<filename%>.pdf_tex}


### Script-Style Macros
Script Macros.
#### Derivative - #d/d(.+)#
Inserts a derivative depending on the trigger.
```JavaScript
editor.write("\\text{\\frac{d}{d" + triggerMatches[1] + "}}")
```

#### scriptfig - fig\.(\S+) (\S+) (.+)#(.\*)\.  
Inserts a figure with width, image name and caption (and label if specified).  
For example: ```fig.somewidth imgname This is a caption.#thisisalabel.``` will be replaced by:
    
    \begin{figure}[h]
      \centering
      \includegraphics[width=somewidth]{imgname}
      \caption{This is a caption.}
      \label{img:thisisalabel}
    \end{figure}
If the label is omitted (input: ```fig.somewidth imgname This is a caption.#.```), the line containing the label will not be present in the output. Note that the first two parameters are separated by a space. Adding spaces in those parameters can lead to unexpected behaviour.

```JavaScript
var str_write;
if (triggerMatches[4] != "") {
  str_write = "\\begin{figure}[h]\n\
  \t\\centering\n\
  \t\\includegraphics[width=" + triggerMatches[1] + "]{" + triggerMatches[2] + "}\n\
  \t\\caption{" + triggerMatches[3] + "}\n\
  \t\\label{img:" + triggerMatches[4] + "}\n\
  \\end{figure}\n";
} else {
  str_write = "\\begin{figure}[h]\n\
  \t\\centering\n\
  \t\\includegraphics[width=" + triggerMatches[1] + "]{" + triggerMatches[2] + "}\n\
  \t\\caption{" + triggerMatches[3] + "}\n\
  \\end{figure}\n";
}
editor.write(str_write);
```

#### scripteqn - eq\.(.+)\.
Inserts an equation environment with contents.
```JavaScript
editor.write("\\begin{equation} \n\
\t\t" + triggerMatches[1].replace(/[$]/g, "") + "\n\
\\end{equation}")
```

#### scriptfrac - (.\*)//(.+)//(.+)//(.\*)
Inserts a fraction. For use in math mode.
```JavaScript
editor.write(
triggerMatches[1] + 
"\\frac{" + triggerMatches[2] + "}{" + triggerMatches[3] + "}" + 
triggerMatches[4]);
```

#### supersub - (.\*)##(.+)##(.\*)
For use in math mode. Inserts a superscript, superscript or ```\mathrm{}``` formatting at the current position. Everything between the "##" and after the first occurance of "\_" or "^" will be formatted as  ```\mathrm{}``` and super-/ or subscripted. No use of "\_" or "^" will just ```\mathrm{}``` the entire thing.  
For Example: ```##A_sub^super##``` will be replaced by ```A_\mathrm{sub}^\mathrm{super}``` and ```##roman##``` wil be replaced by ```\mathrm{roman}```. **The Sequence of ^ and _ will be considered when creating the LaTeX code to insert!** 

```JavaScript
editor.write(triggerMatches[1]);

var mid = triggerMatches[2].split(/\^|_/g);
var hat_pos = triggerMatches[2].indexOf("^");
var und_pos = triggerMatches[2].indexOf("_");

if ((hat_pos == -1) && (und_pos != -1)) {
  editor.write(mid[0] + "_\\mathrm{" + mid[1] + "}");
} else if ((und_pos == -1) && (hat_pos != -1)) {
  editor.write(mid[0] + "^\\mathrm{" + mid[1] + "}");
} else if ((und_pos != -1) && (hat_pos != -1)) { 
  if (hat_pos < und_pos) {
    editor.write(mid[0] + "^\\mathrm{" + mid[1] + "}_\\mathrm{" + mid[2] + "}");
  } else {
    editor.write(mid[0] + "_\\mathrm{" + mid[1] + "}^\\mathrm{" + mid[2] + "}");
  }
} else {
  editor.write("\\mathrm{" + triggerMatches[2] + "}");
}
editor.write(triggerMatches[3]);
```

#### ArrowsRight - ([-]{1,2}|[=]{1,2})>
Inserts right facing arrows depending on input. Outputs ```\rightarrow```, ```\Rightarrow```, ```\longrightarrow``` or ```\Longrightarrow``` for inputs of "->", "=>", "-->" and "==>" respectively. For use in math mode.
```JavaScript
switch(triggerMatches[1]) {
  case "-":
    editor.write("\\rightarrow");
    break;
  case "=":
    editor.write("\\Rightarrow");
    break;
  case "--":
    editor.write("\\longrightarrow");
    break;
  case "==":
    editor.write("\\Longrightarrow");
    break;
  default:
    editor.write(triggerMatches[1] + ">");
    break;
}
```

#### ArrowsLeft - <([-]{1,2}|[=]{1,2})
Same as ArrowsRight but arrows facing the other way.
```JavaScript
switch(triggerMatches[1]) {
  case "-":
    editor.write("\\leftarrow");
    break;
  case "=":
    editor.write("\\Leftarrow");
    break;
  case "--":
    editor.write("\\longleftarrow");
    break;
  case "==":
    editor.write("\\Longleftarrow");
    break;
  default:
    editor.write("<" + triggerMatches[1]);
    break;
}
```


