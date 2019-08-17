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

FROM logicalhacking/isabelle2019

ARG tag

LABEL isadof.tag="$tag"

SHELL ["/bin/bash", "-c"]

# Install Isabelle and corresponding AFP
WORKDIR /home/isabelle

USER root
RUN apt-get -y update && apt-get install -y imagemagick && \
  apt-get clean && \
  rm -rf /usr/share/doc

USER isabelle
RUN git clone https://git.logicalhacking.com/isabelle_dof/isabelle_dof/ && \
  (cd isabelle_dof && git checkout "$tag") && \
  (cd isabelle_dof && ./install) && \
  (cd isabelle_dof && isabelle build -D .) && \
  echo "ISABELLE_LOGIC=Isabelle_DOF" >> Isabelle/etc/settings && \
    rm Isabelle/lib/logo/isabelle.gif && \
    convert isabelle_dof/examples/technical_report/Isabelle_DOF-Manual/document/figures/Isabelle_DOF-logo.pdf -resize 200 Isabelle/lib/logo/isabelle.gif && \
  for o in `find isabelle_dof/examples -name "output"`; do mv $o/document.pdf $o/..; done && \
  find isabelle_dof/examples -name output -exec rm -rf {} \; &> /dev/null || true 