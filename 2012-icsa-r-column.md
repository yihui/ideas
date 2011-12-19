# Turn Research into Fun, and Vice Versa

Yihui Xie
(Address: 102 Snedecor Hall, Ames, IA 50011; Email: xie@yihui.name Homepage: http://yihui.name)

I really appreciate the opportunity offered by our editor Jun Yan asking me to write a short article on the R language. I thought for a while, and decided not to write it in a technical manner. I want to summarize what I have done in my 7 years of using R, and I hope my experience can be helpful to the student readers of this bulletin.

Currently I'm a third year PhD student in the Department of Statistics, Iowa State University. My research interest is data visualization and dynamic/interactive statistical graphics, and I use R extensively in my daily work. The progression of this article will follow a series of R packages that I developed in the past few years.

## The animation Package

The **animation** package (http://cran.r-project.org/package=animation) was my first R package, and I started it in 2007 while I was in the Renmin University of China, two years before I came to the US. The idea of this package was fairly simple -- I realized some topics in statistics could be visualized via animations, and how can we make animations in R? My answer was just to draw plots one by one, with a short pause between them (see the function _Sys.sleep()_). It is apparently a naive and inefficient approach, but that's it. I did the Brownian motion first (with points moving on the plot randomly), and it was fun. Then I moved to other topics which had more statistical flavor, for example, the Central Limit Theorem, the Newton-Raphson method, Galton's Box and k-Means clustering, etc. I showed statistical methods and algorithms step by step to help other people understand them. Although my implementation sounds clumsy from the perspective of computer science, these animations opened many doors to me later. Having worked as a web administrator for 3 years, I made a website based on them so people can view these animations online without really calling my functions in R.

About 3 months later, someone noticed my package and website (a few months later I realized it was Hadley Wickham, who is now a famous author of many R packages including ggplot2), and he pointed my website to his advisor. Guess who was this advisor? She is my current advisor, Dr Di Cook. She emailed me in January 2008, and the connection was established by that time. In June 2008 I got a chance to attend a workshop on data visualization in Germany, and it was my first time of going out of China. The reason that I was accepted to the workshop was because of the animation package. At the workshop I talked to Di and other great people in the area of data visualization. Long story short, I came to Iowa State in Fall 2009. By the way, in August 2008 I went to Germany again to attend the useR! conference to talk about this package.

So a naive idea can help, as long as you feel there is fun, and pursue the fun till it has more scientific flavor (i.e. you can publish something out of it). The question is, how to turn fun into research? For the animation package, the accumulation of examples and demos as time goes by made me think how these animations could be related to different aspects of statistics. For instance, some are about random numbers and simulations, and some are about sampling and resampling, etc. The classification of these animations gives me a clearer view of what role animations can play in statistics to help people understand our methods and theories. A short article on this package was published in R News in 2008, and I also have another longer paper submitted to the Journal of Statistical Software early this year.

Another door that opened to me was the John Chambers Award (Statistical Computing Section, ASA), which I think is probably worth (shamelessly) mentioning here. I won this award in 2009 due to the animation package, and it enabled me to go to JSM in DC. In the summer of 2009, I flew from Beijing to DC, then went to Iowa State as a new graduate student. This sounds too good to be true, but yes, everything started from that stupid animation of the Brownian motion, with points moving stupidly in an R plot window.

When I was walking through some posters at JSM (2011 Miami), I saw a few of them used the animation package to illustrate data in dynamic processes, and of course I felt very happy about this.

## The fun Package

People may feel that I'm not a serious statistician because I always look for funny things to work on. The animation package was fun, but actually I wrote a package which was really named **fun** with two other authors (http://cran.r-project.org/package=fun). You can play some classical games in R with this package, such as the mine sweeper. It may sound surprising to many R users, but the implementation is not that hard (go check the source code).

What is the point of this almost obviously meaningless package? Well, I always believe fun can be interwined with research. Take the function _alzheimer\_test()_ for example: it sounds like a joke, because statisticians should do t-test instead of something called Alzheimer test. This function prints a character block on the screen which consist of one character but there is another character hidden in the block, e.g.

```
999999999999999999999999999999
999999999999999999999999999999
999999999999999999999999999999
999999999999999999999999999999
999999999999999999999999999999
999999999999999999999999999999
999999999999999999999999999999
999999999999999699999999999999
999999999999999999999999999999
999999999999999999999999999999
```

The goal of this game is to find out where is the different character (to show you are not too old and slow). There is actually a deeper thought behind it: when making scatter plots, some people do not pay enough attention to the choice of point symbols to denote different groups, which makes the plot really dificult to read, because different groups of points cannot stand out clearly. Imagine a scatter plot in which there are two groups and you use the symbols `6` and `9`. The principle is you should choose symbols carefully to make them as distinct as possible (e.g. `+` and `o` can be a good choice). This is another example of possibly turning fun into research.

## The formatR package

I hate R code without spaces and proper indentation, but I'm lazy on the other hand, therefore I wrote the **formatR** package (http://cran.r-project.org/package=formatR), which can reformat R code automatically, no matter how ugly it looks originally. It is not much fun by itself, but I found an interesting place to use it soon -- Sweave. For those who are not familar with Sweave, the idea is to mix program code and text together in an input document, and Sweave can execute the code and put the corresponding results into the output document (this idea came a long way from literate programming).

One thing that I really dislike about many books on R is the poor quality of R code (I mean the poor format). I understand the authors may not want to type spaces and indentation, and are lazy like me. The formatR package can play a helpful role in Sweave to reformat the source code so that even if you are lazy, your code in the output can still look nice. I did not get a chance to make it into the official Sweave (it is not likely for base R to use an add-on package), but I found the pgfSweave package, which is an add-on package based on Sweave, and formatR was successfully applied in it. This is not the end of the story, because I found the design of Sweave tied my hands, and I re-invented the wheel.

## The knitr Package

As mentioned before, Sweave can be used to write statistical reports dynamically; you no longer need to copy and paste results -- all you maintain is the source code, and you just run the code to get a report. Sweave has many limitations, for example, normally you can only get one plot per chunk of code (yes you can hack at it to get more than one). As a student working on graphics, this is a serious limitation, since it is often the case that I have multiple plots per code chunk. The **knitr** package (http://yihui.github.com/knitr/) was motivated from my daily use of Sweave, but it gives users much more flexiblility to control the output. The formatR package serves as a tool to reformat R code in this package, which makes it fun for me to write statistical reports.

A closely related topic is the reproducible research (RR), and Roger Peng has been talking about it frequently. As he said, this is a hard topic. Ideally all scientific research should be reproducible, and Sweave has made a significant progress to RR because people do not need to copy and paste when doing data analysis (`Ctrl+C` and `Ctrl+V` are barely reproducible!). RR is hard both technically and practically. Currently I do not have a voice loud enough to persuade people thinking about RR, but I can do something for the technical part of the difficulty. The **knitr** package has a completely different design with Sweave, and I think very hard on RR when I was writing this package. For example, Sweave uses environment variables, and I believe this is a disaster to RR, because environment variables can be specific to an operating system; a report may not be reproducible in a different computer because of different environment variables.

What I discussed here is only a tiny detail in this package. My point is we should not underestimate the importance of software packages, and neither should we use R functions blindly. As a statistician, have you ever thought of a possible fact that your results are confounded by environment variables?

## Conclusions

In this article, I introduced four of my R packages, in all of which I believe there is lots of fun. I have another package named **cranvas** under development, and it will probably become the main topic of my PhD thesis (dynamic and interactive graphics). I have enjoyed the development so far, and it is interesting to see how people worked in this area in the 70's and 80's. Perhaps it is because I'm not good at math; I like things that are visually appealing, no matter it is an interesting plot (animation), or a clean chunk of code (formatR), or a beautifully formatted statistical report (knitr). To me, it does not matter which area you work in -- the really important thing is to be able to find fun out of research (otherwise you get bored and lose motivation), and turn fun into research as well (you have to survive after all).
