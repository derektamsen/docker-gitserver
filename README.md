[![](https://badge.imagelayers.io/derektamsen/gitserver:latest.svg)](https://imagelayers.io/?images=derektamsen/gitserver:latest 'Get your own badge on imagelayers.io')

# docker-gitserver
A gitolite server running in docker. All repositories are stored in the
'gitserver-data' container. This allows stopping, removing, and upgrading the
'gitserver' container without losing any data.

# Starting the data and server containers
- clone repository to your docker host.
- ```
  GITSERVER_SSH_KEY=$(cat ~/.ssh/id_rsa.pub) \
  GITSERVER_SSH_ADMIN=${USER} \
  docker-compose up -d
  ```
