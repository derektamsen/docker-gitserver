FROM debian:jessie

RUN useradd --system --no-create-home --user-group --shell /bin/false git

RUN mkdir -p /data && \
  chown -R git:git /data

USER git

ENTRYPOINT ["/bin/true"]
