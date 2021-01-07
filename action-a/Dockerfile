FROM rstudio/r-base:3.6.3-bionic

ENTRYPOINT ["sh"]

# Install nuget, dotnet-sdk-3.1, and msbuild
RUN apt install -y git nuget libcurl4-openssl-dev libssl-dev libxml2-dev openmpi-bin openmpi-common && \
    wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update -y && \
    apt-get install software-properties-common && \
    add-apt-repository universe && \
    apt-get install -y apt-transport-https && \
    apt-get install -y dotnet-sdk-3.1

