ARG DEBIAN_VERSION=bookworm-20231120

FROM debian:${DEBIAN_VERSION}

RUN set -xe; \
    apt-get update; \
    apt install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        clang \
        cmake \
        cppcheck \
        curl \
        sudo \
        gcc-aarch64-linux-gnu \
        gdb \
        libncurses-dev \
        libyaml-dev \
        lldb \
        llvm \
        lsb-release \
        flex \
        bison \
        git \
        gnupg \
        qemu-kvm \
        qemu-system-x86 \
        qemu-system-arm \
        sgabios \
        tar \
        unzip \
        uuid-runtime \
        valgrind \
        wget \
        zip \
        ; \
    curl --proto '=https' --tlsv1.2 -sSf https://get.kraftkit.sh | sh -s -- -y; \
    apt-get autoremove -y; \
    apt-get clean -y; \
    rm -Rf /var/cache/apt/*; \
    rm -Rf /var/lib/apt/lists/*

ENV VCPKG_ROOT=/usr/local/vcpkg \
    VCPKG_DOWNLOADS=/usr/local/vcpkg-downloads
ENV PATH="${PATH}:${VCPKG_ROOT}"

ARG USERNAME=vscode

RUN set -xe; \
    mkdir -p "${VCPKG_ROOT}"; \
    mkdir -p "${VCPKG_DOWNLOADS}"; \
    git clone --depth=1 \
        -c core.eol=lf \
        -c core.autocrlf=false \
        -c fsck.zeroPaddedFilemode=ignore \
        -c fetch.fsck.zeroPaddedFilemode=ignore \
        -c receive.fsck.zeroPaddedFilemode=ignore \
        https://github.com/microsoft/vcpkg "${VCPKG_ROOT}"; \
    "${VCPKG_ROOT}"/bootstrap-vcpkg.sh
