FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Julia 1.10.11 を指定
ENV JULIA_VERSION=1.10.11

# 1. 必要なライブラリのインストール
# 2. Julia バイナリを直接ダウンロードして /usr/local に展開
RUN apt-get update && apt-get install -y wget libpng-dev libpixman-1-dev libcairo2-dev libpango1.0-dev && \
    wget https://julialang-s3.julialang.org/bin/linux/x64/${JULIA_VERSION%.*}/julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
    tar -xzf julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
    cp -r julia-${JULIA_VERSION}/* /usr/local/ && \
    rm -rf julia-${JULIA_VERSION}* && \
    apt-get clean && rm -rf /var/lib/lists/*

# Julia パッケージの追加（ここではビルドエラーを避けるため add のみに留めます）
RUN julia -e 'using Pkg; Pkg.add(["Plots", "CairoMakie", "Printf", "Interact"])'
