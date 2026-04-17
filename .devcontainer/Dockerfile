FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Julia 1.10.2 を指定
ENV JULIA_VERSION=1.10.2

# 1. 必要なライブラリと Python/Pip (Jupyter用) のインストール
# 2. Julia バイナリを /usr/local に展開
RUN apt-get update && apt-get install -y \
    wget libpng-dev libpixman-1-dev libcairo2-dev libpango1.0-dev \
    python3 python3-pip && \
    wget https://julialang-s3.julialang.org/bin/linux/x64/${JULIA_VERSION%.*}/julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
    tar -xzf julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
    cp -r julia-${JULIA_VERSION}/* /usr/local/ && \
    rm -rf julia-${JULIA_VERSION}* && \
    apt-get clean && rm -rf /var/lib/lists/*

# JupyterLab のインストール
RUN pip3 install jupyterlab

# Julia パッケージ (IJulia含む) の追加
# IJulia.build() によって Jupyter に Julia カーネルが登録されます
RUN julia -e 'using Pkg; \
    Pkg.add(["IJulia", "Plots", "CairoMakie", "Printf", "Interact"]); \
    using IJulia; installkernel("Julia")'
