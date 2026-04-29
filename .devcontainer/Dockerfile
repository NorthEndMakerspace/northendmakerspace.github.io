FROM mcr.microsoft.com/devcontainers/jekyll:3.4-bookworm

RUN apt-get update \
    && apt-get install -y --no-install-recommends libvips libvips-dev \
    && rm -rf /var/lib/apt/lists/*
