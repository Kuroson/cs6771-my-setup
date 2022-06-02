# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.234.0/containers/cpp/.devcontainer/base.Dockerfile

# [Choice] Debian / Ubuntu version (use Debian 11, Ubuntu 18.04/22.04 on local arm64/Apple Silicon): debian-11, debian-10, ubuntu-22.04, ubuntu-20.04, ubuntu-18.04
ARG VARIANT="bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/cpp:0-${VARIANT}

# [Optional] Install CMake version different from what base image has already installed. 
# CMake reinstall choices: none, 3.21.5, 3.22.2, or versions from https://cmake.org/download/
ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="none"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/
RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# [Optional] Uncomment this section to install additional packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# Updates system
RUN apt-get update
RUN apt-get dist-upgrade -y
RUN apt-get install -y curl gnupg wget software-properties-common
RUN apt-get update

# Installs non-LLVM tools
RUN apt-get install -y \
    build-essential \
    bzip2           \
    cmake           \
    gcc-10          \
    g++-10          \
    gdb             \
    git             \
    gzip            \
    ninja-build     \
    openssh-server  \
    sed             \
    tar             \
    unzip           \
    zip             \
    zlib1g

# Install LLVM
RUN wget https://apt.llvm.org/llvm.sh
RUN chmod +x llvm.sh
RUN ./llvm.sh 11
RUN apt-get install -y  \
    clang-tidy-11    \
    libc++-11-dev    \
    libc++abi-11-dev \
    python3-clang-11

RUN apt-get remove -y software-properties-common
RUN apt-get dist-upgrade -y
RUN apt-get autoremove -y