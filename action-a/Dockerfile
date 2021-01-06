FROM rstudio/r-base:3.6.3-centos7

ENTRYPOINT ["sh", "-c"]

RUN . /etc/bashrc && \
    R --no-save -e "install.packages('R6', repos='http://cran.rstudio.com/')" 
