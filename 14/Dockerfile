ARG BASE
FROM ${BASE}

ARG NODE_MAJOR_VERSION
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y --no-install-recommends \
        apt-utils \
        gpg-agent \
        curl \
        software-properties-common \
        tzdata \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*

RUN curl -sL https://deb.nodesource.com/setup_${NODE_MAJOR_VERSION}.x | bash - \
 && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
 && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
       nodejs \
       yarn \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*

RUN addgroup --gid 1000 node \
 && adduser --uid 1000 --ingroup node \
    --shell /bin/sh --disabled-login --gecos "" node 

ENTRYPOINT [ "node" ]

LABEL \
    maintainer="Rui Carmo" \
    org.label-schema.arch=${ARCH} \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.description="NodeJS Runtime" \
    org.label-schema.name="NodeJS" \
    org.label-schema.vcs-ref=${VCS_REF} \
    org.label-schema.vcs-type="Git" \
    org.label-schema.vcs-url=${VCS_URL} \
    org.label-schema.version=${BUILD_VERSION} \
    org.label-schema.build-date=${BUILD_DATE} \
