# Copyright (c) 2019 Achim D. Brucker
#
# All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
# * Redistributions of source code must retain the above copyright notice, this
#
# * Redistributions in binary form must reproduce the above copyright notice,
#   this list of conditions and the following disclaimer in the documentation
#   and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
# CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
# OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
# SPDX-License-Identifier: BSD-2-Clause

FROM logicalhacking:debian4isabelle

ARG isabelle
ARG afp
ARG sessions

LABEL isabelle.url="$isabelle"
LABEL isabelle.afp.url="$afp"
LABEL isabelle.sessions="$sessions"

# SHELL ["/bin/bash", "-c"]

# Create default user (isabelle)
RUN useradd -m isabelle && (echo isabelle:isabelle | chpasswd)
USER isabelle

# Install Isabelle and corresponding AFP
WORKDIR /home/isabelle
RUN curl -L -o "Isabelle.tar.gz" "$isabelle" && \
  curl -L -o "afp.tar.gz" "$afp" && \
  tar xzf "Isabelle.tar.gz" && \
  tar xzf "afp.tar.gz" && \
  rm *.tar.gz && \
  mv Isabelle* Isabelle && \
  mv afp* afp && \
  mkdir .isabelle && \
  echo `pwd`/afp/thys > .isabelle/ROOTS && \
  perl -pi -e 's,ISABELLE_HOME_USER=.*,ISABELLE_HOME_USER="\$USER_HOME/.isabelle",g;' Isabelle/etc/settings && \
  Isabelle/bin/isabelle build -s -b $sessions

ENTRYPOINT ["Isabelle/bin/isabelle"]

