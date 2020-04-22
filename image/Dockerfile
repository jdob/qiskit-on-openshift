FROM centos/python-36-centos7:latest

EXPOSE 8888

# User setup for OpenShift
USER root
ENV HOME=/jupyter
RUN mkdir -p ${HOME}/notebooks && \
    useradd -u 9000 -r -g 0 -d ${HOME} -s /sbin/nologin \
            -c "Jupyter User" jupyter-user
WORKDIR ${HOME}

# Python dependencies
RUN pip install --upgrade pip && \
    pip install qiskit jupyter

# Specific notebook configuration
ADD jupyter_notebook_config.py ${HOME}/jupyter_notebook_config.py
ADD playground.ipynb ${HOME}/notebooks/playground.ipynb
RUN chown -R 9000:0 ${HOME} && \
    find ${HOME} -type d -exec chmod g+ws {} \;
WORKDIR ${HOME}/notebooks

# Run the notebook
USER 1001
CMD ["jupyter", "notebook", "--config", "/jupyter/jupyter_notebook_config.py"]
