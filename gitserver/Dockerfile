FROM alpine:3.5

ENV LC_ALL=C DEBIAN_FRONTEND=noninteractive

# create git user group
RUN addgroup -S git ;\
  adduser -S -H -h /data/git -s /bin/sh -D git

# Install the services
RUN apk update && apk add \
  openssh \
  git \
  gitolite

# Improve sshd security
COPY sshd_config /etc/ssh/sshd_config

# Fixup stuff for sshd
RUN mkdir -p /var/run/sshd ;\
  sed -i 's/^AcceptEnv LANG LC_\*$//g' /etc/ssh/sshd_config

# add setup script
COPY init /init
RUN chmod +x /init

EXPOSE 22

ENTRYPOINT ["/init", "/usr/sbin/sshd", "-D", "-h", "/data/etc/ssh/ssh_host_ecdsa_key", "-h", "/data/etc/ssh/ssh_host_ed25519_key", "-h", "/data/etc/ssh/ssh_host_rsa_key"]
