# Cloud Native Meetup Bern Demo

## Setup

```sh
git clone https://github.com/tim-koko/kubevirt-demo.git
```


1. Create cloud init secret

```sh
kubectl create secret generic fedora-vm --from-file=userdata=kubevirt-demo/cloud-native-meetup/cloudinit-userdata-2.yaml --namespace=$USER
```

1. go through the vm artefact
1. create the vm

```sh
kubectl apply -f kubevirt-demo/cloud-native-meetup/vm.yaml --namespace=$USER
```

1. start the vm

```sh
virtctl start fedora-vm --namespace=$USER
```

1. connect to the console and log in

```sh
virtctl console fedora-vm --namespace=$USER
```
execute curl to verify the running nginx

1. create networking

```sh
kubectl apply -f kubevirt-demo/cloud-native-meetup/svc-ingress.yaml --namespace=$USER
```

1. live migrate a vm from one node to an other

Terminal 1
```sh
while true; do sleep 1; echo -n `date +"[%H:%M:%S,%3N] "`; echo -n " "; curl --max-time 1 --connect-timeout 0.8 https://cloudnative-meetup.training.cluster.acend.ch/; echo ""; done
```

Terminal 2
```sh
virtctl migrate vm --namespace=$USER
```
```sh
kubectl get vmi -w --namespace=$USER
```

## reset

```sh

kubectl delete secret fedora-vm  --namespace=$USER
kubectl delete -f kubevirt-demo/cloud-native-meetup/vm.yaml --namespace=$USER
kubectl delete -f kubevirt-demo/cloud-native-meetup/svc-ingress.yaml --namespace=$USER
```
