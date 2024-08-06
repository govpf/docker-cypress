FROM cypress/base:12.8.1

ENV TZ Pacific/Tahiti
ARG CYPRESS_VERSION="3.3.1"

RUN echo "$TZ" > /etc/timezone \
    && rm -f /etc/localtime \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    && apt-get update && apt-get install -y --no-install-recommends \
        git locales net-tools curl ca-certificates gnupg dirmngr \
    && curl https://bin.gov.pf/artifactory/ca/casit.crt > /usr/local/share/ca-certificates/casit.crt \
    && curl https://bin.gov.pf/artifactory/ca/casit-prod2.crt > /usr/local/share/ca-certificates/casit-prod2.crt \
    && curl https://bin.gov.pf/artifactory/ca/cadsi-prod.crt > /usr/local/share/ca-certificates/cadsi-prod.crt \    
    && update-ca-certificates \
    && locale-gen fr_FR.UTF-8 \
    && dpkg-reconfigure locales \
    && rm -rf /var/lib/apt/lists/* \
    && npm config -g set user $(whoami) \
    && npm install -g "cypress@${CYPRESS_VERSION}" jwt-decode \
    && cypress verify \
    && cypress cache path \
    && cypress cache list \
    && echo "node version:    $(node -v) \n" \
            "npm version:     $(npm -v) \n" \
            "yarn version:    $(yarn -v) \n" \
            "debian version:  $(cat /etc/debian_version) \n" \
            "user:            $(whoami) \n"
