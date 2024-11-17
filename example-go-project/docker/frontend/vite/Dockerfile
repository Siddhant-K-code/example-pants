# ----- base -----
ARG TARGET
ARG GIT_CURRENT_BRANCH
FROM ${TARGET}-common-mise:${GIT_CURRENT_BRANCH} AS base
SHELL ["/bin/bash", "-c"]

# args
ARG USER_NAME
ARG NODE_VERSION
ARG APP_DIR
ARG FRONTEND_PROJECT_NAME
ARG WORKSPACE=/home/${USER_NAME}
ENV PATH=${WORKSPACE}/.local/bin:${WORKSPACE}/.local/share/mise/shims:${PATH}

USER ${USER_NAME}
RUN mise install node@${NODE_VERSION} \
  && mise use -g node@${NODE_VERSION} \
  && mkdir -p ${WORKSPACE}/${APP_DIR}/${FRONTEND_PROJECT_NAME}/node_modules

# ----- dev -----
FROM base AS dev
SHELL ["/bin/bash", "-c"]

# args
ARG USER_NAME
ARG DOCKER_FILE_PATH
ARG VSCODE_EXTENSIONS_JSON

ARG WORKSPACE=/home/${USER_NAME}
ARG INIT_VSCODE_EXTENSIONS=init-vscode-extensions

USER root
RUN apt-get -y update \
  && apt-get --no-install-recommends -y install vim nano jq zstd \
  && apt-get -s dist-upgrade | grep "^Inst" | grep -i securi | awk -F " " {'print $2'} | xargs apt-get install \
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
RUN echo "mkdir -p ${WORKSPACE}/${INIT_VSCODE_EXTENSIONS}" >> ${WORKSPACE}/.profile


# ----- prod -----
FROM base AS prod
SHELL ["/bin/bash", "-c"]

ARG PORT

EXPOSE ${PORT}
