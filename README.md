# SUT Definition for iCloud 


```console
minikube start --memory=8192 --cpus=4 --kubernetes-version=v1.14.0 --vm-driver=hyperkit \
               --bootstrapper=kubeadm --insecure-registry='docker.apple.com' \
               --extra-config=apiserver.enable-admission-plugins="LimitRanger,NamespaceExists,NamespaceLifecycle,ResourceQuota,ServiceAccount,DefaultStorageClass,MutatingAdmissionWebhook"
```
