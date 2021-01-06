# FROM debian:9.5-slim
FROM rstudio/r-base:3.6.3-centos7

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
