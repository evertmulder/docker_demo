# Installatie

## Download minishift & Virtualbox

Zorg ervoor dat minishift in het path te vinden is.

```bash
minishift config set memory 6144
minishift config set cpus 2
minishift config set vm-driver virtualbox
minishift addon enable admin-user
minishift addon enable anyuid
```

Run it!

```bash
$ minishift start
...
OpenShift server started.

The server is accessible via web console at:
    https://192.168.99.100:8443

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin

```


```sh
$ minishift config view
- cpus: 3
- memory: 8192
- vm-driver: virtualbox
$ minishift status
Minishift:  Running
Profile:    minishift
OpenShift:  Running (openshift v3.10.0+e3465d0-44)
DiskUsage:  16% of 19G (Mounted On: /mnt/sda1)
CacheUsage: 1.849 GB (used by oc binary, ISO or cached images)
$ minishift ip
192.168.99.103
$ minishift dashboard --url
http://192.168.99.103:30000
$ minishift dashboard
```


```sh
eval $(minishift docker-env)
eval $(minishift oc-env)
```

Voer een aantal docker commando's uit:

```bash
$ docker ps
$ docker images
```


```
$ minishift ssh
$ free -h
$ df -h
$ top
$ ctrl-c
$ exit
```

```
$ oc login $(minishift ip):8443 -u admin -p admin

$ kubectl config set-context $(kubectl config current-context) --namespace=myproject
Context "myproject/192-168-99-100:8443/admin" modified.

$ oc status

$ kubectl get deployments

$ kubectl get pods

$ kubectl expose deployment hello-minikube --type=NodePort
$ kubectl get service
$ minishift ip

```
connect met service poort


```
kubectl describe deployment hello-minikube

kubectl get pods -w

$ kubectl delete service hello-minikube

$ kubectl delete deployment hello-minikube

```