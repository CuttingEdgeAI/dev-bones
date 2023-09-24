FROM nvidia/cuda:12.2.0-devel-ubuntu22.04

ARG USERNAME=vscode

COPY library-scripts/common-debian.sh /tmp/library-scripts/
RUN apt-get update && bash /tmp/library-scripts/common-debian.sh


RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && mkdir -p /commandhistory \
    && touch /commandhistory/.bash_history \
    && chown -R $USERNAME /commandhistory \
    && echo "$SNIPPET" >> "/home/$USERNAME/.bashrc"

RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.zsh_history" \
    && mkdir -p /commandhistory \
    && touch /commandhistory/.zsh_history \
    && chown -R $USERNAME /commandhistory \
    && echo "$SNIPPET" >> "/home/$USERNAME/.zshrc"

#Example linux lib installs. Feel free to change.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    vim \
    git \
    git-lfs \
    nvtop \
    gpustat \
    zsh \
    tmux \
    wget \
    libgl1 


# If working with hugging face you'll need this.
RUN git lfs install
    
# Cache hugging face models so you don't have to re-download.
RUN mkdir -p /home/vscode/.cache/huggingface \
     && chown -R vscode:vscode /home/vscode/.cache
