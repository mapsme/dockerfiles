FROM ubuntu:18.04

MAINTAINER Maksim Andrianov <m.andrianov@corp.mail.ru>

ARG TAG=master

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

RUN apt-get update && apt-get install -y \
	build-essential \
	cmake \
	git \
	libgl1-mesa-dev \
	libsqlite3-dev \
	python3 \
	python3-pip \
	qt5-default \
	zlib1g-dev \
	&& ln -s /usr/bin/python3 /usr/bin/python

WORKDIR /mapsme

RUN git clone -b ${TAG} --single-branch --recurse-submodules -j8  https://github.com/mapsme/omim.git

RUN echo "" | ./omim/configure.sh \
	&& ./omim/tools/unix/build_omim.sh -rs generator_tool \ 
	&& pip3 install -r omim/tools/python/maps_generator/requirements.txt


RUN useradd -d /mapsme -s /bin/bash mapsme \
	&& chown mapsme:mapsme /mapsme
USER mapsme

ENV PYTHONPATH $PYTHONPATH:omim/tools/python

ENTRYPOINT ["python3", "-m", "maps_generator"]

