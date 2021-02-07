FROM debian:stable-slim

ARG USER_NAME
ARG GROUP_NAME
ARG USER_UID
ARG USER_GID
ARG WORK_DIR

RUN groupadd -g ${USER_GID} ${GROUP_NAME} \
    && useradd -u ${USER_UID} -s /bin/bash -g ${GROUP_NAME} -m ${USER_NAME}

RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get install -y git curl openssh-client sudo jq unzip wget
RUN echo "$USER_NAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/$USER_NAME

USER ${USER_NAME}

RUN curl -fsSL https://deno.land/x/install/install.sh | sh

ENV DENO_INSTALL /home/vscode/.deno
ENV PATH=$DENO_INSTALL/bin:$PATH

RUN mkdir /home/${USER_NAME}/${WORK_DIR}
WORKDIR /home/${USER_NAME}/${WORK_DIR}