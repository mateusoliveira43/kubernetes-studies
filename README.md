# Kubernetes studies :ship::pencil:

Studies to understand how Kubernetes works.

## About

[Kubernetes](https://kubernetes.io/docs/concepts/overview/) is a management tool for containerized applications. it is not a mere orchestration system. Orchestration is the execution of defined workflow steps. On the other hand, Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the desired state.

### [Components](https://kubernetes.io/docs/concepts/overview/components/)

- Cluster: a set of control plane and worker nodes. Every cluster has at least one worker node.
- Control Plane: manages the worker nodes and the pods in the cluster. Control planes cannot be used to allocate pods (without changing their [taint](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)). It is composed by kube-apiserver, ETCD, kube-scheduler and kube-controller-manager (optionally cloud-controller-manager).
    - ETCD: a highly-available key value store for all cluster data.
    - kube-scheduler: selects the [best](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler) node for each pod.
    - kube-controller-manager: controls if the current state of the cluster is the desired state.
- Node: a worker machine with Kubelet, a network proxy (kube-proxy), container runtime and a set of pods.
    - Kubelet: a process responsible for communication between the cluster control plane and the worker node.
- Pod: a set of containers.


### [Workload Resources](https://kubernetes.io/docs/concepts/workloads/controllers/)

There are still [Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/), [Automatic Clean-up for Finished Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/ttlafterfinished/), [CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/) and [ReplicationController](https://kubernetes.io/docs/concepts/workloads/controllers/replicationcontroller/) (deprecated) not addressed in this material.

#### Deployments

Provides declarative updates for Pods and ReplicaSets (to maintain a stable set of replica Pods running at any given time). The Deployment Controller changes the current state to the desired state, at a controlled rate. The pods only share one [PVC](https://kubernetes.io/docs/reference/glossary/?all=true#term-persistent-volume-claim) among them.

#### StatefulSets

Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods. Each pod has its own [PVC](https://kubernetes.io/docs/reference/glossary/?all=true#term-persistent-volume-claim). Good for databases (cluster of databases), e.g. one RW database and the others RO (syncing with the first). If the first goes down, one of the others become a RW and a new RO is created.

#### DaemonSet

Creates a pod in each (or some) node. The pods only share one [PVC](https://kubernetes.io/docs/reference/glossary/?all=true#term-persistent-volume-claim) among them.
Good for monitoring/log solutions.

### Helm

When configuring Kubernetes objects, the number of **manifests** can easily grow fast (along with the commands to create them). To solve this problem, there is the Helm tool. Helm manages Kubernetes packages called **[Charts](https://helm.sh/docs/topics/charts/)**, which provide a reproducible way of creating and sharing Kubernetes applications, with few commands.

Remember that Kubernetes is the Greek for "helmsman".

## Running

To run the commands in this section, use [minikube](https://minikube.sigs.k8s.io/docs/).

[To install minikube](https://minikube.sigs.k8s.io/docs/start/), run
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
rm -f minikube-linux-amd64
```

Follow [Kubernetes](https://kubernetes.io/docs/tutorials/hello-minikube/) and [minikube](https://minikube.sigs.k8s.io/docs/start/) tutorials.

To add [`kubectl`](https://kubernetes.io/docs/reference/kubectl/) alias, in each new terminal, run
```
alias kubectl="minikube kubectl --"
```

It is possible to pass more than one [resource type](https://kubernetes.io/docs/reference/kubectl/#resource-types) to `kubectl` command. For example
```
kubectl get pod,svc,deploy
```

To uninstall minikube, run
```
sudo rm -f /usr/local/bin/minikube
```

### TODO Helm

https://helm.sh/docs/intro/quickstart/
https://helm.sh/docs/intro/using_helm/

## References :books:

- https://github.com/badtuxx/DescomplicandoKubernetes
- https://kubernetes.io/docs/home/
- https://kubernetes.io/docs/reference/glossary/?all=true
- https://helm.sh/docs/
