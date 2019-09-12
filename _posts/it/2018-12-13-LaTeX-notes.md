---
layout: post
title: LaTeX notes
categories: [it]
tags: [LaTeX]
toc: 1
date: 2018-12-13
---

## Fundamentals
- `\include{}` equiv.to `\clearpage \input{} \clearpage`.
- list of contents (`\tableofcontents`), figures (`listoffigures`),
tables (`listoftables`).
- use the `siunitx` macro package for SI unit:
    {% highlight latex %}
    \SI{1}{cm} % 1 cm
    \ang{1;2;3} % product 1 degree 2 minuters 3 seconds
    {% endhighlight %}
- curly braces ({}) has two meaning:
  1. is a grouping (or scope). For example, `\textbf{Some bold text}`
  2. after a LaTeX command, stands for mandatory arguments (or parameters)
  {% include tip.html content="LaTeX takes the first non-space object
  following the command name as the argument, in this way, there are only
  a meaning for grouping" %}
- optional arguments must always be enclosed in square bracets [ ]
- **moving arguments** is the data that LaTeX saves and will reread later.
Places to look for are all arguments that may go into table of contents, list
of figures etc.
- **fragile command** is a command that expands into *illegal* TeX code during
the save process, can seriously mess things up when they are used in what is
termed a *moving argument*.
- **robust command** is a command that expands into *legal* TeX code during the
save process
- [More information about arguments and command above](https://www.tug.org/tetex/html/texfaq/faq_15.html)

## Bibliography
- Always use the sequence:
  1. `LaTeX`: produces the necessary intermediate file
  2. `makeindex`: sort the index
  3. `bibtex`: create the bibliography
  4. `LaTeX`: include bibliography and index, resolve cross-references
  5. `LaTeX`: resolve remaining cross-references
{% include tip.html content="`bibtex *.aux` not `bibtex *.bib`. The
auxiliary file contains all the information needed for cross-referencing" %}


## Beamer
- Beamer themes in [Beamer Theme Matrix](https://hartwork.org/beamer-theme-matrix/)
   ```latex
    \usetheme{Berkeley}
    \usecolortheme{beaver}
   ```

## Tikz
- `+` and `++` operation
  ```latex
      \draw (x1, y1) -- +(x2, y2) -- +(x3, y3); % from (x1, y1) to (x1+x2, y1+y2) to (x1+x3, y1+y3)
      \draw (x1, y1) -- +(x2, y2) -- ++(x3, y3); % from (x1, y1) to (x1+x2, y1+y2) to (x1+x2+x3, y1+y2+y3)
  ```
- Standalone TeX file is able to compile the pictures on thier own and can be included in other files through `\input` or `\include`.
  ```latex
  \documentclass[tikz]{standalone}
  \usepackage{tikz}
  \begin{document}

  \begin{tikzpicture}
    % code in here
  \end{tikzpicture}

  \end{document}
  ```
