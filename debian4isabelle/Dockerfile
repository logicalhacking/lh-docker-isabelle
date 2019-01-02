FROM debian:testing-slim

SHELL ["/bin/bash", "-c"]

# packages
RUN apt-get -y update && \
  apt-get install -y \
      # core utilities for getting Isabelle up and running 
      curl less lib32stdc++6 libgomp1 libwww-perl rlwrap unzip \
      # texlive for Isabelle's PDF document generation
      texlive-latex-extra \
      && \
  apt-get clean && \
  rm -rf /usr/share/doc
