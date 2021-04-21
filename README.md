# Template: Workshop Reader

This repository is a template for workshop readers for the UC Davis DataLab.
This template uses **bookdown** to knit the reader. You can also optionally use
**renv** to manage packages and Git Large File Storage to manage large files
(instructions included).

To get started, create a new repo on GitHub from this template
([instructions][gh]), then `git clone` your new repo.

[gh]: https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template

Once you've cloned the repo, here's a checklist of things to do to prepare the
repo:

1. **renv** (optional): To set up **renv**, open R at the top level of the repo
   and run:

    ```r
    renv::init()
    ```

    Restart R. Then, to install the **bookdown** toolchain to the project
    package library, run:

    ```r
    install.packages("bookdown")
    renv::snapshot()
    ```

    You can skip this step if you're not going to use **renv**.

2. `index.Rmd`: Replace the all-caps text with your workshop details.
    + Title (in 2 places, 1 of them in the `output:` HTML block)
    + Author's name
    + Repo name (in 4 places, 2 of them in the `output:` HTML block)
    + Description, learning goals, & prerequisites

3. `README.md`: Replace the all-caps text with your workshop details.
    + Title
    + Quarter & year
    + Author's name & email
    + Reader URL
    + Event URL
    + Description, learning goals, & prerequisites

4. GitHub: In the repo's About section, add the reader URL and appropriate
   tags.

5. GitHub: In the repo's Settings page, enable GitHub pages. Set the branch to
   `master` and the directory to `docs/`.

6. `README.md`: Remove these template instructions, which end at the `#
   Workshop:` header below

7. `git add` all changed files, then `git commit` and `git push`.


# Workshop: YOUR WORKSHOP TITLE

_[UC Davis DataLab](https://datalab.ucdavis.edu/)_  
_Spring 2021_  
_Instructor: Michele Tobias, PhD <<mmtobias@ucdavis.edu>>_  

* [Reader](https://ucdavisdatalab.github.io/workshop_coordinate_reference_systems/)
* [Event Page](https://datalab.ucdavis.edu/eventscalendar/maptimedavis-projected-coordinate-systems-in-r/)

## Description 
In this workshop, participants will learn about projected coordinate reference systems (CRS, commonly called “projections”) and how to apply them in R to spatial data. We will discuss the components of a CRS, how to apply them, how to translate your data into a different CRS, and how to choose a CRS.

## Learning Objectives
By the end of this workshop, participants will have a better understanding of what a projected coordinate system is, why you would choose one over another, and how to apply them correctly to geospatial data in R.

## Prerequisites
Participants should have a basic understanding of R (for example, be able to create variables and load common data formats like a CSV) and a basic understanding of GIS data formats (e.g., raster and vector data). Participants should also install R and RStudio.


## Contributing

The course reader is a live webpage, hosted through GitHub, where you can enter
curriculum content and post it to a public-facing site for learners.

To make alterations to the reader:

1.  Run `git pull`, or if it's your first time contributing, see
    [Setup](#setup).

2.  Edit an existing chapter file or create a new one. Chapter files are R
    Markdown files (`.Rmd`) at the top level of the repo. Enter your text,
    code, and other information directly into the file. Make sure your file:

    - Follows the naming scheme `##_topic-of-chapter.Rmd` (the only exception
      is `index.Rmd`, which contains the reader's front page).
    - Begins with a first-level header (like `# This`). This will be the title
      of your chapter. Subsequent section headers should be second-level
      headers (like `## This`) or below.
    - Uses caching for resource-intensive code (see [Caching](#caching)).

    Put any supporting resources in `data/` or `img/`. For large files, see
    [Large Files](#large-files). You do not need to
    add resources generated by your R code (such as plots). The knit step saves
    these in `docs/` automatically.

3.  Run `knit.R` to regenerate the HTML files in the `docs/`. You can do this
    in the shell with `./knit.R` or in R with `source("knit.R")`.

4.  Run `renv::snapshot()` in an R session at the top level of the repo to
    automatically add any packages your code uses to the project package
    library.

5.  When you're finished, `git add`:
    - Any files you added or edited directly, including in `data/` and `img/`
    - `docs/` (all of it)
    - `_bookdown_files/` (contains the **knitr** cache)
    * `renv.lock` (contains the **renv** package list)
    - `.gitattributes` (contains the Git LFS file list)

    Then `git commit` and `git push`. The live web page will update
    automatically after 1-10 minutes.


### Caching

If one of your code chunks takes a lot of time or memory to run, consider
caching the result, so the chunk won't run every time someone knits the
reader. To cache a code chunk, add `cache=TRUE` in the chunk header. It's
best practice to label cached chunks, like so:

````
```{r YOUR_CHUNK_NAME, cache=TRUE}
# Your code...
```
````

Cached files are stored in the `_bookdown_files/` directory. If you ever want
to clear the cache, you can delete this directory (or its subdirectories).
The cache will be rebuilt the next time you knit the reader.

Beware that caching doesn't work with some packages, especially packages that
use external libraries. Because of this, it's best to leave caching off for
code chunks that are not resource-intensive.


### Large Files

If you want to include a large file (say over 1 MB), you should use git LFS.
You can register a large file with git LFS with the shell command:

```sh
git lfs track YOUR_FILE
```

This command updates the `.gitattributes` file at the top level of the repo. To
make sure the change is saved, you also need to run:

```sh
git add .gitattributes
```

Now that your large is registered with git LFS, you can add, commit, and push
the file with git the same way you would any other file, and git LFS will
automatically intercede as needed.

GitHub provides 1 GB of storage and 1 GB of monthly bandwidth free per repo for
large files. If your large file is more than 50 MB, check with the other
contributors before adding it.


## Setup


### Git LFS

This repo uses [Git Large File Storage][git-lfs] (git LFS) for large files. If
you don't have git LFS installed, [download it][git-lfs] and run the installer.
Then in the shell (in any directory), run:

```sh
git lfs install
```

Then your one-time setup of git LFS is done. Next, clone this repo with `git
clone`. The large files will be downloaded automatically with the rest of the
repo.

[git-lfs]: https://git-lfs.github.com/


### R Packages

This repo uses [**renv**](https://rstudio.github.io/renv/) for package
management. Install **renv** according to the installation instructions on
their website.

Then open an R session at the top level of the repo and run:

```r
renv::restore()
```

This will download and install the correct versions of all the required
packages to **renv**'s package library. This is separate from your global R
package library and will not interfere with other versions of packages you have
installed.

[Back to Top](#top)
