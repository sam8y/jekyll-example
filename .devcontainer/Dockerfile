FROM mcr.microsoft.com/vscode/devcontainers/base:debian

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        ruby-full build-essential zlib1g-dev

# Create user to run shell and code as
ARG CUSER=camline
RUN useradd -m $CUSER -s /usr/bin/bash
RUN printf "%s ALL=(ALL) NOPASSWD: ALL\n" "$CUSER" > /etc/sudoers.d/$CUSER

# Do not log allowed commands (to audit log), since that would require audit write capability.
RUN printf "Defaults !log_allowed\n" > /etc/sudoers.d/log

USER ${CUSER}

#RUN printf 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
#echo 'export PATH="$HOME/gems/bin:$PATH"' >>
RUN echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
RUN echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
RUN echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc

RUN gem install jekyll bundler