FROM debian:jessie

ENV LC_ALL=C
ENV DEBIAN_FRONTEND=noninteractive

# Install the services
RUN apt-get update && apt-get install -y \
  openssh-server \
  git \
  gitolite3

# Fixup stuff for sshd
RUN mkdir -p /var/run/sshd
RUN sed -i 's/^AcceptEnv LANG LC_\*$//g' /etc/ssh/sshd_config
RUN sed -i '/session    required     pam_loginuid.so/d' /etc/pam.d/sshd

# Create a shareable sshd host key location
RUN mkdir -p /data/etc/ssh

# create the git user
RUN adduser --system --shell /bin/bash --group --disabled-password --home /data/git git

# add setup script
ADD ./init /init
RUN chmod +x /init

EXPOSE 22

ENTRYPOINT [ '/init', "/usr/sbin/sshd", "-D",
            '-h /data/etc/ssh/ssh_host_dsa_key',
            '-h /data/etc/ssh/ssh_host_ecdsa_key',
            '-h /data/etc/ssh/ssh_host_ed25519_key',
            '-h /data/etc/ssh/ssh_host_rsa_key' ]
