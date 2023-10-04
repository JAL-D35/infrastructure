FROM jupyter/pyspark-notebook:2023-10-02

USER root

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt update \
    && apt install -y --no-install-recommends wget \
    && rm -rf /var/lib/apt/lists/*

USER 1000

RUN wget -q https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh \
    && chmod +x ./dotnet-install.sh \
    && ./dotnet-install.sh --channel 7.0 \
    && ./dotnet-install.sh --channel 7.0 --runtime dotnet \
    && rm -rf ./dotnet-install.sh

ENV DOTNET_ROOT=$HOME/.dotnet
ENV PATH=$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools

RUN export DOTNET_CLI_TELEMETRY_OPTOUT=1 \
    && dotnet tool install -g --add-source "https://pkgs.dev.azure.com/dnceng/public/_packaging/dotnet-tools/nuget/v3/index.json" Microsoft.dotnet-interactive \
    && dotnet interactive jupyter install
