FROM rstudio/r-base:3.6.3-centos7

RUN . /etc/bashrc && \
    R -e "install.packages('R6',dependencies=TRUE, repos='http://cran.rstudio.com/')" --no-save 
#    R -e "install.packages('knitr',dependencies=TRUE, repos='http://cran.rstudio.com/')" --no-save \
#    R -e "install.packages('rmarkdown',dependencies=TRUE, repos='http://cran.rstudio.com/')" --no-save \
#    R -e "install.packages('testthat',dependencies=TRUE, repos='http://cran.rstudio.com/')" --no-save \
#    R -e "install.packages('pander',dependencies=TRUE, repos='http://cran.rstudio.com/')" --no-save 
    
