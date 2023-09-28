ARG base_image

FROM ${base_image}


RUN apt update && apt install -y \
 curl \
 bash \
 jq \
 gettext

COPY check /opt/resource/check
COPY in    /opt/resource/in
COPY out   /opt/resource/out

RUN chmod +x /opt/resource/out /opt/resource/in /opt/resource/check

ADD test/ /opt/resource-tests/
RUN /opt/resource-tests/all.sh \
 && rm -rf /tmp/*
