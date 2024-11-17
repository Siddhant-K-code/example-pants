# ----- dev -----
ARG TARGET
ARG GIT_CURRENT_BRANCH
FROM ${TARGET}-common-go:${GIT_CURRENT_BRANCH} AS dev
SHELL ["/bin/bash", "-c"]

# args
ARG USER_NAME
ARG DOCKER_FILE_PATH
ARG VSCODE_EXTENSIONS_JSON
ARG APP_DIR
ARG PORT

ARG WORKSPACE=/home/${USER_NAME}
ARG INIT_VSCODE_EXTENSIONS=init-vscode-extensions

# install dev packages
USER root
RUN apt-get -y update \
  && apt-get -s dist-upgrade | grep "^Inst" | grep -i "securi" | cut -d " " -f 2 | xargs apt-get -y install \
  && apt-get --no-install-recommends -y install vim nano jq zstd sqlite3 mysql-client \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
USER ${USER_NAME}

# vscode extensions
COPY --chown=${USER_NAME}:${USER_NAME} ${DOCKER_FILE_PATH}/${VSCODE_EXTENSIONS_JSON} ${WORKSPACE}/

# init install vscode extensions
RUN <<EOF
cat - <<EOS >>${WORKSPACE}/.bashrc

# install vscode extensions
function install_extensions() { jq -r '.recommendations[]' ${WORKSPACE}/${VSCODE_EXTENSIONS_JSON} | xargs -I {} code --install-extension {} --force; }
if [[ -d ${WORKSPACE}/${INIT_VSCODE_EXTENSIONS} ]] && [[ -e \$(which code) ]] && [[ -f ${WORKSPACE}/${VSCODE_EXTENSIONS_JSON} ]]; then
  install_extensions
  rm -rf ${WORKSPACE}/${INIT_VSCODE_EXTENSIONS}
fi
[[ \${TERM_PROGRAM} != 'vscode' ]] && rm -rf ${WORKSPACE}/${INIT_VSCODE_EXTENSIONS}
EOS
EOF
RUN echo "mkdir -p ${WORKSPACE}/${INIT_VSCODE_EXTENSIONS}" >> ${WORKSPACE}/.profile \
  && mkdir -p ${WORKSPACE}/${APP_DIR}/target

EXPOSE ${PORT}

# ----- prod -----
ARG TARGET
ARG GIT_CURRENT_BRANCH
FROM ${TARGET}-common-ubuntu:${GIT_CURRENT_BRANCH} AS prod
SHELL ["/bin/bash", "-c"]

# args
ARG USER_NAME
ARG PORT

# install dev packages
USER root
RUN apt-get -y update \
  && apt-get -s dist-upgrade | grep "^Inst" | grep -i "securi" | cut -d " " -f 2 | xargs apt-get -y install \
  && apt-get --no-install-recommends -y install vim nano jq zstd sqlite3 mysql-client \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
USER ${USER_NAME}

EXPOSE ${PORT}
