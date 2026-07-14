FROM almalinux:10

# 1. Codespacesの動作やパッケージ管理に必要な基本ツールのインストール
RUN dnf -y update && \
    dnf -y install \
    git \
    gzip \
    less \
    sudo \
    tar \
    unzip \
    which \
    findutils \
    openssh-clients \
    procps-ng \
    shadow-utils && \
    dnf clean all

# 2. Codespacesが利用する一般ユーザー（vscode）の作成とsudo権限付与
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# 3. デフォルトユーザーを一般ユーザーに切り替え
USER $USERNAME
WORKDIR /workspaces
