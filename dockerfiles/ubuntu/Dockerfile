ARG base_image=ubuntu:22.04

FROM ${base_image}

# Verify we're running Ubuntu (supply chain security check)
RUN test -f /etc/lsb-release && grep -q "Ubuntu" /etc/lsb-release || \
    (echo "ERROR: Base image is not Ubuntu. Aborting build for security." && exit 1)

# Install dependencies with security updates and cleanup
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        curl \
        bash \
        jq \
        gettext && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY check /opt/resource/check
COPY in    /opt/resource/in
COPY out   /opt/resource/out

RUN chmod +x /opt/resource/out /opt/resource/in /opt/resource/check

ADD test/ /opt/resource-tests/
RUN /opt/resource-tests/all.sh && \
    rm -rf /tmp/* /var/tmp/* /opt/resource-tests
