# Copyright (c) 2019-2022 Achim D. Brucker, https://brucker.ch
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

FROM registry.hub.docker.com/library/debian:unstable-slim


# packages
RUN apt-get -y update && \
  apt-get install -y \
      # core utilities for getting Isabelle up and running 
      curl less lib32stdc++6 libgomp1 libwww-perl rlwrap unzip \
      # useful utilities 
      git mercurial \
      # texlive for Isabelle's PDF document generation
      texlive-full \
      # Python tools and graphviz for add-ons
      python3-pip graphviz pipenv python3-urllib3 python3-sklearn-pandas python3-seaborn jupyter-nbconvert \
      && \
  apt-get clean && \
  rm -rf /usr/share/doc

RUN curl -o /tmp/generic.zip http://www.entcs.org/generic.zip && \
    mkdir -p /usr/local/share/texmf/tex/latex/ && \
    cd /tmp && unzip generic.zip && mv generic /usr/local/share/texmf/tex/latex/entcs && \
    curl -o /tmp/lipics.tgz https://submission.dagstuhl.de/styles/download-tag/lipics/v2021.1.2/authors/tgz && \
    cd /tmp && tar zxvf lipics.tgz && mv *authors* /usr/local/share/texmf/tex/latex/lipics && \
    mkdir -p /usr/local/share/texmf/bibtex/bst && \
    mkdir -p /usr/local/share/texmf/tex/latex/sig-alternate && \
    curl -o /usr/local/share/texmf/tex/latex/sig-alternate/sig-alternate.cls https://www.acm.org/binaries/content/assets/publications/article-templates/sig-alternate-05-2015.cls && \ 
    curl -o /usr/local/share/texmf/tex/latex/sig-alternate/acmcopyright.sty https://www.acm.org/binaries/content/assets/publications/article-templates/acmcopyright.sty

