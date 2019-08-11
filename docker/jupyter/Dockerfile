FROM jupyter/datascience-notebook:27ba57364579

USER root

ADD conf/jupyter_notebook_config.py ${HOME}/.jupyter/jupyter_notebook_config.py
ARG PASSWORD=password
RUN sed -i "s/<password>/${PASSWORD}/g" ${HOME}/.jupyter/jupyter_notebook_config.py

ADD ./conf/ipaexg /usr/share/fonts/ipaexg
RUN fc-cache -fv && rm -rf /home/jovyan/.cache/matplotlib
ADD ./conf/matplotlibrc /home/jovyan/.config/matplotlib/matplotlibrc

ADD ./requirements.txt /tmp
RUN cd /tmp && pip install -r requirements.txt

WORKDIR /var/www
EXPOSE 8888
