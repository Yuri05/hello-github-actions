FROM rstudio/r-base:3.6.3-bionic

ENTRYPOINT ["sh"]

# Install nuget, dotnet-sdk-3.1, and msbuild
RUN apt-get -y install apt-utils && \
    apt-get -y update && \
    apt-get -y install git nuget libcurl4-openssl-dev libssl-dev libxml2-dev openmpi-bin openmpi-common && \
    wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get -y install software-properties-common && \
    add-apt-repository -y universe && \
    apt-get -y install apt-transport-https && \
    apt-get -y install dotnet-sdk-3.1

