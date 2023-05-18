# 🚀 Kubernetes 101 🚀

we're going to...

* create a deployment called `web` using kubectl
* delete the deployment `web`
* create the deployment `web` using yaml
* create the service `web` using yaml

## Create the deployment `web` using kubectl

```shell
kubectl create deployment web --image=nginx
```

one pod on one worker node. Your first step 🏃‍♀️
let's poke around using kubectl in minikube a little.

Look at:

* the name of the pod
* the yaml that was created `kubectl describe pod <podname>` or use Lens, Loft, or K9s
* what are some conclusions that you can draw? how useful is this pod for example?
* what will happen if we delete the pod?

That's nice...let's delete it. 👋 Let's do something _better_

```shell
kubectl delete deployment web
```

## Create the deployment web using yaml

Next, we'll use yaml files to help us add equity by including more stuff that would be a bummer to try to type out. You could see the value of having this yaml file - check it into GIT and share it.

```shell
kubectl apply -f deployment.yaml
```

* what are some conclusions that you can draw? how useful is creating a deployment vs pods for example?
* what will happen if we delete one of the pods?

While we're here, there is something to go over about service discovery and DNS in K8s networks. You can log in to many containers and do fun things but some you can't because they are without a shell 🐚 Here is a time when being able to stand up an ad-hoc pod is cool and can help you debug.

```shell
kubectl run -it --image=debian:stable-slim bash
```

and now you can test to ensure your pod is working. The IP address of your pod is from `k get pods -o wide`

```shell
curl 10-244-0-9.default.pod.cluster.local:5678 <--- you need to get the ip of a pod. this is just an example.
```

## Create the service using yaml

back onto a local laptop shell, let's create some more k8s abstractions to help us make use of that wonderful deployment.

```shell
kubectl apply -f service.yaml
```

now let's go back to our `debian:stable-slim` container and poke around

```shell
curl web-service:8080
```

should show you a response from one of the pods defined by your deployment. You can scale and the service will automatically be updated to point to the fewer or more pods.
