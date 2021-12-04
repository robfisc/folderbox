# folderbox
A [LaTeX](https://www.latex-project.org) package for creating labels for paper file folders and archive file boxes.

The folderbox package provides three benefits:
1. Printable labels for standard paper folders (8 cm width) with crop marks for precise cutting
2. Outside label for standard archive box holding five folders
3. A document serving as index or catalogue of the contents of one or multiple archive boxes

The following illustration shows the result: an archive box containing folders, where each folder has a label and all labels are visible on the outside of the box.

![Archive box containing five file folders with labels and an overview of all labels on the outside of the box](./doc/folderbox_with_labels.svg)


[//]: # (TOC - START)

## Table of Contents
1. [Introduction](#introduction)
2. [Example](#example)
3. [Installation](#installation)

[//]: # (TOC - END)


## Introduction

folderbox achieves its goals by creating one landscape A4 page for five folders (see [Example](#example) below). The number five corresponds both to the capacity of standard archive box (approx. inside dimensions 41 x 32 x 28 cm), and provides enough width to fit five labels of approx. 5 cm next to each other.
The resulting document containing one or multiple pages with labels for boxes simultaneously serves as catalogue that indexes the contents of those boxes.

Personal remark:
Works well with folder or ring binders with

## Example

![Example label for one box](./example/example_with_cropmarks.svg)

This example is available [with](example/example_with_cropmarks.pdf) and [without](example/example_without_cropmarks.pdf) crop marks as PDF file. The [source tex file](example/example.tex) can be compiled using `latexmk` called from the example folder.


```tex
\documentclass[landscape]{scrartcl}
\usepackage[
    top=0.5cm,
    bottom=0.5cm,
    left=1.3cm,
    right=1cm
    ]{geometry}

%\usepackage{folderbox}
\usepackage[cropmarks]{folderbox}

\begin{document}

% one environment per page, one page per 5 folder / one box
\begin{folderbox}{Folder Box 1}

% one call to \folder per folder
% first argument corresponds to header, second to content
\folder{Bank}{
    % content of the label goes here
}

\folder{Invoice}{
}


\folder{Taxes}{
    2021

    2020

    2019

    2018
}

\folder{School}{}
\folder{Archive}{}

\end{folderbox}

\end{document}

```



## Installation

See [answer on stackexchange](https://tex.stackexchange.com/a/73017) for overview on possibilities to use user-installed LaTeX packages.

### Option using `TEXINPUTS` variable in `latexmkrc`

See [example latexmkrc file](example/latexmkrc) for concrete usage. Gist of it:

```latexmkrc
ensure_path('TEXINPUTS', '<path to folder with .sty file>');
```

### Manual installation
1. Get base directory `<base dir>`
    - System wide: `kpsewhich -var-value TEXMFLOCAL`
    - Current user only: `kpsewhich -var-value TEXMFHOME`

2. If necessary, create package directory

    ```bash
    mkdir -p <base dir>/tex/latex/<package name>
    ```

3. Copy `.sty` file into package directory

4. For system-wide packages, update tex index
    ```bash
    which mktexlsr
    sudo /path/to/mktexlsr
    ```

### Local installation
To be done




## Further Plans

- Document .sty file (create .dtx file?)
- Write local install script
- Decide on configurable parameters (which per document and which per page?)
- Create PDF package documentation
- Eventually, create CTAN package
