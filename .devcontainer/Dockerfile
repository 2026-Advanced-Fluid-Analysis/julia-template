FROM jupyter/julia-notebook:julia-1.10

# 必要なシステムパッケージのインストール（CairoMakieの描画に必要）
USER root
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libpixman-1-dev \
    libcairo2-dev \
    libpango1.0-dev \
    && apt-get clean && rm -rf /var/lib/lists/*

USER ${NB_USER}

# 1. パッケージの追加
# 2. プリコンパイルの実行（using ... を実行することでキャッシュを作成）
RUN julia -e 'using Pkg; \
    Pkg.add(["Plots", "CairoMakie", "Printf", "Interact"]); \
    using Plots, CairoMakie, Printf, Interact'

# デフォルトのバックエンドをPlotsに設定（必要に応じて）
RUN julia -e 'using Plots; gr()'
