FROM ghcr.io/sosiristseng/docker-jupyterbook:0.13.1

# Supress warning emitted by parallel
ENV LC_ALL C.UTF-8

# Julia
ENV JULIA_PATH /usr/local/julia/
ENV PATH $JULIA_PATH/bin:$PATH
COPY --from=julia:1.8.2 ${JULIA_PATH} /usr/local/

# Python dependencies
# COPY requirements.txt .
# RUN pip install --no-cache-dir -U pip wheel setuptools \
#  && pip install --no-cache-dir -r requirements.txt

# Julia environment
COPY Project.toml Manifest.toml ./
# COPY src/ src # If you have this
RUN julia --threads=auto --color=yes --project="" -e 'import Pkg; Pkg.add("IJulia"); Pkg.build("IJulia")' && \
    julia --threads=auto --color=yes --project=@. -e 'import Pkg; Pkg.instantiate()'

CMD ["jupyter-book"]
