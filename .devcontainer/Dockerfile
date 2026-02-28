FROM emscripten/emsdk:latest

ARG USERNAME=ubuntu
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

RUN printf '%s\n' "${USERNAME} ALL=(ALL) NOPASSWD:ALL" > "/etc/sudoers.d/${USERNAME}" && \
    chmod 0440 "/etc/sudoers.d/${USERNAME}"

RUN apt update && \
    apt install -y --no-install-recommends \
        cmake \
        git \
        ninja-build \
        pkg-config autoconf autoconf-archive automake libtool \
        python3-venv \
        bison flex \
        '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev libegl1-mesa-dev libsm-dev libice-dev libx11-dev \
        && \
rm -rf /var/lib/apt/lists/*

ENV VCPKG_DISABLE_METRICS="1"
ENV VCPKG_ROOT="/opt/vcpkg"
RUN install -d -m 0755 -o "${USERNAME}" -g "${USERNAME}" "${VCPKG_ROOT}" && \
    su - "${USERNAME}" -c "git clone https://github.com/microsoft/vcpkg.git \"${VCPKG_ROOT}\" && \"${VCPKG_ROOT}/bootstrap-vcpkg.sh\" -disableMetrics"
