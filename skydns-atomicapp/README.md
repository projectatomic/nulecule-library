# SkyDNS Atomic App

### Description

Deploys [SkyDNS](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns) on the respective Kubernetes cluster.

### Deployment

__Requirements:__
You must provide a cluster DNS and cluster domain in your Kubernetes deployment:
```
--cluster-dns=<dns_server>
--cluster-domain=<dns_domain>
```

If you are using default values provided in `Nulecule` file, you can use:
```
KUBELET_ARGS="--cluster_dns=10.254.0.10 --cluster_domain=cluster.local"
```

__Note about SELinux being enabled:__
If you have SELinux enabled, then etcd container will be failing with
`etcdserver create snapshot directory error: mkdir /var/etcd/data/member: permission denied`
and kubectl-proxy will be stuck.


To fix etcd, you have to label `/var/lib/kubelet/pods/{{ pod_uid }}/volumes/kubernetes.io~empty-dir` `svirt_sandbox_file_t`

To fix kubectl proxy, you have to label `/var/lib/kubelet/pods/{{ pod_uid }}/volumes/kubernetes.io~secret` `svirt_sandbox_file_t` (you may have to restart kubectl-proxy container)

You can get `pod_uid` with this command: 
```
# kubectl  get pods
NAME                READY     STATUS    RESTARTS   AGE
kube-dns-v9-sl60t   5/5       Running   4          1h

# kubectl  get pod kube-dns-v9-sl60t -o template --template="{{ .metadata.uid }}"
031c5758-8210-11e5-b8db-525400e09276
```

#### Deploying with Default Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/skydns-atomicapp
```

##### Using Atomic App

```sh
sudo atomicapp run projectatomic/skydns-atomicapp
```

#### Deploying with User-Provided Parameters

##### Using Atomic CLI

```sh
sudo atomic run projectatomic/skydns-atomicapp --mode fetch --destination skydns-atomicapp
cd skydns-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
sudo atomic run projectatomic/skydns-atomicapp .
```

##### Using Atomic App

```sh
atomicapp fetch projectatomic/skydns-atomicapp --destination skydns-atomicapp
cd skydns-atomicapp
cp answers.conf.sample answers.conf # Modify then copy answers.conf.sample
atomicapp run .
```

### Interaction

To test and see if SkyDNS is working correctly:

Create file `busybox.yaml`:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - image: busybox
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
    name: busybox
  restartPolicy: Always
```

Create a pod using this file:
```
kubectl create -f busybox.yaml
```

Wait until the pod is running:
```
kubectl get pods busybox
```

Once the pod is running exec nslookup in that container:
```
kubectl exec busybox nslookup kubernetes
```

You sould see output simillar to this:
```
Server:    10.254.0.10
Address 1: 10.254.0.10

Name:      kubernetes
Address 1: 10.254.0.1
```
