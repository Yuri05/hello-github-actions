# FROM debian:9.5-slim
FROM rstudio/r-base:3.6.3-centos7

# Install mono
RUN rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" && \
    yum-config-manager --add-repo http://repo1.xorcom.com/repos/mono-project/mono-project/ && \
    yum install -y mono-complete-0:5.18.0.240-0.xamarin.2.epel7.x86_64

# Install nuget, dotnet-sdk-3.1, and msbuild
RUN yum install -y libxml2-devel git nuget openmpi-devel && \
    rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm && \
    yum install -y https://packages.microsoft.com/centos/7/prod/netstandard-targeting-pack-2.1.0-x64.rpm && \
    yum install -y dotnet-sdk-3.1
# yum install -y msbuild && \
# module load mpi

# Install pandoc
# Skipp installing pandoc, since this cause the qualification to fail
# ADD https://github.com/jgm/pandoc/releases/download/2.9.2.1/pandoc-2.9.2.1-linux-amd64.tar.gz /root/
# RUN mkdir /pandoc && \
#     cd /pandoc && \
#     mv /root/pandoc-2.9.2.1-linux-amd64.tar.gz /pandoc && \
#     tar -xzf pandoc-2.9.2.1-linux-amd64.tar.gz && \
#     rm -f /usr/bin/pandoc && \
#     ln -s /pandoc/pandoc-2.9.2.1/bin/pandoc /usr/bin/pandoc


# Get software
ADD https://github.com/Open-Systems-Pharmacology/TLF-Library/releases/download/v1.0.68/tlf_1.0.68.tar.gz /root/
ADD https://github.com/Open-Systems-Pharmacology/rClr/files/4127362/rClr_0.8.3_CentOS7.tar.gz /root/
ADD https://github.com/Open-Systems-Pharmacology/OSPSuite-R/releases/download/v9.1/ospsuite_9.1.1_centOS7.tar.gz /root/
ADD https://github.com/Open-Systems-Pharmacology/OSPSuite.ReportingEngine/releases/download/v1.0.73/ospsuite.reportingengine_1.0.73.tar.gz /root/
# ADD https://cran.r-project.org/src/contrib/Rmpi_0.6-9.tar.gz /root/

# Install tlf, rClr, ospsuite and reportingengine
RUN . /etc/bashrc && \
    R CMD INSTALL /root/tlf_1.0.68.tar.gz && \
    R CMD INSTALL /root/rClr_0.8.3_CentOS7.tar.gz && \
    R CMD INSTALL /root/ospsuite_9.1.1_centOS7.tar.gz && \
    R CMD INSTALL /root/ospsuite.reportingengine_1.0.73.tar.gz
#    R CMD INSTALL /root/Rmpi_0.6-9.tar.gz --configure-args="--with-Rmpi-include=/usr/include/openmpi-x86_64 --with-Rmpi-libpath=/usr/lib64/openmpi/lib --with-Rmpi-type=OPENMPI" && \


RUN rm -rf /root/tlf_1.0.68.tar.gz \
           /root/rClr_0.8.3_CentOS7.tar.gz \
           /root/ospsuite_9.1.1_centOS7.tar.gz \
           /root/ospsuite.reportingengine_1.0.73.tar.gz
#            /root/Rmpi_0.6-9.tar.gz \


ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
