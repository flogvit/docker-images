FROM ubuntu:16.04
LABEL maintainer="Vegard Hanssen <Vegard.Hanssen@menneske.no>"
ARG DEBIAN_FRONTEND=noninteractive

# install apt packages
RUN apt-get update
RUN apt-get install -yq python3-pip htop nano git wget libglib2.0-0 ffmpeg

# install python modules
ADD requirements.txt /
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt

# setup jupyter
RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension
RUN jupyter contrib nbextension install --user
RUN jupyter nbextension enable codefolding/main

RUN mkdir -p /notebooks && chmod a+rwx /notebooks
RUN mkdir /.local && chmod a+rwx /.local

WORKDIR /notebooks
EXPOSE 8080 7007
CMD ["bash", "-c", "jupyter notebook --notebook-dir=/notebooks --ip 0.0.0.0 --no-browser --allow-root"]
