<h1>CHEAT SHEET</h1>
<h2>COMMANDS</h2>

<h3>DOCKER</h3>

1) docker build -t <IMAGE_NAME> <DOCKERFILE_PATH> || docker images
2) docker run --name <CONTAINER_NAME> -p 8080:8080 -d <IMAGE_NAME> || docker ps
3) docker inspect <CONTAINER_NAME> | docker exec -it <CONTAINER_NAME> bash

<h3>DOCKER HUB</h3>

1) docker build -t <IMAGE_NAME> <DOCKERFILE_PATH> 
2) docker tag <IMAGE_NAME> <DOCKER_HUB_ID/IMAGE_NAME>
3) docker push <DOCKER_HUB_ID/IMAGE_NAME>

<h3>DOCKER CONATAINER LOGS</h3>

1) docker logs <CONTAINER_ID> | ssh log into the node
1) kubectl logs <NAME_INSTANCE> (-c container (if hv multiple containers same pod))

<h3>MINIKUBE</h3>

1) minikube start
2) kubectl run <NAME_INSTANCE> --image=<DOCKER_REGISTRY_IMAGE> --port=8080
3) kubectl get svc | kubectl get nodes | kubectl get po
4) kubectl cluster-info | kubectl describe po

<h3>SERVICE EXPOSE</h3>

1) kubectl expose pod <POD_NAME> --type=LoadBalancer --name <SERVICE_NAME>
2) minikube tunnel (separate terminal)
3) minikube service <SERVICE_NAME>

<h3>POD FORWARDING</h3>

1) kubectl port-forward <NAME_INSTANCE> 8888:8080 (in a different terminal)
2) http://localhost:8888

<h3>POD YAML</h3>

1) kubectl create -f <POD.yaml>
	-> kubectl get po <POD_NAME> -o yaml
2) kubectl delete po <POD_NAME>
2) kubectl delete po --all

<h3>LABELS</h3>

1) kubectl label <RESOURCE> <RESOURCE_NAME> <LABEL_NAME>=<VALUE>
1) kubectl label <RESOURCE> <RESOURCE_NAME> <LABEL_NAME>=<NEW_VALUE> --overwrite
	-> kubectl get <RESOURCE> -L <KEY>
	-> kubectl get <RESOURCE> --show-lables
2) kubectl delete <RESOURCE> <RESOURCE_NAME> -l <LABEL_NAME>=<VALUE>

<h3>LABELS SELECTORS</h3>

1) Contain a certain key -> kubectl get <RESOURCE> -l <CERTAIN_KEY>
2) Don't contain a certain key -> kubectl get <RESOURCE> -l '!<CERTAIN_KEY>'
3) Contain a certain key and value -> kubectl get <RESOURCE> -l <CERTAIN_KEY>=<VALUE>
4) Others: <KEY!=VALUE> | <KEY> in (<VALUE1,VALUE2>) | <KEY> notin (<VALUE1,VALUE2>)

<h3>REPLICA SET LABELS SELECTORS</h3>

1) Label value must match specific value -> In
2) Label value must not match specific value -> NotIn
3) Label with specific key -> Exists
4) Label with no specific ket -> DoesNotExist

<h3>ANNOTATIONS</h3>

kubectl annotate <RESOURCE> <RESOURCE_NAME> <ANOTATION>="<VALUE>"
	-> kubectl describe <RESOURCE> <RESOURCE_NAME>

<h3>NAMESPACES</h3>

1) kubectl create -f <NAMESPACE.yaml>
1) kubectl create namespace <NAMESPACE_NAME>
2) kubectl delete ns <NAMESPACE_NAME>
Add resources: kubectl create -f <POD.yaml> -n <NAMESPACE_NAME>
Change Namespace: kubectl config set-context $(kubectl config current-context) --namespace <NAMESPACE_NAME>

<h3>REPLICATION CONTROLLER</h3>

1) kubectl create -f <REPLICATION_CONTROLLER.yaml>
2) kubectl edit rc <REPLICATION_CONTROLLER_NAME>
2) kubectl get rc <REPLICATION_CONTROLLER_NAME> -o yaml > <REPLICATION_CONTROLLER.yaml> | #edit text | kubectl apply -f <REPLICATION_CONTROLLER.yaml>
3) kubectl scale <REPLICATION_CONTROLLER_NAME> --replicas=X
4) kubectl delete rc <REPLICATION_CONTROLLER_NAME> 
4) kubectl delete rc <REPLICATION_CONTROLLER_NAME> --cascade=false

<h3>REPLICA SET</h3>

1) kubectl create -f <REPLICA_SET.yaml>