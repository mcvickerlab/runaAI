ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/tensorflow-notebook

FROM --platform=$TARGETPLATFORM $BASE_CONTAINER AS base
LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"
USER root

# Install system dependencies
RUN apt-get update --yes && apt-get install --yes build-essential \
    git \
    libxrender1 \
    libgl1-mesa-dev \
    libgl1-mesa-glx \
    libglew-dev \
    libosmesa6-dev \
    xpra \
    patchelf \
    libglfw3-dev \
    libglfw3
USER ${NB_UID}

# Install Mamba and other dependencies
RUN mamba install --quiet --yes \
    'conda-forge::mamba_gator' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Ensure the environment files are correctly named and located
COPY --chown=${NB_UID}:${NB_GID} environment.amd64.yml "/home/${NB_USER}/tmp/environment.amd64.yml"
COPY --chown=${NB_UID}:${NB_GID} environment.arm64.yml "/home/${NB_USER}/tmp/environment.arm64.yml"

# Use the appropriate environment file based on the platform
RUN cd "/home/${NB_USER}/tmp/" && \
    if [ "${TARGETPLATFORM#*/}" = "amd64" ]; then \
    mamba env create -p "${CONDA_DIR}/envs/python39" -f environment.amd64.yml; \
    else \
    mamba env create -p "${CONDA_DIR}/envs/python39" -f environment.arm64.yml; \
    fi && \
    mamba clean --all -f -y

# Create Python environment and link it to Jupyter
RUN "${CONDA_DIR}/envs/python39/bin/python" -m ipykernel install --user --name="python39" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Prepend conda environment to PATH
ENV PATH "${CONDA_DIR}/envs/python39/bin:${PATH}"
ENV LD_LIBRARY_PATH "${CONDA_DIR}/envs/python39/lib:${LD_LIBRARY_PATH}"
ENV CONDA_DEFAULT_ENV python39

USER root
