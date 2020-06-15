#FROM ubuntu:latest as intermediate
FROM ubuntu:latest

RUN apt-get -q update \
    && apt-get install -yq --no-install-recommends wget golang git\
	&& apt-get clean && rm -rf /var/lib/apt/lists/* \
    && echo "===============Finished Update======================"

WORKDIR /usr/src/app
RUN wget https://github.com/gohugoio/hugo/releases/download/v0.72.0/hugo_extended_0.72.0_Linux-64bit.deb --no-check-certificate \
    && echo "Finished Download" \ 
    && dpkg -i hugo*_Linux-64bit.deb \ 
    && hugo --help \
    && rm  hugo*_Linux-64bit.deb \
    && echo "==================Finished Install of hugo=======================" 
 




