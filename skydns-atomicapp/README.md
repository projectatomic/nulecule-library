# skydns-atomicapp
 
An Atomicapp (based on http://github.com/projectatomic/nulecule) 
provides a skyDNS service for Kubernetes (https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns/skydns) 



## 1) enable DNS in Kubernetes cluster

Add following flags to kubelet.
```
--cluster-dns=<dns_server>
--cluster-domain=<dns_domain>
```

In default kubernetes setup you can do this by editing `KUBELET_ARGS` in 
`/etc/kubernetes/kubelet`.

If you are using default values provided in `Nulecule` file, you can use this:
```
KUBELET_ARGS="--cluster_dns=10.254.0.10 --cluster_domain=cluster.local"
```

Don't forget to restart kubelets `systemctl restart kubelet`

## 2) Run SkyDNS in Kubernetes cluster
Create empty directory for your application.

### Option a: use default parameters
Download and run application, using default values.
```
atomic run projectatomic/skydns-atomicapp
```

### Option b: custom parameters

Download the application files:
```
atomic install projectatomic/skydns-atomicapp
```

Create `answers.conf`
```
cp answers.conf.sample answers.conf
```

Review and edit parameters in `answers.conf` if desired
```
$EDITOR  answers.conf
```

Run application
```
atomic run projectatomic/skydns-atomicapp
```

## Note about SELinux
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



## 3) Test if it is working

### Create simple pod for test

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

Create pod using this file:
```
kubectl create -f busybox.yaml
```

Wait until pod is running:
```
kubectl get pods busybox
```

Once is running exec nslookup in that container:
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



