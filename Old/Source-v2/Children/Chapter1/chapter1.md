Introducing Reproducible Research {#Intro}
=================================

Research is often presented in very selective containers: slideshows,
journal articles, books, or maybe even websites. These presentation
documents announce a project's findings and try to convince us that the
results are correct [@Mesirov2010]. It's important to remember that
these documents are not the research. Especially in the computational
and statistical sciences, these documents are the "advertising". The
research is the "full software environment, code, and data that produced
the results" [@Buckheit1995; @Donoho2010 385]. When we separate the
research from its advertisement we are making it difficult for others to
verify the findings by reproducing them.

This book gives you the tools to dynamically combine your research with
the presentation of your findings. The first tool is a workflow for
reproducible research that weaves the principles of reproducibility
throughout your entire research project, from data gathering to the
statistical analysis, and the presentation of results. You will also
learn how to use a number of computer tools that make this workflow
possible. These tools include:

-   the **R** statistical language that will allow you to gather data
    and analyze it;

-   the **LaTeX** and **Markdown** markup languages that you can use to
    create documents--slideshows, articles, books, and webpages--for
    presenting your findings;

-   the *knitr* and *rmarkdown* **packages** for R and other tools,
    including **command-line shell programs** like GNU Make and Git
    version control, for dynamically tying your data gathering,
    analysis, and presentation documents together so that they can be
    easily reproduced;

-   **RStudio**, a program that brings all of these tools together in
    one place.

What Is Reproducible Research?
------------------------------

Though there is some debate over what are the necessary and sufficient
conditions for a replication [@Makel2014 2], research results are
generally considered *replicable* if there is sufficient information
available for independent researchers to make the same findings using
the same procedures with new data.[^1] For research that relies on
experiments, this can mean a researcher not involved in the original
research being able to rerun the experiment, including sampling, and
validate that the new results are comparable to the original ones. In
computational and quantitative empirical sciences, results are
replicable if independent researchers can recreate findings by following
the procedures originally used to gather the data and run the computer
code. Of course, it is sometimes difficult to replicate the original
data set because of issues such as limited resources to gather new data
or because the original study already sampled the full universe of
cases. So as a next-best standard we can aim for "*really reproducible
research*" [@Peng2011 1226].[^2] In computational sciences[^3] this
means:

> the data and code used to make a finding are available and they are
> sufficient for an independent researcher to recreate the finding.

In practice, research needs to be *easy* for independent researchers to
reproduce [@Ball2012]. If a study is difficult to reproduce it's more
likely that no one will reproduce it. If someone does attempt to
reproduce this research, it will be difficult for them to tell if any
errors they find were in the original research or problems they
introduced during the reproduction. In this book you will learn how to
avoid these problems.

In particular you will learn tools for dynamically "*knitting*"[^4] the
data and the source code together with your presentation documents.
Combined with well-organized source files and clearly and completely
commented code, independent researchers will be able to understand how
you obtained your results. This will make your computational research
easily reproducible.

Why Should Research Be Reproducible?
------------------------------------

Reproducible research is one of the main components of science. If
that's not enough reason for you to make your research reproducible,
consider that the tools of reproducible research also have direct
benefits for you as a researcher.

### For science

Replicability has been a key part of scientific inquiry from perhaps the
1200s [@Bacon1267; @Nosek2012]. It has even been called the "demarcation
between science and non-science" [@Braude1979 2]. Why is replication so
important for scientific inquiry?

##### Standard to judge scientific claims

*Replication* opens claims to scrutiny, allowing us to keep what works
and discard what doesn't. Science, according to the American Physical
Society, "is the systematic enterprise of gathering knowledge
...organizing and condensing that knowledge into testable laws and
theories". The "ultimate standard" for evaluating scientific claims is
whether or not the claims can be replicated [@Peng2011; @Kelly2006].
Research findings cannot even really be considered "genuine
contribution\[s\] to human knowledge" until they have been verified
through replication [@Stodden2009 38]. Replication "requires the
complete and open exchange of data, procedures, and materials".
Scientific conclusions that are not replicable should be abandoned or
modified "when confronted with more complete or reliable
...evidence".[^5]

*Reproducibility enhances replicability*. If other researchers are able
to clearly understand how a finding was originally made, then they will
be better able to conduct comparable research in meaningful attempts to
replicate the original findings. Sometimes strict replicability is not
feasible, for example, when it is only possible to gather one data set
on a population of interest. In these cases reproducibility is a
"minimum standard" for judging scientific claims [@Peng2011].

It is important to note that though reproducibility is a minimum
standard for judging scientific claims, "a study can be reproducible and
still be wrong" [@Peng2014]. For example, a statistically significant
finding in one study may remain statistically significant when
reproduced using the original data/code, but when researchers try to
replicate it using new data and even methods, they are unable to find a
similar result. The original finding could simply have been noise, even
though it is fully reproducible.

##### Avoiding effort duplication & encouraging cumulative knowledge development

Not only is reproducibility important for evaluating scientific claims,
it can also contribute to the cumulative growth of scientific knowledge
[@Kelly2006; @King1995]. Reproducible research cuts down on the amount
of time scientists have to spend gathering data or developing procedures
that have already been collected or figured out. Because researchers do
not have to discover on their own things that have already been done,
they can more quickly build on established findings and develop new
knowledge.

### For you

Working to make your research reproducible does require extra upfront
effort. For example, you need to put effort into learning the tools of
reproducible research by doing things such as reading this book. But
beyond the clear benefits for science, why should you make this effort?
Using reproducible research tools can make your research process more
effective and (hopefully) ultimately easier.

##### Better work habits

Making a project reproducible from the start encourages you to use
better work habits. It can spur you to more effectively plan and
organize your research. It should push you to bring your data and source
code up to a higher level of quality than you might if you "thought 'no
one was looking'" [@Donoho2010 386]. This forces you to root out
errors--a ubiquitous part of computational research--earlier in the
research process [@Donoho2010 385]. Clear documentation also makes it
easier to find errors.[^6]

Reproducible research needs to be stored so that other researchers can
actually access the data and source code. By taking steps to make your
research accessible for others you are also making it easier for
yourself to find your data and methods when you revise your work or
begin new a project. You are avoiding personal effort duplication,
allowing you to cumulatively build on your own work more effectively.

##### Better teamwork

The steps you take to make sure an independent researcher can figure out
what you have done also make it easier for your collaborators to
understand your work and build on it. This applies not only to current
collaborators, but also future collaborators. Bringing new members of a
research team up to speed on a cumulatively growing research project is
faster if they can easily understand what has been done already
[@Donoho2010 386].

##### Changes are easier

A third person may or may not actually reproduce your research even if
you make it easy for them to do so. But, *you will almost certainly
reproduce parts or even all of your own research*. No actual research
process is completely linear. You almost never gather data, run
analyses, and present your results without going backwards to add
variables, make changes to your statistical models, create new graphs,
alter results tables in light of new findings, and so on. You will
probably try to make these changes long after you last worked on the
project and long since you remembered the details of how you did it.
Whether your changes are because of journal reviewers' and conference
participants' comments or you discover that new and better data has been
made available since beginning the project, designing your research to
be reproducible from the start makes it much easier to change things
later on.

Dynamic reproducible documents in particular can make changing things
much easier. Changes made to one part of a research project have a way
of cascading through the other parts. For example, adding a new variable
to a largely completed analysis requires gathering new data and merging
it with existing data sets. If you used data imputation or matching
methods you may need to rerun these models. You then have to update your
main statistical analyses, and recreate the tables and graphs you used
to present the results. Adding a new variable essentially forces you to
reproduce large portions of your research. If when you started the
project you used tools that make it easier for others to reproduce your
research, you also made it easier to reproduce the work yourself. You
will have taken steps to have a "better relationship with \[your\]
future \[self\]" [@Bowers2011 2].

##### Higher research impact

Reproducible research is more likely to be useful for other researchers
than non-reproducible research. Useful research is cited more frequently
[@Donoho2002; @Piwowar2007; @Vandewalle2012]. Research that is fully
reproducible contains more information, i.e. more reasons to use and
cite it, than presentation documents merely showing findings.
Independent researchers may use the reproducible data or code to look at
other, often unanticipated, questions. When they use your work for a new
purpose they will (should) cite your work. Because of this, Vandewalle
et al. even argue that "the goal of reproducible research is to have
more impact with our research" [-@Vandewalle2007 1253].

A reason researchers often avoid making their research fully
reproducible is that they are afraid other people will use their data
and code to compete with them. I'll let Donoho et al. address this one:

> *True. But competition means that strangers will read your papers, try
> to learn from them, cite them, and try to do even better. If you
> prefer obscurity, why are you publishing?* [-@Donoho2009 16]

Who Should Read This Book?
--------------------------

This book is intended primarily for researchers who want to use a
systematic workflow that encourages reproducibility as well as practical
state-of-the-art computational tools to put this workflow into practice.
These people include professional researchers, upper-level
undergraduate, and graduate students working on computational
data-driven projects. Hopefully, editors at academic publishers will
also find the book useful for improving their ability to evaluate and
edit reproducible research.

The more researchers that use the tools of reproducibility the better.
So I include enough information in the book for people who have very
limited experience with these tools, including limited experience with
R, LaTeX, and Markdown. They will be able to start incorporating
reproducible research tools into their workflow right away. The book
will also be helpful for people who already have general experience
using technologies such as R and LaTeX, but would like to know how to
tie them together for reproducible research.

### Academic researchers

Hopefully so far in this chapter I've convinced you that reproducible
research has benefits for you as a member of the scientific community
and personally as a computational researcher. This book is intended to
be a practical guide for how to actually make your research
reproducible. Even if you already use tools such as R and LaTeX you may
not be leveraging their full potential. This book will teach you useful
ways to get the most out of them as part of a reproducible research
workflow.

### Students

Upper-level undergraduate and graduate students conducting original
computational research should make their research reproducible for the
same reasons that professional researchers should. Forcing yourself to
clearly document the steps you took will also encourage you to think
more clearly about what you are doing and reinforce what you are
learning. It will hopefully give you a greater appreciation of research
accountability and integrity early in your career [@Barr2012; @Ball2012
183].

Even if you don't have extensive experience with computer languages,
this book will teach you specific habits and tools that you can use
throughout your student research and hopefully your careers. Learning
these things earlier will save you considerable time and effort later.

### Instructors

When instructors incorporate the tools of reproducible research into
their assignments they not only build students' understanding of
research best practice, but are also better able to evaluate and provide
meaningful feedback on students' work [@Ball2012 183]. This book
provides a resource that you can use with students to put
reproducibility into practice.

If you are teaching computational courses, you may also benefit from
making your lecture material dynamically reproducible. Your slides will
be easier to update for the same reasons that it is easier to update
research. Making the methods you used to create the material available
to students will give them more information. Clearly documenting how you
created lecture material can also pass information on to future
instructors.

### Editors

Beyond a lack of reproducible research skills among researchers, an
impediment to actually creating reproducible research is a lack of
infrastructure to publish it [@Peng2011]. Hopefully, this book will be
useful for editors at academic publishers who want to be better at
evaluating reproducible research, editing it, and developing systems to
make it more widely available. The journal *Biostatistics* is a good
example of a publication that is encouraging (actually requiring)
reproducible research. From 2009 the journal has had an editor for
reproducibility that ensures replication files are available and that
results can be replicated using these files [@Peng2009]. The more
editors there are with the skills to work with reproducible research the
more likely it is that researchers will do it.

### Private sector researchers

Researchers in the private sector may or may not want to make their work
easily reproducible outside of their organization. However, that does
not mean that significant benefits cannot be gained from using the
methods of reproducible research. First, even if public reproducibility
is ruled out to guard proprietary information,[^7] making your research
reproducible to members of your organization can spread valuable
information about how analyses were done and data was collected. This
will help build your organization's knowledge and avoid effort
duplication. Just as a lack of reproducibility hinders the spread of
information in the scientific community, it can hinder it inside of a
private organization. Using the sort of dynamic automated processes run
with clearly documented source code we will learn in this book can also
help create robust data analysis methods that help your organization
avoid errors that may come from cutting-and-pasting data across
spreadsheets.[^8]

Also, the tools of reproducible research covered in this book enable you
to create professional standardized reports that can be easily updated
or changed when new information is available. In particular, you will
learn how to create batch reports based on quantitative data.

The Tools of Reproducible Research
----------------------------------

This book will teach you the tools you need to make your research highly
reproducible. Reproducible research involves two broad sets of tools.
The first is a **reproducible research environment** that includes the
statistical tools you need to run your analyses as well as "the ability
to automatically track the provenance of data, analyses, and results and
to package them (or pointers to persistent versions of them) for
redistribution". The second set of tools is a **reproducible research
publisher**, which prepares dynamic documents for presenting results and
is easily linked to the reproducible research environment [@Mesirov2010
415].

In this book we will focus on learning how to use the widely available
and highly flexible reproducible research environment--R/RStudio
[@RLanguage; @RStudioCite].[^9] R/RStudio can be linked to numerous
reproducible research publishers such as LaTeX and Markdown with Yihui
Xie's *knitr* package [-@R-knitr] or the related *rmarkdown* package
[@R-rmarkdown]. The main tools covered in this book include:

-   **R**: a programming language primarily for statistics and graphics.
    It can also be useful for data gathering and creating presentation
    documents.

-   ***knitr* and *rmarkdown***: related R packages for literate
    programming. They allow you to combine your statistical analysis and
    the presentation of the results into one document. They work with R
    and a number of other languages such as Bash, Python, and Ruby.

-   **Markup languages**: instructions for how to format a presentation
    document. In this book we cover LaTeX, Markdown, and a little HTML.

-   **RStudio**: an integrated developer environment (IDE) for R that
    tightly combines R, *knitr*, *rmarkdown*, and markup languages.

-   **Cloud storage & versioning**: Services such as Dropbox and
    Git/GitHub that can store data, code, and presentation files, save
    previous versions of these files, and make this information widely
    available.

-   **Unix-like shell programs**: These tools are useful for working
    with large research projects.[^10] They also allow us to use
    command-line tools including GNU Make for compiling projects and
    Pandoc, a program useful for converting documents from one markup
    language to another.

Why Use R, *knitr*/*rmarkdown*, and RStudio for Reproducible Research?
----------------------------------------------------------------------

##### Why R?

Why use a statistical programming language like R for reproducible
research? R has a very active development community that is constantly
expanding what it is capable of. As we will see in this book, R enables
researchers across a wide range of disciplines to gather data and run
statistical analyses. Using the *knitr* or *rmarkdown* package, you can
connect your R-based analyses to presentation documents created with
markup languages such as LaTeX and Markdown. This allows you to
dynamically and reproducibly present results in articles, slideshows,
and webpages.

The way you interact with R has benefits for reproducible research. In
general you interact with R (or any other programming and markup
language) by explicitly writing down your steps as source code. This
promotes reproducibility more than your typical interactions with
Graphical User Interface (GUI) programs like SPSS[^11] and Microsoft
Word. When you write R code and embed it in presentation documents
created using markup languages, you are forced to explicitly state the
steps you took to do your research. When you do research by clicking
through drop-down menus in GUI programs, your steps are lost, or at
least documenting them requires considerable extra effort. Also it is
generally more difficult to dynamically embed your analysis in
presentation documents created by GUI word processing programs in a way
that will be accessible to other researchers both now and in the future.
I'll come back to these points in Chapter
[\[GettingStartedRR\]](#GettingStartedRR){reference-type="ref"
reference="GettingStartedRR"}.

##### Why and ?

Literate programming is a crucial part of reproducible quantitative
research.[^12] Being able to directly link your analyses, your results,
and the code you used to produce the results makes tracing your steps
much easier. There are many different literate programming tools for a
number of different programming languages.[^13] Previously, one of the
most common tools for researchers using R and the LaTeX markup language
was *Sweave* [@Leisch2002]. The packages I am going to focus on in this
book are newer and have more capabilities. They are called *knitr* and
*rmarkdown*. Why are we going to use these tools in this book and not
*Sweave* or some other tool?

The simple answer is that they are more capable than *Sweave*. Both
*knitr* and *rmarkdown* can work with markup languages other than LaTeX
including Markdown and HTML. *rmarkdown* can even output Microsoft Word
documents. They can work with programming languages other than R. They
highlight R code in presentation documents making it easier for your
readers to follow.[^14] They give you better control over the inclusion
of graphics and can cache code chunks, i.e. save the output for later.
*knitr* has the ability to understand *Sweave*-like syntax, so it will
be easy to convert backwards to *Sweave* if you want to.[^15] You also
have the choice to use much simpler and more straightforward syntax with
*knitr* and *rmarkdown*.

*knitr* and *rmarkdown* have broadly similar capabilities and syntax.
They both are literate programming tools that can produce presentation
documents from multiple markup languages. They have almost identical
syntax when used in Markdown. Their main difference is that they take
different approaches to creating presentation documents. *knitr*
documents must be written using the markup language associated with the
desired output. For example, with *knitr*, LaTeX must be used to create
PDF output documents and Markdown or HTML must be used to create
webpages. *rmarkdown* builds directly on *knitr*, the key difference
being that it uses the straightforward Markdown markup language to
generate PDF, HTML, and MS Word documents.[^16]

Because you write with the simple Markdown syntax, *rmarkdown* is
generally easier to use. It has the advantage of being able to take the
same markup document and output multiple types of presentation
documents. Nonetheless, for complex documents like books and long
articles or work that requires custom formatting, *knitr* LaTeX is often
preferable and extremely flexible, though the syntax is more
complicated.

##### Why RStudio?

Why use the RStudio integrated development environment for reproducible
research? R by itself has the capabilities necessary to gather data,
analyze it, and, with a little help from *knitr*/*rmarkdown* and markup
languages, present results in a way that is highly reproducible. RStudio
allows you to do all of these things, but simplifies many of them and
allows you to navigate through them more easily. It also is a happy
medium between R's text-based interface and a pure GUI.

Not only does RStudio do many of the things that R can do but more
easily, it is also a very good standalone editor for writing documents
with LaTeX and Markdown. For LaTeX documents it can, for example, insert
frequently used commands like `\section{}` for numbered sections (see
Chapter [\[LatexChapter\]](#LatexChapter){reference-type="ref"
reference="LatexChapter"}).[^17] There are many LaTeX editors available,
both open source and paid. But RStudio is currently the best program for
creating reproducible LaTeX and Markdown documents. It has full syntax
highlighting. Its syntax highlighting can even distinguish between R
code and markup commands in the same document. It can spell check LaTeX
and Markdown documents. It handles *knitr*/*rmarkdown* code chunks
beautifully (see Chapter
[\[GettingStartedRKnitr\]](#GettingStartedRKnitr){reference-type="ref"
reference="GettingStartedRKnitr"}).

Finally, RStudio not only has tight integration with various markup
languages, it also has capabilities for using other tools such as C++,
CSS, JavaScript, and a few other programming languages. It is closely
integrated with the version control programs Git and SVN. Both of these
programs allow you to keep track of the changes you make to your
documents (see Chapter [\[Storing\]](#Storing){reference-type="ref"
reference="Storing"}). This is important for reproducible research since
version control programs can document many of your research steps. It
also has a built-in ability to make HTML slideshows from
*knitr*/*rmarkdown* documents. Basically, RStudio makes it easy to
create and navigate through complex reproducible research documents.

### Installing the main software {#InstallR}

Before you read this book you should install the main software. All of
the software programs covered in this book are open source and can be
easily downloaded for free. They are available for Windows, Mac, and
Linux operating systems. They should run well on most modern computers.

You should install R before installing RStudio. You can download the
programs from the following websites:

-   **R**: <http://www.r-project.org/>,

-   **RStudio Desktop (Open Source License)**:
    <http://www.rstudio.com/products/rstudio/download/>.

The download webpages for these programs have comprehensive information
on how to install them, so please refer to those pages for more
information.

After installing R and RStudio you will probably also want to install a
number of user-written packages that are covered in this book. To
install all of these user-written packages, please see page .

##### Installing markup languages {#InstallMarkup}

If you are planning to create LaTeX documents you need to install a TeX
distribution.[^18] They are available for Windows, Mac, and Linux
systems. They can be found at: <http://www.latex-project.org/ftp.html>.
Please refer to that site for more installation information.

If you want to create Markdown documents you can separately install the
*markdown* package in R. You can do this the same way that you install
any package in R, with the command.[^19]

##### GNU Make

If you are using a Linux computer you already have GNU
Make[\[InstallMake\]]{#InstallMake label="InstallMake"} installed.[^20]
Mac users will need to install the command-line developer tools. There
are two ways to do this. One is go to the App Store and download Xcode
(it's free). Once Xcode is installed, install command-line tools, which
you will find by opening Xcode then clicking on `Preference`
`Downloads`. However, Xcode is a very large download and you only need
the command-line tools for Make. To install just the command-line tools,
open the Terminal and try to run Make by typing `make` and hitting
return. A box should appear asking you if you want to install the
command-line developer tools. Click `Install`. Windows users will have
Make installed if they have already installed Rtools (see page ). Mac
and Windows users will need to install this software not only so that
GNU Make runs properly, but also so that other command-line tools work
well.

##### Other Tools

We will discuss other tools such as Git that can be a useful part of a
reproducible research workflow. Installation instructions for these
tools will be discussed below.

Book Overview
-------------

The purpose of this book is to give you the tools that you will need to
do reproducible research with R and RStudio. This book describes a
workflow for reproducible research primarily using R and RStudio. It is
designed to give you the necessary tools to use this workflow for your
own research. It is not designed to be a complete reference for R,
RStudio, *knitr*/*rmarkdown*, Git, or any other program that is a part
of this workflow. Instead it shows you how these tools can fit together
to make your research more reproducible. To get the most out of these
individual programs I will along the way point you to other resources
that cover these programs in more detail.

To that end, I can recommend a number of resources that cover more of
the nitty-gritty:[\[OtherBooks\]]{#OtherBooks label="OtherBooks"}

-   Michael J. Crawley's [-@Crawley2013] encyclopaedic R book,
    appropriately titled ***The R Book***, published by Wiley.

-   Hadley Whickham [-@Whickham2014book] has a great new book out from
    Chapman and Hall on ***Advanced R***.

-   Yihui Xie's [-@Xie2013] book ***Dynamic Documents with R and
    knitr***, published by Chapman and Hall, provides a comprehensive
    look at how to create documents with *knitr*. It's a good complement
    to this book's generally more research project--level focus.

-   Norman Matloff's [-@Matloff2011] tour through the programming
    language aspects of R called ***The Art of R Programming: A Tour of
    Statistical Design Software***, published by No Starch Press.

-   Cathy O'Neil and Rachel Schutt [-@ONeil2013] give a great
    introduction the field of data science generally in ***Doing Data
    Science***, published by O'Reilly Media Inc.

-   For an excellent introduction to the command-line in Linux and Mac,
    see William E. Shotts Jr.'s [-@ShottsJr2012] book ***The Linux
    Command-line: A Complete Introduction*** also published by No Starch
    Press. It is also helpful for Windows users running PowerShell (see
    Chapter
    [\[DirectoriesChapter\]](#DirectoriesChapter){reference-type="ref"
    reference="DirectoriesChapter"}).

-   The RStudio website (<http://www.rstudio.com/ide/docs/>) has a
    number of useful tutorials on how to use *knitr* with LaTeX and
    Markdown. They also have very good documentation for *rmarkdown* at
    <http://rmarkdown.rstudio.com/>.

That being said, my goal is for this book to be *self-sufficient*. A
reader without a detailed understanding of these programs will be able
to understand and use the commands and procedures I cover in this book.
While learning how to use R and the other programs I personally often
encountered illustrative examples that included commands, variables, and
other things that were not well explained in the texts that I was
reading. This caused me to waste many hours trying to figure out, for
example, what the `$` is used for (preview: it's the component selector,
see Section [\[ComponentSelect\]](#ComponentSelect){reference-type="ref"
reference="ComponentSelect"}). I hope to save you from this wasted time
by either providing a brief explanation of possibly frustrating and
mysterious things and/or pointing you in the direction of good
explanations.

### How to read this book

This book gives you a workflow. It has a beginning, middle, and end. So,
unlike a reference book, it can and should be read linearly as it takes
you through an empirical research processes from an empty folder to a
completed set of documents that reproducibly showcase your findings.

That being said, readers with more experience using tools like R or
LaTeX may want to skip over the nitty-gritty parts of the book that
describe how to manipulate data frames or compile LaTeX documents into
PDFs. Please feel free to skip these sections.

##### More-experienced R users

If you are an experienced R user you may want to skip over the first
section of Chapter
[\[GettingStartedRKnitr\]](#GettingStartedRKnitr){reference-type="ref"
reference="GettingStartedRKnitr"}: Getting Started with R, RStudio, and
*knitr*/*rmarkdown*. But don't skip over the whole chapter. The latter
parts contain important information on the *knitr*/*rmarkdown* packages.
If you are experienced with R data manipulation you may also want to
skip all of Chapter [\[DataClean\]](#DataClean){reference-type="ref"
reference="DataClean"}.

##### More-experienced LaTeX users

If you are familiar with LaTeX you might want to skip the first part of
Chapter [\[LatexChapter\]](#LatexChapter){reference-type="ref"
reference="LatexChapter"}. The second part may be useful as it includes
information on how to dynamically create BibTeX bibliographies with
*knitr* and how to include *knitr* output in a Beamer slideshow.

##### Less-experienced LaTeX/Markdown users

If you do not have experience with LaTeX or Markdown you may benefit
from reading, or at least skimming, the introductory chapters on these
top topics (chapters
[\[LatexChapter\]](#LatexChapter){reference-type="ref"
reference="LatexChapter"} and
[\[MarkdownChapter\]](#MarkdownChapter){reference-type="ref"
reference="MarkdownChapter"}) before reading Part III.

### Reproduce this book

This book practices what it preaches. It can be reproduced. I wrote the
book using the programs and methods that I describe. Full documentation
and source files can be found at the book's GitHub repository. Feel free
to read and even use (within reason and with attribution, of course) the
book's source code. You can find it at:
<https://GitHub.com/christophergandrud/Rep-Res-Book>. This is especially
useful if you want to know how to do something in the book that I don't
directly cover in the text.

If you notice any errors or places where the book can be improved please
report them on the book's GitHub Issues page:
<https://GitHub.com/christophergandrud/Rep-Res-Book/issues>. Corrections
will be posted at:
<http://christophergandrud.GitHub.io/RepResR-RStudio/errata.htm>.

### Contents overview

The book is broken into four parts. The first part (chapters
[\[GettingStartedRR\]](#GettingStartedRR){reference-type="ref"
reference="GettingStartedRR"},
[\[GettingStartedRKnitr\]](#GettingStartedRKnitr){reference-type="ref"
reference="GettingStartedRKnitr"}, and
[\[DirectoriesChapter\]](#DirectoriesChapter){reference-type="ref"
reference="DirectoriesChapter"}) gives an overview of the reproducible
research workflow as well as the general computer skills that you'll
need to use this workflow. Each of the next three parts of the book
guides you through the specific skills you will need for each part of
the reproducible research process. Part two (chapters
[\[Storing\]](#Storing){reference-type="ref" reference="Storing"},
[\[DataGather\]](#DataGather){reference-type="ref"
reference="DataGather"}, and
[\[DataClean\]](#DataClean){reference-type="ref" reference="DataClean"})
covers the data gathering and file storage process. The third part
(chapters [\[StatsModel\]](#StatsModel){reference-type="ref"
reference="StatsModel"},
[\[TablesChapter\]](#TablesChapter){reference-type="ref"
reference="TablesChapter"}, and
[\[FiguresChapter\]](#FiguresChapter){reference-type="ref"
reference="FiguresChapter"}) teaches you how to dynamically incorporate
your statistical analysis, results figures, and tables into your
presentation documents. The final part (chapters
[\[LatexChapter\]](#LatexChapter){reference-type="ref"
reference="LatexChapter"},
[\[LargeDocs\]](#LargeDocs){reference-type="ref" reference="LargeDocs"},
and [\[MarkdownChapter\]](#MarkdownChapter){reference-type="ref"
reference="MarkdownChapter"}) covers how to create reproducible
presentation documents including LaTeX articles, books, slideshows, and
batch reports as well as Markdown webpages and slideshows.

[^1]: This is close to what [@Lykken1968] calls "operational
    replication".

[^2]: The idea of really reproducible computational research was
    originally thought of and implemented by Jon Claerbout and the
    Stanford Exploration Project beginning in the 1980s and early 1990s
    [@Fomel2009; @Donoho2009]. Further seminal advances were made by
    Jonathan B. Buckheit and David L. Donoho who created the Wavelab
    library of MATLAB routines for their research on wavelets in the
    mid-1990s [@Buckheit1995].

[^3]: Reproducibility is important for both quantitative and qualitative
    research [@King1994]. Nonetheless, we will focus mainly on on
    methods for reproducibility in quantitative computational research.

[^4]: Much of the reproducible computational research and literate
    programming literatures have traditionally used the term "weave" to
    describe the process of combining source code and presentation
    documents [see @Knuth1992 101]. In the R community weave is usually
    used to describe the combination of source code and LaTeX documents.
    The term "knit" reflects the vocabulary of the *knitr* R package
    (knit + R). It is used more generally to describe weaving with a
    variety of markup languages. The term is used by RStudio if you are
    using the *rmarkdown* package, which is similar to *knitr*. We also
    cover the *rmarkdown* package in this book. Because of this, I use
    the term knit rather than weave in this book.

[^5]: See the American Physical Society's website at
    <http://www.aps.org/policy/statements/99_6.cfm>. See also
    [@Fomel2009].

[^6]: Of course, it's important to keep in mind that reproducibility is
    "neither necessary nor sufficient to prevent mistakes"
    [@Stodden2009b].

[^7]: There are ways to enable some public reproducibility without
    revealing confidential information. See [@Vandewalle2007] for a
    discussion of one approach.

[^8]: See this post by David Smith about how the J.P. Morgan "London
    Whale" problem may have been prevented with the type of processes
    covered in this book:
    <http://blog.revolutionanalytics.com/2013/02/did-an-excel-error-bring-down-the-london-whale.html>
    (posted 11 February 2013).

[^9]: The book was created with R version and developer builds of
    RStudio version 0.99.370.

[^10]: In this book I cover the Bash shell for Linux and Mac as well as
    Windows PowerShell.

[^11]: I know you can write scripts in statistical programs like SPSS,
    but doing so is not encouraged by the program's interface and you
    often have to learn multiple languages for writing scripts that run
    analyses, create graphics, and deal with matrices.

[^12]: Donald Knuth coined the term literate programming in the 1970s to
    refer to a source file that could be both run by a computer and
    "woven" with a formatted presentation document [@Knuth1992].

[^13]: A very interesting tool that is worth taking a look at for the
    Python programming language is HTML Notebooks created with IPython.
    For more details see
    <http://ipython.org/ipython-doc/dev/notebook/index.html>.

[^14]: Syntax highlighting uses different colors and fonts to
    distinguish different types of text.

[^15]: Note that the Sweave-style syntax is not identical to actual
    *Sweave* syntax. See Yihui Xie's discussion of the differences
    between the two at: <http://yihui.name/knitr/demo/sweave/>. *knitr*
    has a function (`Sweave2knitr`) for converting *Sweave* to *knitr*
    syntax.

[^16]: It does this by relying on a tool called Pandoc [@Pandoc2014].

[^17]: If you are more comfortable with a what-you-see-is-what-you-get
    (WYSIWYG) word processor like Microsoft Word, you might be
    interested in exploring Lyx. It is a WYSIWYG-like LaTeX editor that
    works with *knitr*. It doesn't work with the other markup languages
    covered in this book. For more information see:
    <http://www.lyx.org/>. I give some brief information on using Lyx
    with *knitr* in Chapter 3's Appendix.

[^18]: LaTeX is is really a set of macros for the TeX typesetting
    system. It is included in all major TeX distributions.

[^19]: The exact command is: .

[^20]: To verify this, open the Terminal and type: `make –version` (I
    used version 3.81 for this book). This should output details about
    the current version of Make installed on your computer.
