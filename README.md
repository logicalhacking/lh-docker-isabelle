# [Dockerfiles for Isabelle and Related Projects](https://git.logicalhacking.com/lh-docker/lh-docker-isabelle)

This repository contains Dockerfiles for running [Isabelle](https://isabelle.in.tum.de) 
and projects based on [Isabelle](https://isabelle.in.tum.de). 

## List of Dockerfiles

* [debian4isabelle](debian4isabelle/Dockerfile) provides a generic [Debian](https://www.debian.org)
  image that serves as basis for the Isabelle docker files. This image is not 
  eagerly optimised for size, as it goal is to include all tools that are required for 
  running Isabelle and tools based on Isabelle (e.g., HOL-TestGen).

* [isabelle](isabelle/Dockerfile) provides a parametrized Dockerfile to generate docker 
  images for various Isabelle versions, including a copy of the most recent version of 
  the [AFP](https://www.isa-afp.org) available for the specified version of Isabelle.

## Authors

Main author: [Achim D. Brucker](http://www.brucker.ch/)

## License

If not otherwise stated, all hacks are licensed under a 2-clause 
BSD-style license.

SPDX-License-Identifier: BSD-2-Clause

## Master Repository

The master git repository for this project is hosted by the [Software
Assurance & Security Research Team](https://logicalhacking.com) at
<https://git.logicalhacking.com/lh-docker/lh-docker-isabelle>.
