FROM rstudio/r-base:3.6.3-centos7

COPY installPkgs.R /root/installPkgs.R
RUN . /etc/bashrc && \
    R CMD BATCH /root/installPkgs.R

RUN rm -rf /root/installPkgs.R
