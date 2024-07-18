# Harbor

Deploys goharbor's Harbor to Docker Swarm using a stack file derived from [bitnami/harbor-portal](https://github.com/bitnami/containers/tree/main/bitnami/harbor-portal)

To make this deployment work on your docker swarm you will need at least to:

* Edit the Volumes directives to point to your own cluster aware volume driver. Its fine to use `local` in the case of a single node swarm.
* Replace `example.com` with a wildcard DNS that points at your own swarm.
* Have Traefik installed as a global ingress and handling https for that domain.
* Replace the `traefik` network with the name of your traefik public network.

The compose file this is derived from is used for testing the bitnami/harbor-portal container and is not fully functional, but it serves to get swarm hosted Harbor working.

## Install in your Swarm

Setup your workdirectory with the following commands (please verify all the variables in the yaml files this generates):

```bash
export BASE_DIR="."
export WORKDIR="$(pwd)/test"
export CHART_DIR="../chart"
export START_PWD=$(pwd)

mkdir -p $WORKDIR/secrets

echo "exec nothelm run deploy --project-dir $CHART_DIR -f $CHART_DIR/values.yaml" > $WORKDIR/setup.sh