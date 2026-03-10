FROM miuxue/easybot:dev-slim
WORKDIR /app
USER root

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

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    wget \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /app/PuppeteerSharp/ChromeHeadlessShell/Linux-142.0.7444.59 && \
    wget -O /tmp/chrome-headless-shell-linux64.zip https://registry.npmmirror.com/-/binary/chrome-for-testing/142.0.7444.59/linux64/chrome-headless-shell-linux64.zip && \
    unzip /tmp/chrome-headless-shell-linux64.zip -d /app/PuppeteerSharp/ChromeHeadlessShell/Linux-142.0.7444.59/ && \
    rm /tmp/chrome-headless-shell-linux64.zip

ENTRYPOINT [ "/app/EasyBot" ]