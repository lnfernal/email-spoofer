FROM alpine:3.11
LABEL maintainer="MyBot Proxy mybotproxy@spoofme.com"

# Install required packages
RUN apk add --no-cache postfix tzdata supervisor rsyslog libsasl cyrus-sasl-plain

# Set up configuration 
COPY configure-postfix /
# Remove the below when pushing to dockerhub
RUN chmod +x /configure-postfix
COPY supervisord.conf /etc/supervisord.conf
COPY rsyslog.conf /etc/rsyslog.conf
COPY header_checks /etc/postfix/header_checks

# Run supervisord
USER       root
WORKDIR    /tmp

EXPOSE     25
CMD        ["/bin/sh", "-c", "/configure-postfix"]
