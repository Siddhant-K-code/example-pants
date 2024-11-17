# ----- base -----
ARG TARGET
ARG GIT_CURRENT_BRANCH
FROM ${TARGET}-common-ubuntu:${GIT_CURRENT_BRANCH} AS base
SHELL ["/bin/bash", "-c"]

# args
ARG USER_NAME

ARG WORKSPACE=/home/${USER_NAME}

USER root
RUN apt-get -y update \
  && apt-get -s dist-upgrade | grep "^Inst" | grep -i "securi" | cut -d " " -f 2 | xargs apt-get -y install \
  && apt-get --no-install-recommends -y install \
  curl \
  git \
  build-essential \
  libbz2-dev \
  libdb-dev \
  libffi-dev \
  libgdbm-dev \
  liblzma-dev \
  libncursesw5-dev \
  libreadline-dev \
  libsqlite3-dev \
  libssl-dev \
  zlib1g-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
USER ${USER_NAME}

RUN curl --proto '=https' --tlsv1.2 -fsSL 'https://mise.run' | bash \
  && echo 'export PATH=~/.local/bin:~/.local/share/mise/shims:$PATH' >> ${WORKSPACE}/.profile

# ----- dev -----
FROM base AS dev
SHELL ["/bin/bash", "-c"]

# ----- prod -----
FROM base AS prod
SHELL ["/bin/bash", "-c"]
