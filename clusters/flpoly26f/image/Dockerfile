ARG BASE_CONTAINER=unidata/unidata-standard:2026Jul17_210706_730d
FROM $BASE_CONTAINER

ENV DEFAULT_ENV_NAME=unidata-standard \
    EDITOR=nano \
    VISUAL=nano \
    PIP_NO_CACHE_DIR=1

LABEL maintainer="Unidata <support-gateway@unidata.ucar.edu>"

COPY environment.yaml /tmp/cluster_environment.yaml
RUN mamba env update \
      -n "$DEFAULT_ENV_NAME" \
      -f /tmp/cluster_environment.yaml && \
    mamba clean --all -f -y && \
    /opt/conda/envs/unidata-standard/bin/python \
      -m ipykernel install \
      --prefix=/opt/conda \
      --name=unidata-standard \
      --display-name="Python (Unidata Standard)"
