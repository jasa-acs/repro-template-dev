JASA Sharing Reproducible Materials over Github
================

This GitHub repository contains a template structure for author(s) who
submit to JASA (either Applications and Case Studies or Theory and
Methods) to include materials to reproduce analyses, visualizations, and
tables.

We provide this template as a default structure that we think could be
useful for many projects, either as is or with modifications by authors.
However, the template is intended to be helpful and is by no means
required of authors. Authors should consult [our reproducibility
guide](https://jasa-acs.github.io/repro-guide) for details on what is
required of reproducibility materials submitted with JASA revisions (not
required upon initial submission).

## Why is template repository this useful?

The purpose of this template repository is to provide a mechanism for
author(s) to share their materials via a Git repository, hosted on a
cloud-based repository manager such as GitHub or GitLab. This provides
the following advantages for author(s):

1.  Analyses (including code, narrative text, output, plots, etc) can be
    version controlled (or branched or forked) allowing original
    author(s) to continue to develop the analyses or other data analysts
    to build off the analyses. Also iterations and changes to the
    analysis are then available via the Git commit history.
2.  Materials are easily available to other researchers.
3.  Preparing a repository also makes it easy for the JASA associate
    editors for reproducibility to copy the materials for a JASA article
    into the JASA GitHub repository.
4.  Others?

## How does the process work?

### Step 1

Author(s) create a public GitHub repository by

1.  Forking this template repository
2.  Using `git clone` and removing the `.git` file
3.  (need to add steps to init a new repository and push to
    github/gitlab/etc.)

Alternatively, author(s) can manually create their own repository with
the structure of this repository (possibly with modifications).

### Step 2

Author(s) edit (or replace) the manuscript template file and add their
data, code, and other files.

**Importantly, the authors should provide an overview of how to carry
out the analyses presented in their manuscript in the README.md of their
repository, replacing the content in this file.** This overview would
generally refer to scripts/code files that execute the analyses and are
placed either in the main directory or the `code` subdirectory. The
*Workflow* section of the ACC form should refer to this README.md as
containing the instructions for how to reproduce the analyses.

### Step 3

Author(s) use `git commit` to track changes over time and use `git push`
to push changes to a repository on the author(s) personal GitHub
account.

### Step 4

Author(s) submit a link to their GitHub repository as part of the [JASA
Reproducibility review
process](https://jasa-acs.github.io/repro-guide/).

### Step 5

JASA Associate Editors for Reproducibility will review the materials in
the personal GitHub repository of the authors and submit a
reproducibility review as part of the standard JASA review process.
Authors have the opportunity to respond to the review by making changes
and pushing their changes to their personal GitHub repository.

**Should reviewers/editors be allow to provide pull requests?**

*My initial two cents is that we hold off on PRs // CJP*

### Step 6

Once the manuscript is accepted, the materials in the author(s) personal
GitHub repository will be copied to the [JASA
repository](https://github.com/jasa-acs).

## Description of template structure using R

Two preferred file structures for submissions are shown below. The goals
in prescribing this structure are to make it easier for the
reproducibility reviewer to confirm the materials are sufficient for
reproducing the results as well as facilitating automated generation of
the outputs via Docker, Singularity, or Github Actions.

## Reproduciblity materials only

The first is for the case where reproducibility materials are being
provided and are separate from the manuscript.

    ## 
    ## project directory
    ##   |-- .here
    ##   |  o-- object of type(s):file
    ##   |-- README.md
    ##   |  o-- object of type(s):file
    ##   |-- renv/
    ##   |  o-- object of type(s):dir
    ##   |-- manuscript/
    ##   |  o-- object of type(s):dir
    ##   |-- data/
    ##   |  o-- object of type(s):dir
    ##   |-- code/
    ##   |  o-- object of type(s):dir
    ##   o-- output/
    ##      o-- object of type(s):dir

## Reproducible document

The second is for manuscripts written as R Markdown documents (this
repository).

    ## 
    ## project directory
    ##   |-- manuscript.rmd
    ##   |  o-- object of type(s):file
    ##   |-- renv/
    ##   |  o-- object of type(s):dir
    ##   |-- preprocessing/
    ##   |  o-- object of type(s):dir
    ##   o-- data/
    ##      o-- object of type(s):dir

## Guidance on the use of reproducible environments

Submissions may include the use of reproducible environments capturing
state of a machine generating manuscript artifacts and even the
manuscript itself. Here we discuss two types of reproducible
environments and their use.

### Package environments

Package environments capture the set of packages used by a programming
language needed to generate output. The R programming language has
`renv`, `switchr` and others to accomplish this, Python has `venv`,
`conda` and others, and Julia has native support (through the `Pkg`
package). When submitting these types of environments, the following are
suggested.

1.  Provide documentation indicating the language environment and the
    version was used to produce outputs.
2.  Use a single package environment for all reproducible content.
3.  Prefer packages from package repositories (CRAN, Bioconductor,
    RForge.net for example).
4.  If you use packages from a code repository (Github, Gitlab, etc.)
    then use a release version. If none is available fork the repository
    and provide a release.

### Virtual environments

Virtual capture like docker and singularity for example, capture the
entire computing environment in which computations were performed. In
general, they are a more robust solution, capable of taking a “snapshot”
of a machine including any system-level utilities and external libraries
needed to perform you computation. They have the advantage that
reproducing materials mean running the virtual environment, rather than
recreating the programming language environment and may be preferred.
When submitting these types of environments, the following are
suggested.

1.  Provide a single saved image with shared folder referencing the
    reproducibility file structure described above.
2.  If a single saved image is not being submitted, be aware of the
    suggestions provided in the [Package
    environments](#package-environments) section above.

## References

Gentleman, Robert, and Duncan Temple Lang. “[Statistical Analyses and
Reproducible
Research](http://biostats.bepress.com/cgi/viewcontent.cgi?article=1001&context=bioconductor).”
(2004).

Gentleman, Robert. “[Reproducible research: a bioinformatics case
study](https://www.degruyter.com/document/doi/10.2202/1544-6115.1034/html).”
Statistical applications in genetics and molecular biology 4.1 (2005).

Marwick, Ben, and Bryan, Jennifer, and Attali, Dean, and Hollister,
Jeffrey W. [rrrpkg Github Page](https://github.com/ropensci/rrrpkg).
