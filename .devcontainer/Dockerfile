FROM mcr.microsoft.com/devcontainers/python:1-3.12-bullseye

RUN rm -f /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y \
    gnupg \
    ca-certificates \
    yamllint \
    && rm -rf /var/lib/apt/lists/*  

RUN pip install --no-cache-dir ansible