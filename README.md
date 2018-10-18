## Install

1 Install `hetzner-kube`

2 Create a config file

```sh
#!/bin/sh
PROJECT_CONTEXT=[your-project-name]
DOMAIN=[your-cluster-domain]
CLUSTER_NAME=[your-cluster-name]

# Create args https://github.com/xetys/hetzner-kube/blob/master/docs/cluster-create.md
CLUSTER_CREATE_EXTRA_ARGS=[your-optional-args]

HETZNER_TOKEN=[your-hetzner-token]
ZEIT_TOKEN=[your-zeit-token]

# Add ssh-key by "$ hetzner-kube ssh-key add -n <name>"
# it will use your .ssh/id_rsa
SSH_KEY_NAME=[your-ssh-key]
```

3 Make sure `./cluster` has execute rights

```
$ chmod 700 ./cluster
```

Now you can create your cluster. Check the help:

```
./cluster help
```

## Dashboard
Creating an admin user for k8s Dashboard
https://github.com/kubernetes/dashboard/wiki/Creating-sample-user#bearer-token

$ kubectl apply -f admin-user.yml
$ kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')

## OpenEBS on Hetzner Cloud
http://stytex.de/blog/2018/01/29/deploy-kubernetes-hetzner-cloud-openebs/
$ kubectl apply -f https://raw.githubusercontent.com/openebs/openebs/master/k8s/openebs-operator.yaml
$ kubectl apply -f https://raw.githubusercontent.com/openebs/openebs/master/k8s/openebs-storageclasses.yaml

## Mongodb

```sh
# http://pauldone.blogspot.com/2017/06/deploying-mongodb-on-kubernetes-gke25.html
# kubectl apply -f db-ssd-persistentvolume.yaml
# kubectl get persistentvolumes

# TMPFILE=$(mktemp)
# /usr/bin/openssl rand -base64 741 > $TMPFILE
# kubectl create secret generic shared-bootstrap-data –from file=internal-auth-mongodb-keyfile=$TMPFILE
# rm $TMPFILE

# kubectl apply -f db-mongodb-service.yaml
# kubectl get all
# kubectl get persistentvolumes
# kubectl exec -it mongod-0 -c mongod-container bash
```

https://docs.openebs.io/docs/next/MongoDB.html
```sh
kubectl apply -f nginx.yml
kubectl apply -f mongodb-stateful.yml
kubectl apply -f helm-tiller.yml 
helm init --service-account tiller
brew install helm
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
helm init --service-account tiller
```