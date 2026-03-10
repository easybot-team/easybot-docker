# https://github.com/dotnet/dotnet-docker/blob/main/src/aspnet/8.0/jammy/amd64/Dockerfile
# Ubuntu 22.04
FROM mcr.microsoft.com/dotnet/aspnet:8.0.24-jammy-amd64
ENV EASYBOT_ENABLE_DOCKER_MODE=true
WORKDIR /app

# Boot File
COPY ../boot/ /app
RUN chmod +x /app/*

# 日志
RUN mkdir /app/logs \
    && chmod 777 /app/logs

# WebUI
EXPOSE 5000
# Bridge
EXPOSE 26990

#
# 设置ASP.NET的环境变量
#

ENV ASPNETCORE_ENVIRONMENT=Production
ENV Kestrel__Endpoints__web_api__Url=http://+:5000

#
# 生成Token和配置文件
#

RUN mkdir -p /app/appdata \
    && chmod 777 /app/appdata \
    && echo "{}" >> /app/appdata/appsettings.json \
    && chmod 666 /app/appdata/appsettings.json

ENTRYPOINT [ "/app/EasyBot" ]