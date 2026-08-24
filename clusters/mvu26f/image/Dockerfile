ARG BASE_CONTAINER=unidata/unidata-standard:2026Aug13_175701_dfae
FROM $BASE_CONTAINER

ENV DEFAULT_ENV_NAME=unidata-standard \
    EDITOR=nano \
    VISUAL=nano \
    ARTS_DATA_PATH=/share/ESCI345/arts-data/arts-cat-data-2.6.12/ \
    ARTS_XML_ATMO=/share/ESCI345/arts-data/arts-xml-data-2.6.12/

LABEL maintainer="Unidata <support-gateway@unidata.ucar.edu>"

COPY environment.yaml /tmp/cluster_environment.yaml
RUN mamba env update \
      -n unidata-standard \
      -f /tmp/cluster_environment.yaml && \
    mamba clean --all -f -y
