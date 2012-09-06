Hi, this is Yihui Xie, and I'm guest posting on the Revolutions blog to talk about one aspect of the **knitr** package: how we can integrate data analysis and reporting in R with the Web. This post includes both the work that has been done and the ongoing work. For those who have no idea of knitr, it is an R package to generate reports dynamically from the mixture of computer code and narratives. It is available on [CRAN](http://cran.r-project.org/package=knitr) and [Github](https://github.com/yihui/knitr).

Why do I put such special emphasis on the web? Let me quote what I heard from [Carlos Scheidegger](http://cscheid.net/) in this summer when I was doing intern at AT&T Labs: one thing does not exist unless it is on the web (one corollary to his "theorem", to my understanding, was "if you do not have a homepage yet, you simply do not exist"). Well, I web, therefore I am.

I wrote a blog post on [enjoyable reproducible research](http://yihui.name/en/2012/06/enjoyable-reproducible-research/) back in June; for those who come from the LaTeX world, let me repeat the idea: reproducible research does not have to begin with `\documentclass{}`, and there can be more fun with the web. LaTeX is mainly for printing purposes in my eyes, so if you are not going to print the stuff that you are reading (like what you are doing now), you may start playing with R in the web now.

## Learn knitr in 5 minutes

Here is [a video](http://www.screenr.com/qcv8) that demonstrates how to use knitr to create HTML pages from Markdown and PDF from Rnw documents respectively:

<iframe src="http://www.screenr.com/embed/qcv8" width="650" height="396" frameborder="0"></iframe>

The examples that I used were from https://github.com/yihui/knitr-examples. The reference card mentioned in the video can be downloaded [here](https://github.com/downloads/yihui/knitr/knitr-refcard.pdf). Next I'm going to introduce a few interesting projects based on knitr.

## RPubs

[RPubs](http://www.rpubs.com/) publishes HTML reports compiled by knitr from R Markdown documents. This website is hosted by RStudio, and it really shows the creativity of users when you give them a simple tool. It has been [mentioned once](http://blog.revolutionanalytics.com/2012/08/creating-beautiful-reports-from-r-with-knitr.html) in this blog, and let me show you a few more significant uses (list not exhaustive, of course):

- [r-de-r](http://www.rpubs.com/r-de-r), especially the graphics examples (that is how R documentation should really look like!!)
- Prof [Daniel Kaplan](http://www.rpubs.com/dtkaplan) even puts his [course schedule](http://www.rpubs.com/dtkaplan/1150) there, and he shows how you can mix all sorts of media sources together so the course notes are no longer boring (e.g. [Introducing Functions of Multiple Variables](http://www.rpubs.com/dtkaplan/785))
- [kaz_yos](http://www.rpubs.com/kaz_yos); oh man, he (or she) has so much [homework](http://www.rpubs.com/kaz_yos/1519) to do (who is the instructor?), and still has time to play with [GapMinder](http://www.rpubs.com/kaz_yos/1268)!
- Prof [Chris Brunsdon](http://rpubs.com/chrisbrunsdon) has some solid reports on Twitter, Olympic breakfast and spatial statistics
- Prof [John Verzani](http://rpubs.com/jverzani) shows how you can make an [interactive quiz](http://rpubs.com/jverzani/1143) to learn R
- [kohske](http://www.rpubs.com/kohske) has an example of [HTML5 slides](http://www.rpubs.com/kohske/319) via [ramnathv](http://www.rpubs.com/ramnathv/)'s package

Within three months, RPubs has got more than 600 contributed reports, demonstrating many exciting applications of R in the web.

## OpenCPU and CRUNCH

The web feature of knitr makes it easy to generate reports in the cloud, so that the client only needs a web browser. I introduce two platforms here, both of which support knitr:

1. [OpenCPU](http://opencpu.org) by Jeroen Ooms: see a [knitr app](http://public.opencpu.org/apps/knitr/); OpenCPU features the REST API, so you can deploy your apps anywhere;
2. [CRUNCH](http://crunch.kmi.open.ac.uk/) by the Knowledge Media Institute of the Open University: see examples by [me](http://crunch.kmi.open.ac.uk/people/~yihui/services/knitr-minimal.R) and [Fridolin](http://crunch.kmi.open.ac.uk/people/~fwild/services/report.rmw); CRUNCH features an RStudio workspace and services to run computationally-intense learning analytics;

The R package [markdown](http://cran.r-project.org/package=markdown) is used to convert the markdown output from knitr to HTML, thanks to the contribution of Jeffrey Horner.

## R notebook

As I mentioned in the beginning, I was working at AT&T Labs in the summer, and one thing that we were trying to do was to build an R notebook, which is similar to the Python notebook. The source code is available on [Github](https://github.com/cscheid/rcloud) now, but it might take you a while to figure out how to run it. Anyway, the idea is still to develop an environment on the web for people to write reports and collaborate with each other.

## R package documentation and vignettes

R documentation could have been much more attractive. Look at the websites of other languages like Python, Ruby, ... What you can say is, sigh. R is so strong at graphics, whereas standard R documentation is almost always plain text, even when you look at `?plot`.

[UCLA R tutorials](http://www.ats.ucla.edu/stat/r/) have included [examples of Singular Value Decomposition](http://www.ats.ucla.edu/stat/r/pages/svd_demos.htm) (built with knitr), and I think `?svd` will be more enjoyable to read if the documentation looks like that. Many R users know Hadley's ggplot2 documentation [website](http://had.co.nz/ggplot2), and the best thing in my eyes about this website is I can learn by reading both the source code and output without having to copy the code, open R, paste the code, and check the results.

In this summer, knitr was accepted to the Google Summer of Code (GSoC) and I had a student (Taiyun Wei) who worked on a few interesting directions. Two of them were related to R documentation:

1. Convert standard R package documentation to HTML pages, run the code in Examples sections and embed results there; for example, you can call `library(knitr); knit_rd('maps')` to generate HTML help pages for all objects in the **maps** package, and you will see maps in the help pages;
2. Write package vignettes with R Markdown instead of LaTeX/Sweave; check out Taiyun's [corrplot](https://github.com/taiyun/corrplot) package on Github, run `R CMD build`/`R CMD INSTALL` on it, and you will see a nice HTML vignette in `help.start()`; the key is in the `Makefile` and `index.Rmd` (more technical details later in my own blog);

Hopefully this can encourage R package authors to write more attractive documentation, since there is no excuse not to write more examples, or avoid package vignettes.

## Vistat

[Vistat](http://vis.supstat.com/) is also a project that we started in GSoC. The motivation was simple: we should be able to reproduce graphs in which we are interested. We reproduce them for the sake of either verification of reproducibility or merely learning purposes. All the examples in this website are generated from knitr (including the animations), and you can always read the R Markdown source if the R code in the pages is not enough for you to figure out how to make the plots.

Another purpose is to see if we can build [a really fast journal](http://yihui.name/en/2012/03/a-really-fast-statistics-journal/) via GIT since it is hosted on Github with Jekyll. Vistat is still in its early stage, and I will see how it moves forward by the help of the community.

## Conclusion

With the simple idea of mixing code into narratives, we can do a lot of interesting things. Go claim your existence by publishing a few web pages!

Bio: [Yihui Xie](http://yihui.name) is a fourth year PhD student in the Department of Statistics, Iowa State University. He has been using R for 8 years and developed a number of R packages including [knitr](http://yihui.name/knitr/), [animation](http://yihui.name/animation/), [formatR](http://yihui.name/formatR/), [Rd2roxygen](http://yihui.name/Rd2roxygen/) and [fun](http://cran.r-project.org/package=fun), etc.
