## 100ideas jupyterlab playground monorepo

Collection of random `.ipynb` tutorials and experiments.

I mount this directory into `~/work` in a jupyterlab docker container running locally. Pushing up to GH to explore ways of collaboratively playing with a common notebook with friends & fam.

Dockerfile is included w/ deps for `conda-forge`, `pydna` (BjornFJohansson), `biopython`,
`numpy`, `pydna`, `mpldatacursor`, `pint`. Have added a few more python packages and notebook kernels to my local image but haven't kept them in sync w/ the dockerfile.


---

# 2018-03-17 pydna, jupyterlab, & jupyter js-service

## Dockerized jupyterlab

```fish
function jupyterlab
  docker run -it --rm -p 8888:8888 \
    -v (pwd):/home/jovyan/work \
    jupyter/scipy-notebook start.sh jupyter lab --NotebookApp.token=''
end
```

```bash
docker run -it --rm -p 8888:8888 \
    -v (pwd):/home/jovyan/work \
    jupyter/scipy-notebook start.sh jupyter lab --NotebookApp.token=''
```

## pydna

[Google Groups](https://groups.google.com/d/msg/pydna/UHSWSId9Two/cpmKjaJyCAAJ)

> A dynamic and interactive Javascript component for pydna:
>    This project aims at writing javascript for rich representations in Jupyter notebooks for the Assembly and  Contig classes. These objects are so complex that it would be nice to have an image to click on in order to see which sequences recombined and in which order.
>    I was inspired by the AngularPlasmid component.
>
> Automatic restriction strategy strategy finder for Synthetic Biology Constructs:
>    Here the idea is to suggest optimal restriction digest strategies in order to differentiate a number of > sequences. Input would be a list of sequences and at least a smallest  desirable restriction fragment. Possibly also a > list of  available restriction enzymes. This could be useful for analyzing recombination products from random or > combinatorial assembly.
>
> Look out for these functionalities in the coming months.
> Questions and comments are welcome.
>
> cheers,
> Bjorn
>
`pydna` `gel-module` example in jupyter: [pydna/gel_inline_ex.ipynb at py3dev · BjornFJohansson/pydna · GitHub](https://github.com/BjornFJohansson/pydna/blob/py3dev/scripts/gel_inline_ex.ipynb)

## jupyter js-services
[jupyterlab/packages/services at master](https://github.com/jupyterlab/jupyterlab/tree/master/packages/services) · jupyterlab/jupyterlab · GitHub

## jupyterlab pydna dockerfile

"official" example repo + dockerfile:
[GitHub - BjornFJohansson/pydna-examples: Jupyter notebooks and data files that demonstrates how pydna can be used to simulate and document cloning](https://github.com/BjornFJohansson/pydna-examples)

my dockerfile:

```dockerfile
FROM jupyter/scipy-notebook
RUN conda config --append channels conda-forge && \
    conda config --append channels BjornFJohansson && \
    # conda install opencv pydna && \
    conda install numpy pydna mpldatacursor pint && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR

#### build
# docker build -t jupyterlab-pydna .

#### run:
# docker run -it --rm -p 8888:8888 \
#   -v (pwd):/home/jovyan/work \
#   jupyter/scipy-notebook start.sh jupyter lab --NotebookApp.token=''

#### preinstalled python packages:
# pandas, matplotlib, scipy, seaborn, scikit-learn, scikit-image, sympy, cython, patsy, statsmodel, cloudpickle, dill, numba, bokeh, vincent, beautifulsoup, xlrd pre-installed

#### lots of great conda packages!
# https://conda-forge.org/feedstocks/
```
