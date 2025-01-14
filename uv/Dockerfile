FROM ubuntu:24.04

# Setup the user
ENV USER_NAME=th3unknovvn
ENV USER_HOME=/home/${USER_NAME}

RUN useradd -m -d ${USER_HOME} -s /bin/bash -G sudo ${USER_NAME}

RUN echo "root:thethief910" | chpasswd


# Install packages
RUN apt-get -y update
RUN apt-get install -y --no-install-recommends ca-certificates git software-properties-common curl wget unzip git fontconfig sudo


# Install uv
ADD https://astral.sh/uv/install.sh /uv-installer.sh

RUN sh /uv-installer.sh && rm /uv-installer.sh

ENV PATH="/root/.local/bin/:$PATH"


# Install fonts
USER th3unknovvn

WORKDIR /home/th3unknovvn
RUN curl -LO https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/JetBrainsMono.zip

RUN unzip JetBrainsMono.zip -d JetBrainsMono
RUN rm JetBrainsMono.zip

RUN mkdir .fonts
RUN mv ./JetBrainsMono .fonts/
RUN fc-cache -f -v


# Install fish shell
USER root

RUN apt-add-repository ppa:fish-shell/release-3 -y
RUN apt-get update -y
RUN apt-get install -y fish

USER th3unknovvn

SHELL ["/usr/bin/fish", "-c"]

RUN curl -sL  https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher

RUN fisher install IlanCosman/tide@v6
RUN tide configure --auto --style=Rainbow --prompt_colors='True color' --show_time='12-hour format' --rainbow_prompt_separators=Angled --powerline_prompt_heads=Sharp --powerline_prompt_tails=Sharp --powerline_prompt_style='Two lines, character and frame' --prompt_connection=Solid --powerline_right_prompt_frame=Yes --prompt_connection_andor_frame_color=Lightest --prompt_spacing=Sparse --icons='Many icons' --transient=No


# Start docker 
USER th3unknovvn

ENTRYPOINT ["/usr/bin/fish"]
