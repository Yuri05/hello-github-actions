FROM rstudio/r-base:3.6.3-centos7

#COPY installPkgs.R /root/installPkgs.R
RUN . /etc/bashrc && \
    R -e "install.packages('ggplot2',dependencies=TRUE, repos='http://cran.rstudio.com/')"

#RUN rm -rf /root/installPkgs.R
