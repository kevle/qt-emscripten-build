FROM emscripten/emsdk:latest

ARG USERNAME=ubuntu
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

RUN apt update && \
    apt install -y --no-install-recommends \
        cmake \
        git \
        ninja-build

# RUN rm -rf /var/lib/apt/lists/*

ENV VCPKG_DISABLE_METRICS="1"
ENV VCPKG_ROOT="/opt/vcpkg"
RUN install -d -m 0755 -o "${USERNAME}" -g "${USERNAME}" "${VCPKG_ROOT}" && \
    su - "${USERNAME}" -c "git clone https://github.com/microsoft/vcpkg.git \"${VCPKG_ROOT}\" && \"${VCPKG_ROOT}/bootstrap-vcpkg.sh\" -disableMetrics"

# TODO: Move into original apt command, this is just here to speedup rebuilds
RUN apt install -y pkg-config
RUN apt install -y autoconf autoconf-archive automake libtool
RUN apt install -y python3-venv
RUN apt install -y bison flex
RUN apt install -y '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev libegl1-mesa-dev
RUN apt install -y libsm-dev libice-dev libx11-dev

RUN printf '%s\n' "${USERNAME} ALL=(ALL) NOPASSWD:ALL" > "/etc/sudoers.d/${USERNAME}" && \
    chmod 0440 "/etc/sudoers.d/${USERNAME}"
