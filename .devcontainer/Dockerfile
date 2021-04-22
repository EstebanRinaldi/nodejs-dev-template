# [Choice] Node.js version: 14, 12, 10, lts, lts-buster
ARG VARIANT=lts
FROM node:${VARIANT}

# Set Environment Variables
ENV DEBIAN_FRONTEND noninteractive

# Copy all scripts and allow execution.
COPY ./scripts /scripts
RUN chmod +x /scripts/*

# Install apt-utils
RUN /scripts/apt-install.sh "apt-utils"

# # Create non-root user.
# ARG USERNAME=node
# ARG USER_UID=1000
# ARG USER_GID=$USER_UID
# RUN /scripts/create-user.sh "${USERNAME}" "${USER_UID}" "${USER_GID}"

# Set timezone
ARG TIMEZONE
RUN /scripts/set-timezone.sh "${TIMEZONE}"

# Install locales and set locale and language.
ARG LOCALE="C.UTF-8"
ARG ADDITIONAL_LOCALES=""
RUN /scripts/install-locales.sh "${ADDITIONAL_LOCALES} ${LOCALE}"
ENV LC_ALL="${LOCALE}"
ENV LANG="${LOCALE}"

# Remove imagemagick due to https://security-tracker.debian.org/tracker/CVE-2019-10131
RUN apt-get purge -y imagemagick imagemagick-6-common

# Update local packages
RUN /scripts/apt-upgrade.sh

# Cleanup
RUN /scripts/cleanup.sh

# Install needed packages and yarn.
RUN /scripts/apt-install.sh "apt-transport-https curl ca-certificates tar gnupg2 yarn"

# Configure global npm install location, use group to adapt to UID/GID changes
ARG NPM_GLOBAL=/usr/local/share/npm-global
ENV PATH=${NPM_GLOBAL}/bin:${PATH}
RUN if ! cat /etc/group | grep -e "^npm:" > /dev/null 2>&1; then groupadd -r npm; fi \
    && usermod -a -G npm ${USERNAME} \
    && umask 0002 \
    && mkdir -p ${NPM_GLOBAL} \
    && chown ${USERNAME}:npm ${NPM_GLOBAL} \
    && chmod g+s ${NPM_GLOBAL} \
    && npm config -g set prefix ${NPM_GLOBAL} \
    && sudo -u ${USERNAME} npm config -g set prefix ${NPM_GLOBAL}

# Install eslint, nodemon and extra modules if required.
ARG EXTRA_MODULES=""
RUN su ${USERNAME} -c "umask 0002 && npm install -g nodemon ${EXTRA_MODULES}" \
    && npm cache clean --force > /dev/null 2>&1

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>""

# Change to non-root user.
USER ${USERNAME}

# Sets the source code dir as working dir.
WORKDIR /workspace

EXPOSE 3000
