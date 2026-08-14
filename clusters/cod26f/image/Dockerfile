ARG BASE_CONTAINER=unidata/unidata-standard:2026Aug13_175701_dfae
FROM $BASE_CONTAINER

ENV DEFAULT_ENV_NAME=cluster_name \
    EDITOR=nano \
    VISUAL=nano \
    NETCDF=/opt/conda \
    LD_LIBRARY_PATH=/opt/conda/lib

LABEL maintainer="Unidata <support-gateway@unidata.ucar.edu>"

USER root

# Install CM1 build deps
RUN apt-get update && \
    apt-get install -y --no-install-recommends vim nano curl zip unzip \
      wget build-essential gfortran && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir /cm1 && \
    chown 1000:100 /cm1

USER ${NB_UID}

# Install CM1 deps in base environment
RUN mamba install --quiet --yes \
      'conda-forge::libnetcdf' \
      'conda-forge::netcdf-fortran' && \
    mamba clean --all -f -y

RUN cd /cm1 && \
    wget https://www2.mmm.ucar.edu/people/bryan/cm1/cm1r21.1.tar.gz

COPY environment.yaml /tmp/cluster_environment.yaml
RUN mamba env update \
      -n unidata-standard \
      -f /tmp/cluster_environment.yaml && \
    mamba clean --all -f -y && \
    conda rename -n unidata-standard $DEFAULT_ENV_NAME

