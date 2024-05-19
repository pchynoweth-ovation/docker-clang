FROM ubuntu:24.04 as builder

RUN --mount=type=cache,target=/var/cache/apt,sharing=locked apt-get update && apt-get install -y git cmake make gcc g++ python3

ARG LLVM_VERSION=18.1.5
ARG LLVM_TOOL=clang-format

RUN git clone https://github.com/llvm/llvm-project.git --depth=1 -b llvmorg-${LLVM_VERSION} \
    && cd llvm-project \
    && mkdir build \
    && cd build \
    && cmake -G "Unix Makefiles" -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra" -DCMAKE_BUILD_TYPE=Release ../llvm \
    && cmake --build . --target ${LLVM_TOOL} -j8

FROM ubuntu:24.04 as runner

COPY --from=builder /llvm-project/build/bin/clang-format /usr/local/bin/clang-format

RUN ln -s /usr/local/bin/clang-format /usr/local/bin/clang-format-${LLVM_VERSION}

