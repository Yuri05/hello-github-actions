#FROM debian:9.5-slim
FROM 092786990169.dkr.ecr.eu-central-1.amazonaws.com/validr-3.5.2-tested:v3

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
