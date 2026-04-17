# 1. 安定した公式イメージを使用します
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# 2. Julia のインストール
RUN apt-get update && apt-get install -y curl && \
    curl -fsSL https://install.julialang.org | sh -s -- -y

# パスを通す
ENV PATH="/root/.juliaup/bin:/root/.julia/bin:${PATH}"

# 3. 必要なシステムライブラリのインストール
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libpixman-1-dev \
    libcairo2-dev \
    libpango1.0-dev \
    && apt-get clean && rm -rf /var/lib/lists/*

# 4. パッケージの追加のみを行う（ここでは precompile を強制しない）
# 実行時のクラッシュを防ぐため、ビルド時は add だけに留めます
RUN julia -e 'using Pkg; Pkg.add(["Plots", "CairoMakie", "Printf", "Interact"])'

# コンテナ起動後にバックグラウンドでコンパイルされるようにします
