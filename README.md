# docker-gitserver
A gitolite server running in docker. All repositories are stored in the
'gitserver-data' container. This allows stopping, removing, and upgrading the
'gitserver' container without losing any data.

# Starting the data and server containers
## Docker Compose
- clone repository to your docker host.
- ```
  GITSERVER_SSH_KEY=$(cat ~/.ssh/id_rsa.pub) \
  GITSERVER_SSH_ADMIN=${USER} \
  docker-compose up -d
  ```

## Kubernetes
- Add the admin ssh public key to the configmap for your instances namespace:

  ```
  kubectl create configmap gitserver-config \
    --from-literal=ssh.key="$(cat ${HOME}/.ssh/id_ed25519.pub | tr -d '\n')" \
    --from-literal=ssh.admin="${USER}"
  ```

- Deploy the kubernetes manifest:

  ```
  kubectl apply -f https://raw.githubusercontent.com/derektamsen/docker-gitserver/master/gitserver-k8s.yaml
  ```
