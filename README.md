# Science.md
An easy framework for drafting scientific documents: *Write* (Markdown), *Compile* (PDF, Word, HTML), *Share*.

![Science.md Howto](https://cloud.githubusercontent.com/assets/7942719/20758851/0b97e1be-b713-11e6-955e-e6d0a96b3a59.png)

## Concept

This framework is designed to make writing easier. It provides lots of helper scripts to do the work for you, like building the manuscript PDF, creating folders for milestones, generating diffs, and more. You can focus on writing, while formating, compiling, and collaborating will just work like a charm.

### Philosophy: 100% tolerance, 0% borders

This product aims to serve everyone and does not try to convince people to use a specific platform or programming language. 

- *Latex-Lovers and Word-Ethusiasts* (Writers meet in the middle with Markdown, Colleagues can put comments in PDF or Word)
- *Console-geeks and Explorer-clickers* (All scripts work from terminal as well as by a gentle double-click)
- *Online-addicted and offline-nostalgist* (It's all local, but you can sync with a remote repo any time)
- *Security-paranoiacs and white-hearted* (No dependency on someone else's server, it's all yours!)
- *Hillary and Donald*

### Technology

No fancy hacking. No strange dependencies. *Science.md* only uses standard shell commands, and well-accepted software tools (Pandoc, LaTeX, latexdiff, mutools). Even the templates are based on Pandoc's defaults with only tiny scholarly adpations. To be honest, the whole magic boils down to the Makefile and a few short scripts that let you process your manuscript as easy as pressing a button.

### Advantages to other collaborative writing tools:

- **Write in Markdown:** Focus on writing, not on Latex's commands or Word's formatting mess. Paper writing is now possible with simple plain text. And so is commenting by individual collaborators, creation of Gantt charts, and many more.
- **Self-hosting repositories:** use any version control software hosted by you or your institution. Many institutions do not allow research to be hosted at someone else's server. You don't even have to use a remote repository, it's all yours!
- **Work offline** from any location. That allows you to be independent from Wifi, and still be able to do fancy WYSIWYG writing in Markdown, e.g., using [Typora](http://www.typora.io/). 
- **Full control:** It's your own folder, your own desktop, your own data. Add analysis scripts, processed data, sketches, ideas, and share anything without being bothered to upload. And by the way, it's only you who decides who has access to your repository.
- **Fast compilation:** PDF and Word documents are created within seconds. By sharing both, your colleagues can choose how they want to annotate and comment your work. Want to put your paper on a website? It's just a millisecond away.
- **Fully adaptable:** all the scripts and templates are open-source. Adapt it to your needs. For example, use a specific journal template, or add more features. 
- **Project planning included:** Markdown-based tools to make *Gantt* and *Task lists*. 

## Screenshots

- Many screenshots are presented in [Issue #1](https://github.com/mschroen/Science.md/issues/1).
- Please have a look at the files `release/science.md.*` to view some examples.
- Here is a summary of some visualisations of *Science.md* output:

![Science.md Screenshots of output](https://cloud.githubusercontent.com/assets/7942719/21054952/82028d20-be27-11e6-9967-c32f4cf72eb8.png)

## Requirements 

### OS

*Science.md* uses no OS-specific software and thus should work on any operating system. However, so far it has been tested only on Windows, and I would be glad if someone could test it on Mac and Linux!  
#### config and run on amazon AMI linux  

- get docker run on AMAZON AMI     

> sudo yum install docker  

- get an image which is ready for pandoc and texlive ,fortunitly, there is one which we an use out-of-box.

> sudo docker pull ivotron/pandoc  

> in your AMI linux ,use git to get Scince.md,then change to the direcotry.

- then we can run the docker like this:  

>sudo docker run -d --name myscimd -v `pwd`:/usr/scimd ivotron/pandoc  

>since there is no *scimd* direcotry in the ivotron/pandoc image ,you should first go into a running one ,mkdir and then commmit the change.   

- go into the docker container like this:    

> sudo docker run exec -it *containerid* /bin/bash/   

- go into /usr/scimd   

> cd /usr/scimd  

- then use cmd :  

> make -s pdf  or any others ,enjoy:). becuase we use docker to mount a direcoty ,you can find you output in you host linux ,they are in *Scince.md/release* direcotry.






### Editing

You do not need anything to write your draft, but a simple text editor to edit the files `content/*.md`. Some text editor suggestions:

- Simple, fast, syntax-highlighting: [Notepad2](https://xhmikosr.github.io/notepad2-mod/),
- Advanced, powerful, incl. Markdown preview: [Atom Editor](https://atom.io/),
- *(most intuitive)* What you see is what you get: [Typora](https://www.typora.io/#download).

### Compiling

If you want to compile your text to LaTeX, PDF, Word, or HTML, you need:

- [pandoc](http://pandoc.org/installing.html), and the additional [cross-ref filter](https://github.com/lierdakil/pandoc-crossref/releases/). The latter is to be extracted into the same folder as pandoc was installed.
- `pdflatex`, e.g., from the [TeXlive distribution](https://www.tug.org/texlive/acquire-netinstall.html),

Then some very basic `bash` commands are needed. Most of them are actually standard on Linux and Mac, but Windows sometimes needs a slight additional kick.

- `make`, `cat`, `sed`, `du`, `rm`, `wc`, e.g. from the [cygwin distribution](https://cygwin.com/install.html).
- *(Optional):* A useful terminal, e.g., `mintty`, also from cygwin.

I recommend creating `.png` equivalents from every `.pdf` figure, such that HTML and Word output can actually display the (originally `.pdf`) figures. There is a handy script for this job in `fig/pdf2png.bat`, which requires *mutools*:

- [mutools software](http://mupdf.com/).

> *General Note: Please make sure that all the binary files of the installed tools are accessible from command line, i.e., registered in the system paths. E.g. on Windows, add all folders containing `pandoc.exe`, `pdflate.exe`, `mutools.exe`, `cygwin/bin/sed.exe`, ..., to the system path via `Control Panel > System > Advanced > Environmental Variables`.*
>


## Workflow

To start writing your paper, use this *Science.md* repository as a template. Just download the whole repository and copy all its content into the folder of your project, which is probably called "my_nature_paper-no3". 

If you want to version-control or share your work, I'd recommend `git` , but also `svn` or anything else would do, it's all your choice. You can self-host the repository remotely on your own server if you want.  There are many GUI tools for version-control, from which I think [GitHub Desktop](https://desktop.github.com/) is the most easy to use for non-geeks. 

1. **Get up to date with remote changes:** `git pull`, or with *GitHub Desktop* press `Sync`.
2. **Examine what your colleagues did:** `git diff` or `git log`, or with *GitHub Desktop*'s `History` tab. Or use run the script `release/diff.bat` to create a *latexdiff* between the current and the latest released version.
3. **Contribute:** change text in `content/*.md`, add figures to `fig/*`, etc.
4. *(Optional):* compile to HTML, Word, PDF using `make -s all` or `make.bat`.
5. *(Optional):* store a milestone version by using `release/release.bat`.
6. **Commit your work:** `git add . && git commit -am "Message"`, or with *GitHub Desktop* press `Commit`.
7. **Upload your contribution:** `git push`, or with *GitHub Desktop* press `Sync`.

As soon as your paper is ready and went smoothly through the internal review, you can submit it to a journal. You can either submit the Word document, or the LateX document. Some journals require a certain LaTeX template, which should be easy to fill with the content from `release/NAME.tex` that *Science.md* generated for you.

### Comments

- **Visible** comments are framed by double equal signs, followed by your initials, space, and the text, e.g. `==XX I better like invisble comments, though.==`. Use the YAML settings in `content/title.md` to add individual initials and the corresponding colors. *Typora* will highlight these comments with yellow shade if the setting is activated in the program preferences. In *MS Word*, individual colors are not supported due to *pandoc* limitations. Comments in general must *not* contain equal signs. 
- **Invisible** comments will not appear in the compiled output and can be of any length. Those comments follow the HTML style guide and look like this: `<!--- this is a comment --->`.

### Figures

- Figure files are located in the folder `fig/`
- Always try to create `.pdf` files to assure high-quality figures. Only for pure photographs `.jpg` is acceptable. After adding or changing `.pdf` figures, go to `fig/` and run `pdf2png.bat`. This will convert all `.pdf` figures to `.png` equivalents, which are easier to visualize in text editors, Word, and web browsers.
- Add figures to the Markdown text using `![caption](../fig/name.png){#fig:label}`. Use the  `.png` extension even for `.pdf` figures, to make them visible for Typora, Word, HTML. The PDF compiled output will always use the corresponding `.pdf` file.

### Literature

Add a citation using `@Eistein1905` or `[see also @Eistein1905]`. The corresponding name must be appended to `lit/references.bib`. Those BibTeX entries can be found everywhere in the internet, e.g. using the *google scholar* search engine or the export feature of any reference manager.

### Compile

The text from `content/*.md` can be compiled to Markdown, LaTeX, PDF, or Word. 

1. *(Once):* Open the file `Makefile` or `make.bat` and make sure that the `.md` files are arranged in the correct order. If you added new files to `content/`, also add them to the given list.
2. If you have a capable terminal, run `make -s all` to compile to all available output formats. Use the flag `-s` to reduce verbose output. The following commands are available:
   * Markdown: `make -s`
   * LaTeX:    `make -s tex`
   * PDF:      `make -s pdf`
   * Word:     `make -s docx`
   * all:      `make -s all`
   * tidy up:  `make clean`

3. *(Or):* On Windows, you can simply double-click the file `make.bat` to compile to all output formats.

### Release

The currently compiled files are stored in `release/` and can be copied to an extra folder, `release/version[Date]-[Time]`, to permanently save one version, which can be used later to perform diffs, for instance. This process has been automated, simply go to `release/` and run `release.bat`.

### Difference between two versions

- The difference between two commits can be visualised with `git diff`, or using the *GitHub Desktop* GUI.
- The difference between two released versions can be visualised using the `latexdiff` script that usually comes with the `texlive` distribution. Edit the file `diff.bat` by specifiying the two folders which you want to compare (the *new* version defaults to the current files in the `release/`folder). Then run `diff.bat`. It creates diffs from the two `.tex` files in the given folders and compiles a new `diff.pdf` where differences are nicely highlighted.

## Markdown Syntax

- citation: `@Einstein2015`, or `[see @Einstein2015; @Newton1730, and references therein]`
- section: `# Section`, `## Subsection`, `### Subsubsection {#sec:label}`, ...
- figure: `![caption](../fig/file.png){#fig:label}`
- math: `$x=1$`, `$$ A=B $$ {#eq:label}`, `$$\begin{aligned} A &= B \\ C &= A+B \end{aligned}$$`
- reference: `@Fig:label`, `[@Fig:label1; @fig:label1]`, `@sec:label`, `@eq:label`, `@tbl:label`, `[Appendix @sec:label]`, `[Appendices @sec:label1; Appendices @sec:label1]`
- comments: `==XX a random comment==`, `==MS a personalized comment==` (defined in *content/title.md*), `<!--- invisible comment --->`
- code: `` `code` `` or paragraphs with a left-padding of 4 spaces 
- table:
    ```
    |  A  |               B | C     |
    | --: | --------------: | :---: |
    |  42 |         $y=x+1$ | True  |
    |  23 |            None | False |

    Table: Caption. {#tbl:label}
    ```

## Further reading

1. G. Wilson et al. (2016): [*Good Enough Practices in Scientific Computing*](https://arxiv.org/abs/1609.00037)
2. A. Bartlett (2016): [Git for Humans](https://speakerdeck.com/alicebartlett/git-for-humans)
3. StackExchange TeX (2014): [*LaTeX vs Word; improvements of LaTeX over the years*](http://tex.stackexchange.com/questions/218567/latex-vs-word-improvements-of-latex-over-the-years)
4. D. Krishnamurthy (2015): [*Writing Technical Papers with Markdown*](http://blog.kdheepak.com/writing-papers-with-markdown.html)
5. Ch. Krycho (2015): [*Academic Markdown and Citations*](http://www.chriskrycho.com/2015/academic-markdown-and-citations.html)
6. D. Leijen (2016): [*Madoko - Write Beautiful Documents*](https://www.madoko.net/)
7. Knauff and Nejasmic (2015): [*An Efficiency Comparison of Document Preparation Systems Used in Academic Research and Development*](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0115069)
8. Marcio von Muhlen (2014): [*We Need a Github of Science*](http://marciovm.com/i-want-a-github-of-science/)
