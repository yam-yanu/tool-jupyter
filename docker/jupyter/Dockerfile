FROM python:latest

RUN pip install --upgrade pip && \
  pip install jupyter==1.0.0

ADD conf/jupyter_notebook_config.py /root/.jupyter/jupyter_notebook_config.py

ADD ./conf/ipaexg /usr/share/fonts/ipaexg
RUN fc-cache -fv && rm -rf /root/.cache/matplotlib
ADD ./conf/matplotlibrc /root/.config/matplotlib/matplotlibrc

RUN apt-get install -y libjpeg-dev

## Install Chrome
RUN cd /tmp && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install && \
    curl -O https://chromedriver.storage.googleapis.com/85.0.4183.87/chromedriver_linux64.zip && \
    unzip chromedriver_linux64.zip && \
    mv chromedriver /usr/local/bin && \
    apt-get update && apt-get install -y libnss3 libgconf-2-4 xvfb libxi6
ADD ./requirements.txt /tmp
RUN pip install -r /tmp/requirements.txt && rm /tmp/requirements.txt

WORKDIR /var/www
EXPOSE 8888

ENTRYPOINT ["jupyter", "notebook", "--ip", "0.0.0.0", "--allow-root", "--no-browser", "--NotebookApp.token=''", "--NotebookApp.password=''"]
