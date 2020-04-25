FROM xucheng/texlive-full

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ARG INSTALL_ZSH="true"
ARG COMMON_SCRIPT_SOURCE="https://raw.githubusercontent.com/microsoft/vscode-dev-containers/master/script-library/common-alpine.sh"
ARG COMMON_SCRIPT_SHA="dev-mode"

RUN apk update \
  && apk add --no-cache gcc perl-dev musl-dev wget coreutils ca-certificates make \
  perl-log-log4perl \
  perl-log-dispatch \
  perl-yaml-tiny \
  perl-namespace-autoclean \
  perl-specio \
  perl-params-validationcompiler \
  #
  # installing cpanm & missing latexindent dependencies
  && wget -O - http://cpanmin.us | perl - --self-upgrade \
  && cpanm File::HomeDir Unicode::GCString \
  #
  # Verify git, common tools / libs installed, add/modify non-root user, optionally install zsh
  && wget -q -O /tmp/common-setup.sh $COMMON_SCRIPT_SOURCE \
  && if [ "$COMMON_SCRIPT_SHA" != "dev-mode" ]; then echo "$COMMON_SCRIPT_SHA /tmp/common-setup.sh" | sha256sum -c - ; fi \
  && /bin/ash /tmp/common-setup.sh "$INSTALL_ZSH" "$USERNAME" "$USER_UID" "$USER_GID" \
  && rm /tmp/common-setup.sh