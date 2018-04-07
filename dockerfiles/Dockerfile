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
