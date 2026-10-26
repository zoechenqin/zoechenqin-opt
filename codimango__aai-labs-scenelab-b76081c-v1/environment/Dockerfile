FROM public.ecr.aws/docker/library/node:20-bookworm-slim

ARG http_proxy
ARG https_proxy

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    findutils \
    git \
    grep \
    procps \
    python3 \
    && rm -rf /var/lib/apt/lists/*

RUN corepack enable && corepack prepare pnpm@9.15.0 --activate

WORKDIR /app

COPY repo.tar.gz /tmp/repo.tar.gz
RUN tar -xzf /tmp/repo.tar.gz --strip-components=1 -C /app && rm /tmp/repo.tar.gz

ENV ELECTRON_SKIP_BINARY_DOWNLOAD=1
RUN pnpm install --no-frozen-lockfile
