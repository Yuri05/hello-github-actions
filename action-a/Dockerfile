FROM rstudio/r-base:3.6.3-centos7

RUN . /etc/bashrc && \
    R -e --no-save "install.packages('R6',dependencies=TRUE, repos='http://cran.rstudio.com/')"
