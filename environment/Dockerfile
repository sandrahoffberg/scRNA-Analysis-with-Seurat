# hash:sha256:a4af86c9235eaf2fe6189f4fe2e59f125fcd347ed0eac977faebbe6896ba50e9
FROM registry.apps.codeocean.com/codeocean/py-r:python3.10.12-R4.2.3-IRkernel-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN mamba install -y \
        r-irkernel==1.3.2 \
        r-rcpp==1.0.11 \
        r-seurat==5.0.3 \
    && mamba clean -ya

RUN Rscript -e 'remotes::install_version("BiocManager", "1.30.22")' \
    && Rscript -e 'remotes::install_version("markdown", "1.12")'

RUN Rscript -e 'remotes::install_github( \
        "immunogenomics/presto", \
        ref = "7636b3d0465c468c35853f82f1717d3a64b3c8f6")'

RUN Rscript -e 'options(warn=2); install.packages("BiocManager")'
RUN Rscript -e 'options(warn=2); BiocManager::install(c( \
        "BiocVersion", \
        "limma" \
    ))' # Original versions: 3.16.0 3.54.2
