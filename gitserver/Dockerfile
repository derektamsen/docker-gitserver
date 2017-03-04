FROM alpine:3.5

# create git user group
RUN addgroup -S git ;\
  adduser -S -H -h /data/git -s /bin/sh -G git -D git

# Install the services
RUN apk update && apk --update add \
  openssh \
  git \
  gitolite \
  && rm  -rf /tmp/* /var/cache/apk/*

# Improve sshd security
COPY sshd_config /etc/ssh/sshd_config

# add setup script
COPY init /init
RUN chmod +x /init

EXPOSE 22

ENTRYPOINT ["/init", "/usr/sbin/sshd", "-D", "-f", "/etc/ssh/sshd_config"]
