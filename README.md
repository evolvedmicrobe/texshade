Nigel's Port of the TexShade Package.  

[Texshade](https://www.ctan.org/pkg/texshade?lang=en) is the display backend for the bioconductor [MSA package](http://bioconductor.org/packages/devel/bioc/html/msa.html) (and on [github](https://github.com/Bioconductor-mirror/msa/tree/release-3.1)):



Texshape has great coloring for amino acids, but is more limited in displaying DNA alignments.  I added one of the  [color brewer](http://colorbrewer2.org/) color packages to enable better DNA display.

I am tricking the program to generate shading by nucleotide by making this a type of functional annotation.  You need to copy the file to a global install as well e.g. sudo cp texshade.sty /usr/local/texlive/2014/texmf-dist/tex/latex/texshade/

Example code to generate MSA plot from R below

    source("http://www.bioconductor.org/biocLite.R")
    biocLite("msa")
    library(msa)
    # if a new computer, just edit this file:
    system.file("tex", "texshade.sty", package="msa")
    dm = readDNAMultipleAlignment("/Users/nigel/pacbio/9320All.fna")
    msaPrettyPrint(dm,  shadingMode="functional", showNumbering="none", showLegend=FALSE, askForOverwrite=FALSE, shadingModeArg = "accessible area", shadingColors="blues", consensusColors="BlueRed", showLogo="none", file="All.pdf",y=c(500, 737))
    msaPrettyPrint(dm,  shadingMode="functional", showNumbering="none", showLegend=FALSE, askForOverwrite=FALSE, shadingModeArg = "accessible area", shadingColors="blues", consensusColors="BlueRed", showLogo="none", file="GoodSnp.pdf",y=c(586, 592), psFonts=TRUE)
    msaPrettyPrint(dm,  shadingMode="functional", showNumbering="none", showLegend=FALSE, askForOverwrite=FALSE, shadingModeArg = "accessible area", shadingColors="blues", consensusColors="BlueRed", showLogo="none", file="BadIndel.pdf",y=c(705, 712), psFonts=TRUE)


And as a pure latex document:


      \documentclass[10pt]{article}      

      \usepackage{texshade}      

      \headheight=0pt
      \headsep=0pt
      \hoffset=0pt
      \voffset=0pt
      \paperwidth=11in
      \paperheight=8.5in
      \ifx\pdfoutput\undefined
      \relax
      \else
      \pdfpagewidth=\paperwidth
      \pdfpageheight=\paperheight
      \fi
      \oddsidemargin=-0.9in
      \topmargin=-0.7in
      \textwidth=10.8in
      \textheight=7.9in      

      \pagestyle{empty}      

      \begin{document}
      \begin{texshade}{/Users/nigel/pacbio/Seq.fasta}
      \seqtype{P}
      \setends{consensus}{500..737}
      \shadingmode[DNA]{functional}
      \showconsensus[BlueRed]{bottom}
      \hidelogoscale
      \shownames{left}
      \nameseq{1}{1}
      \nameseq{2}{2}
      \nameseq{3}{3}
      \nameseq{4}{4}
      \nameseq{5}{5}
      \nameseq{6}{6}
      \nameseq{7}{7}
      \nameseq{8}{8}
      \nameseq{9}{9}
      \nameseq{10}{10}
      \hidenumbering
      \end{texshade}
      \end{document}
