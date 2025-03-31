```open -a docker // open docker demon
docker system df // check docker storage
docker system prune -a --volumes // cleanup, --volume is optional

// check where it is installed
cd /opt/homebrew/bin/kind
cd /usr/local/bin

// to find where it stored
which kind

_____x______x_____x_____

brew install kind // install
kind version // check v

brew install kubectl
kubectl version --client

// for 1 node
kind create cluster --name first-cluster // create a new cluster, it creates the control panel not the worker node

// now create clusters through .yml file
// you have to create this in vi or vim, so open the folder first then give it a name (check vi commands to save, quit, rename)
// create a new folder & a new file inside that: kind.yml
// it creates 2 local workers and 1 master node
// for multiple node: here 1 master node and 2 workder node

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker

// then run this to run or create :
kind create cluster --config clusters.yml --name first-test

kind delete cluster --name first-cluster
docker ps // to see all are running or not

cat /.kube/config // (optional, dont really need it)
// now we have to interact with the 1 master node
kubectl // if it is running the fine

kubectl get nodes --v=8 // to get the endpoint
// if it shows refused or dont show any endpoint like 127:0.0, do this:

kind get clusters // get all the clusters
kubectl config get-contexts // get the name and add a kind- before that name
// generally it is named as kind-<node_name>
kubectl config use-context kind-first-kind // switch from one to another

// now do 
kubectl get nodes

// now we have to create the pods
// untill now we ware running on docker, but now we use pods
 cat /Users/rudra/.kube/config // here is the config file saved
  kubectl config view // to see the config

kubectl get pods // to check all pods
// for testing we have to pull the nginx image
docker run -p 3000:80 nginx

kubectl run nginx --name=nginx --port=80 // the name shoud the image name we pulled nginx so here nginx
// it will say pod/nginx started

docker logs nginx // you will see the same logs, as we saw while running docker -> docker run -p 3000:80 nginx

kubectl describe pod nginx // show where it is running, check the node

// to run another pod
kubectl run nginx-2 --name=nginx --port=80

// to run postgress pod
kubectl run postgres --name=postgres --port=80

kubectl get pods -w // watch

kubectl delete pod postgres // to delete pod

// manifest
// create a new manifest file in a new folder - open vi & paste this:

apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80

kubectl apply -f manifest.yml

```