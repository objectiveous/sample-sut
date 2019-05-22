# Testbed Definition for Demo 

```console
minikube start --memory=8192 --cpus=4 --kubernetes-version=v1.14.0 --vm-driver=hyperkit \
               --bootstrapper=kubeadm --insecure-registry='docker.apple.com' \
               --extra-config=apiserver.enable-admission-plugins="LimitRanger,NamespaceExists,NamespaceLifecycle,ResourceQuota,ServiceAccount,DefaultStorageClass,MutatingAdmissionWebhook"
```


# Install the Testbed definition

First, we'll install redis-graph and neo4j into our cluster using kubectl and [kustomize](https://kustomize.io). 

```console
 kubectl apply --kustomize .
```

# Redis Graph 

```console
kubectl port-forward svc/redis-master 6379:6379
``` 

```console
brew install redis

```

log into redis: 

```console 

redis-cli

```

Insert some nodes: 

```
GRAPH.QUERY MotoGP "CREATE (:Rider {name:'Valentino Rossi'})-[:rides]->(:Team {name:'Yamaha'}), (:Rider {name:'Dani Pedrosa'})-[:rides]->(:Team {name:'Honda'}), (:Rider {name:'Andrea Dovizioso'})-[:rides]->(:Team {name:'Ducati'})" 
```

And finally, search for some nodes: 

```
GRAPH.QUERY MotoGP "MATCH (r:Rider)-[:rides]->(t:Team) WHERE t.name = 'Yamaha' RETURN r,t"
```

# Neo4j 

```console 

kubectl port-forward neo4j-core-0 8474:7474 8687:7687

```

Visit the UI [http://localhost:8474/](http://localhost:8474/) and connect using ```:server connect```. When 
prompted for a connection string use ```bolt://localhost:8687```. No credentials are required. 


