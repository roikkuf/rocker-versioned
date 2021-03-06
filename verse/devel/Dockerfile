FROM rocker/tidyverse:devel
MAINTAINER "Carl Boettiger" cboettig@ropensci.org

## Add LaTeX, rticles and bookdown support
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ghostscript \
    imagemagick \
    ## system dependency of hadley/pkgdown
    libmagick++-dev \
    ## system dependency of hunspell (devtools)
    libhunspell-dev \
    ## R CMD Check wants qpdf to check pdf sizes, or iy throws a Warning 
    qpdf \
    ## for git via ssh key 
    ssh \
    ## for building pdfs via pandoc/LaTeX
    lmodern \
    texlive-fonts-recommended \
    texlive-humanities \
    texlive-latex-extra \
    texinfo \
    ## just because
    less \
    vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/ \
  ## R manuals use inconsolata font, but texlive-fonts-extra is huge, so:
  && cd /usr/share/texlive/texmf-dist \
  && wget http://mirrors.ctan.org/install/fonts/inconsolata.tds.zip \
  && unzip inconsolata.tds.zip \
  && rm inconsolata.tds.zip \
  && echo "Map zi4.map" >> /usr/share/texlive/texmf-dist/web2c/updmap.cfg \
  && mktexlsr \
  && updmap-sys \
  ## And some nice R packages for publishing-related stuff 
  && . /etc/environment \ 
  && install2.r --error --repos $MRAN --deps TRUE \
    bookdown rticles rmdshower

## Consider including: 
# - libv8-dev (Javascript V8 packages)
# - yihui/printr R package (when released to CRAN)
# - jekyll ruby-rouge (servr R package, Jekyll)
# - jags 4.2 (build from source, repo version too old and apt-tagging forces upgrade of all compiler libs)
# - libgdal-dev libproj-dev libgeos-dev (for rgdal and related geo deps)
# - libgsl0-dev (GSL math library dependencies)
# - liblzma-dev libbz2-dev libiuc-dev (dev libraries needed to build R, also used to build littler & rJava)
# - default-jdk needed for rJava

