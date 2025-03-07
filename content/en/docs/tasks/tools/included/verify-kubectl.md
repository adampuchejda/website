---
title: "verify kubectl install"
description: "How to verify kubectl."
headless: true
_build:
  list: never
  render: never
  publishResources: false
---

In order for kubectl to find and access a Kubernetes cluster, it needs a
[kubeconfig file](/docs/concepts/configuration/organize-cluster-access-kubeconfig/),
which is created automatically when you create a cluster using
[kube-up.sh](https://github.com/kubernetes/kubernetes/blob/master/cluster/kube-up.sh)
or successfully deploy a Minikube cluster.
By default, kubectl configuration is located at `~/.kube/config`.

Check that kubectl is properly configured by getting the cluster state:

```shell
kubectl cluster-info
```

If you see a URL response, kubectl is correctly configured to access your cluster.

If you see a message similar to the following, kubectl is not configured correctly or is not able to connect to a Kubernetes cluster.

```
The connection to the server <server-name:port> was refused - did you specify the right host or port?
```

For example, if you are intending to run a Kubernetes cluster on your laptop (locally), you will need a tool like Minikube to be installed first and then re-run the commands stated above.

If kubectl cluster-info returns the url response but you can't access your cluster, to check whether it is configured properly, use:

```shell
kubectl cluster-info dump
```

### Troubleshooting the 'No Auth Provider Found' error message {#no-auth-provider-found}

In Kubernetes 1.26, kubectl removed the built-in authentication for the following cloud
providers' managed Kubernetes offerings. These providers have released kubectl plugins to provide the cloud-specific authentication. For instructions, refer to the following provider documentation:

* Azure  AKS: [kubelogin plugin](https://azure.github.io/kubelogin/)
* Google Kubernetes Engine: [gke-gcloud-auth-plugin](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl#install_plugin)

(There could also be other reasons to see the same error message, unrelated to that change.)
