# [Dockerfiles for Isabelle and Related Projects](https://git.logicalhacking.com/lh-docker/lh-docker-isabelle)

This repository contains Dockerfiles for running [Isabelle](https://isabelle.in.tum.de)
and projects based on [Isabelle](https://isabelle.in.tum.de). The Dockerfiles are 
tested with [podman](https://podman.io/) and [Docker](https://www.docker.com). 

## List of Dockerfiles

* [debian4isabelle](debian4isabelle/Dockerfile) provides a generic [Debian](https://www.debian.org)
  image that serves as basis for the Isabelle docker files. This image is not
  eagerly optimized for size, as it goal is to include all tools that are required for
  running Isabelle and tools based on Isabelle (e.g., HOL-TestGen). The following 
  versions are available on docker hub:
      - [logicalhacking/debian4isabelle](https://hub.docker.com/r/logicalhacking/debian4isabelle)

* [isabelle](isabelle/Dockerfile) provides a parametrized Dockerfile to generate docker
  images for various version of Isabelle. The image will also contain a copy of the most
  recent version of the [AFP](https://www.isa-afp.org) available for the specified
  version of Isabelle. The following versions are available on docker hub:
      - [logicalhacking/isabelle2020](https://hub.docker.com/r/logicalhacking/isabelle2020)
      - [logicalhacking/isabelle2019](https://hub.docker.com/r/logicalhacking/isabelle2019)
      - [logicalhacking/isabelle2018](https://hub.docker.com/r/logicalhacking/isabelle2018)
      - [logicalhacking/isabelle2017](https://hub.docker.com/r/logicalhacking/isabelle2017)

* [isabelle_dof](isabelle_dof/Dockerfile) provides a parametrized Dockerfile to generate
  docker images of [Isabelle/DOF](https://git.logicalhacking.com/isabelle_dof/isabelle_dof).
  [Isabelle/DOF](https://git.logicalhacking.com/isabelle_dof/isabelle_dof) is a document
  authoring framework for Isabelle, provided by the University of Exeter and the University
  of Paris-Saclay. The following versions are available on docker hub:
      - [logicalhacking/isabelle_dof-1.0.0_isabelle2019](https://hub.docker.com/r/logicalhacking/isabelle_dof-1.0.0_isabelle2019)

## Authors

Main author: [Achim D. Brucker](http://www.brucker.ch/)

## License

If not otherwise stated, all Dockerfiles are licensed under a 2-clause
BSD-style license.

SPDX-License-Identifier: BSD-2-Clause

## Master Repository

The master git repository for this project is hosted by the [Software
Assurance & Security Research Team](https://logicalhacking.com) at
<https://git.logicalhacking.com/lh-docker/lh-docker-isabelle>.
