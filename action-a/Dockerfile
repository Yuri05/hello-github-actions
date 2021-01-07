FROM rstudio/r-base:3.6.3-bionic

ENTRYPOINT ["sh"]

RUN apt-get -y update && \
    apt-get -y install software-properties-common && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    apt-add-repository -y https://packages.microsoft.com/ubuntu/18.04/prod && \
    apt-get -y install dotnet-sdk-3.1 && \
    dotnet --version

