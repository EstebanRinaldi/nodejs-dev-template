ARG VARIANT=latest
FROM postgres:${VARIANT}

# Copy all scripts and allow execution.
COPY ./scripts /scripts
RUN chmod +x /scripts/*

# Set timezone
ARG TIMEZONE
RUN /scripts/set-timezone.sh "${TIMEZONE}"

# Install locales and set locale and language.
ARG LOCALE="C.UTF-8"
ARG ADDITIONAL_LOCALES=""
RUN /scripts/install-locales.sh "${ADDITIONAL_LOCALES} ${LOCALE}"
ENV LC_ALL="${LOCALE}" 
ENV LANG="${LOCALE}"
    
EXPOSE 5432
