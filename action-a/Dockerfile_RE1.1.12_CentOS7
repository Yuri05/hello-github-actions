FROM rstudio/r-base:3.6.3-centos7

ENTRYPOINT ["sh"]

# Install R package dependencies
RUN R --no-save -e "install.packages('R6', repos='http://cran.rstudio.com/')"

# Install mono
RUN rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" && \
    yum update -y && \
    yum-config-manager --add-repo http://repo1.xorcom.com/repos/mono-project/mono-project/ && \
    yum install -y mono-complete-0:5.18.0.240-0.xamarin.2.epel7.x86_64

# Install nuget, dotnet-sdk-3.1, and msbuild
RUN yum install -y libxml2-devel git nuget openmpi-devel && \
    rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm && \
    yum install -y https://packages.microsoft.com/centos/7/prod/netstandard-targeting-pack-2.1.0-x64.rpm && \
    yum install -y dotnet-sdk-3.1

# Get software
ADD https://github.com/Open-Systems-Pharmacology/rClr/releases/download/v0.8.3_Linux/rClr_0.8.3_CentOS7.tar.gz /root/
ADD https://github.com/Open-Systems-Pharmacology/OSPSuite-R/releases/download/v9.1.4/ospsuite_9.1.4_centOS7.tar.gz /root/

# Install rClr and ospsuite
RUN R CMD INSTALL /root/rClr_0.8.3_CentOS7.tar.gz && \
    R CMD INSTALL /root/ospsuite_9.1.4_centOS7.tar.gz --install-tests

RUN rm -rf /root/rClr_0.8.3_CentOS7.tar.gz \
           /root/ospsuite_9.1.4_centOS7.tar.gz 

ENV LC_ALL=en_US.UTF-8
ENV LD_LIBRARY_PATH="/usr/lib64/openmpi/lib:/opt/R/3.6.3/lib/R/library/ospsuite/lib:$LD_LIBRARY_PATH"
ENV PATH="/opt/R/3.6.3/bin:${PATH}"

# Simple test: run a population simulation
RUN R --no-save -e "library(ospsuite);setwd(system.file('extdata', package = 'ospsuite'));sim=loadSimulation('simple.pkml');pop=loadPopulation('simple_pop.csv');runSimulation(sim, pop)"

# Install testthat and run all package tests
# RUN R --no-save -e "install.packages('testthat', repos='http://cran.rstudio.com/')" 
# RUN R --no-save -e "setwd(system.file('tests', package = 'ospsuite')); source('testthat.R')" 

# ================== Next steps are required for the reporting engine only

# Install pandoc
ADD https://github.com/jgm/pandoc/releases/download/2.9.2.1/pandoc-2.9.2.1-linux-amd64.tar.gz /root/
RUN mkdir /pandoc && \
    cd /pandoc && \
    mv /root/pandoc-2.9.2.1-linux-amd64.tar.gz /pandoc && \
    tar -xzf pandoc-2.9.2.1-linux-amd64.tar.gz && \
    rm -f /usr/bin/pandoc && \
    ln -s /pandoc/pandoc-2.9.2.1/bin/pandoc /usr/bin/pandoc

ADD https://github.com/Open-Systems-Pharmacology/TLF-Library/releases/download/v1.1.1/tlf_1.1.1.tar.gz /root/
ADD https://ci.appveyor.com/api/buildjobs/g792yu9hohdx6hkn/artifacts/ospsuite.reportingengine_1.1.12.tar.gz /root/
ADD https://cran.r-project.org/src/contrib/Rmpi_0.6-9.tar.gz /root/

RUN R --no-save -e "install.packages('ggplot2', repos='http://cran.rstudio.com/')" && \
    R --no-save -e "install.packages('reshape2', repos='http://cran.rstudio.com/')" && \
    R --no-save -e "install.packages('knitr', repos='http://cran.rstudio.com/')" && \
    R CMD INSTALL /root/tlf_1.1.1.tar.gz --install-tests && \
    R CMD INSTALL /root/ospsuite.reportingengine_1.1.12.tar.gz --install-tests && \
    R CMD INSTALL /root/Rmpi_0.6-9.tar.gz --configure-args="--with-Rmpi-include=/usr/include/openmpi-x86_64 --with-Rmpi-libpath=/usr/lib64/openmpi/lib --with-Rmpi-type=OPENMPI"

RUN rm -rf /root/ospsuite.reportingengine_1.1.12.tar.gz \
           /root/tlf_1.1.1.tar.gz \
           /root/Rmpi_0.6-9.tar.gz
           
# Install testthat and run all package tests
# RUN R --no-save -e "install.packages('testthat', repos='http://cran.rstudio.com/')" 
RUN R --no-save -e "setwd(system.file('tests', package = 'ospsuite.reportingengine')); source('testthat.R')" 
