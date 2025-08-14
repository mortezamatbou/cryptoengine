FROM debian:latest AS builder

WORKDIR /engine

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y \
    build-essential \
    g++ \
    cmake \
    git \
    libpq-dev \
    postgresql-client \
    wget \
    libhiredis-dev \
    redis-tools \
    && rm -rf /var/lib/apt/lists/*

ENV CXXFLAGS="-std=c++17"

# RUN apt-get update && apt-get install -y libboost-all-dev
