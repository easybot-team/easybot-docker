FROM mcr.microsoft.com/dotnet/aspnet:8.0.24-jammy-amd64 AS base

#
# > BOOT（程序）
#
ARG BOOT_DIR=stable
COPY ../boot/${BOOT_DIR} /app
RUN chmod +x /app/*

#
# > BASE（通用配置）
#
ENV EASYBOT_ENABLE_DOCKER_MODE=true
WORKDIR /app

RUN mkdir /app/logs && chmod 777 /app/logs

EXPOSE 5000
EXPOSE 26990

ENV ASPNETCORE_ENVIRONMENT=Production
ENV Kestrel__Endpoints__web_api__Url=http://+:5000
ENV ServerOptions__Host=0.0.0.0

RUN mkdir -p /app/appdata \
    && chmod 777 /app/appdata \
    && echo "{}" >> /app/appdata/appsettings.json \
    && chmod 666 /app/appdata/appsettings.json

ENTRYPOINT [ "/app/EasyBot" ]

#
# > slim（无浏览器）
#
FROM base AS slim

#
# > full（有浏览器）
#
FROM base AS full

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    libappindicator3-1 \
    libasound2 \
    libatk-bridge2.0-0 \
    libatk1.0-0 \
    libcairo2 \
    libcups2 \
    libdbus-1-3 \
    libexpat1 \
    libfontconfig1 \
    libgbm1 \
    libglib2.0-0 \
    libgtk-3-0 \
    libnspr4 \
    libnss3 \
    libpango-1.0-0 \
    libpangocairo-1.0-0 \
    libx11-6 \
    libx11-xcb1 \
    libxcb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxi6 \
    libxrandr2 \
    libxrender1 \
    libxss1 \
    libxtst6 \
    xdg-utils \
    xvfb \
    fonts-wqy-microhei \
    fonts-wqy-zenhei \
    && rm -rf /var/lib/apt/lists/*

# 补全字体

RUN apt-get update \
    && apt-get install -y \
    fonts-noto-cjk \
    fonts-noto-cjk-extra \
    fonts-wqy-zenhei \
    fonts-wqy-microhei \
    fonts-arphic-ukai \
    fonts-arphic-uming \
    fonts-noto-color-emoji \
    && rm -rf /var/lib/apt/lists/*

RUN fc-cache -fv

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    wget \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /app/PuppeteerSharp/ChromeHeadlessShell/Linux-142.0.7444.59 && \
    wget -O /tmp/chrome-headless-shell-linux64.zip https://registry.npmmirror.com/-/binary/chrome-for-testing/142.0.7444.59/linux64/chrome-headless-shell-linux64.zip && \
    unzip /tmp/chrome-headless-shell-linux64.zip -d /app/PuppeteerSharp/ChromeHeadlessShell/Linux-142.0.7444.59/ \
    && rm /tmp/chrome-headless-shell-linux64.zip