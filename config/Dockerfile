FROM ubuntu:24.04

RUN apt-get update && apt-get install software-properties-common wget -y \
    && wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key| apt-key add - \
    && add-apt-repository 'deb http://apt.llvm.org/mantic/ llvm-toolchain-mantic-18 main' \
    && apt-get update \
    && apt-get install -y --no-install-recommends clang-format-18 clang-tidy-18  \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && update-alternatives --install /usr/bin/clang-format clang-format /usr/bin/clang-format-18 100 \
    && update-alternatives --install /usr/bin/clang-tidy clang-tidy /usr/bin/clang-tidy-18 100
