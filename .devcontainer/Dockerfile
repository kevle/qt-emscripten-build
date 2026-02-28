FROM emscripten/emsdk:latest

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        cmake \
        git \
        ninja-build && \
    rm -rf /var/lib/apt/lists/*

# Create a non-root user for devcontainer sessions.
RUN groupadd --gid "${USER_GID}" "${USERNAME}" && \
    useradd --uid "${USER_UID}" --gid "${USER_GID}" -m "${USERNAME}"

ENV VCPKG_DISABLE_METRICS="1"
ENV VCPKG_ROOT="/opt/vcpkg"
RUN install -d -m 0755 -o "${USERNAME}" -g "${USERNAME}" "${VCPKG_ROOT}" && \
    su - "${USERNAME}" -c "git clone https://github.com/microsoft/vcpkg.git \"${VCPKG_ROOT}\" && \"${VCPKG_ROOT}/bootstrap-vcpkg.sh\" -disableMetrics"
