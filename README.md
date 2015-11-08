# docker-gitserver
A gitolite server running in docker. All repositories are stored in the
'gitserver-data' container. This allows stopping, removing, and upgrading the
'gitserver' container without losing any data.

# Starting the data and server containers
- clone repository to your docker host.
- `./run`
