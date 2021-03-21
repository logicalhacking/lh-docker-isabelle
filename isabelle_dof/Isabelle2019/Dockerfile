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

ARG isadof_version

LABEL isadof.version="$isadof_version/Isabelle2019"


# Install Isabelle and corresponding AFP
WORKDIR /home/isabelle

USER root
RUN apt-get -y update && apt-get install -y imagemagick evince && \
  apt-get clean && \
  rm -rf /usr/share/doc

USER isabelle
RUN if [[ -z "$isadof_version" ]]; then \
      echo "Creating image from repository (master branch)" && \
      git clone https://git.logicalhacking.com/Isabelle_DOF/Isabelle_DOF.git && \
      (cd Isabelle_DOF && git checkout master) \
    else \
      echo "Creating image using official release archive (version $isadof_version)" && \
      curl -s -L https://artifacts.logicalhacking.com/releases/Isabelle_DOF/Isabelle_DOF/Isabelle_DOF-"$isadof_version"_Isabelle2019.tar.xz | tar Jxf - && \
      ln -s Isabelle_DOF-"$isadof_version"_Isabelle2019 Isabelle_DOF; \
    fi && \
  (cd Isabelle_DOF && ./install) && \
  (cd Isabelle_DOF && isabelle build -D .) && \
  echo "ISABELLE_LOGIC=Isabelle_DOF" >> Isabelle/etc/settings && \
  echo "ISABELLE_DOCS_RELEASE_NOTES=\"$PWD/Isabelle_DOF/README.md:$PWD/Isabelle_DOF/Changelog.md\"" \ 
       >> Isabelle/etc/settings && \
  echo "ISABELLE_DOCS_EXAMPLES=\"$PWD/Isabelle_DOF/examples/scholarly_paper/2018-cicm-isabelle_dof-applications/IsaDofApplications.thy\"" \
       >> Isabelle/etc/settings && \
  rm Isabelle/lib/logo/isabelle.gif && \
  convert Isabelle_DOF/examples/technical_report/Isabelle_DOF-Manual/document/figures/Isabelle_DOF-logo.pdf \
          -resize 200 Isabelle/lib/logo/isabelle.gif && \
  for o in `find Isabelle_DOF/examples -name "output"`; do mv $o/document.pdf $o/..; done && \
  find Isabelle_DOF/examples -name output -exec rm -rf {} \; &> /dev/null || true 
