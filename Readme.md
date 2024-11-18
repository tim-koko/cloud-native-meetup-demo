# Cloud Native Meetup Bern Demo

Setup
```sh
git clone https://github.com/tim-koko/kubevirt-demo.git
```

1. Create cloud init secret

```sh
kubectl create secret generic cloud-native-meetup --from-file=userdata=kubevirt-demo/cloud-native-meetup/cloudinit-userdata-2.yaml --namespace=$USER
```

1. go through the vm artefact
1. create the vm

```sh
kubectl apply -f kubevirt-demo/cloud-native-meetup/vm.yaml --namespace=$USER
```

1. start the vm

```sh
virtctl start cloud-native-meetup-vm --namespace=$USER
```

1. connect to the console and log in

```sh
virtctl console cloud-native-meetup-vm --namespace=$USER
```

1. create networking

```sh
kubectl apply -f kubevirt-demo/cloud-native-meetup/svc-ingress.yaml --namespace=$USER
```



## reset

```sh

kubectl delete secret cloud-native-meetup --namespace=$USER
kubectl delete -f kubevirt-demo/cloud-native-meetup/vm.yaml --namespace=$USER
kubectl delete -f kubevirt-demo/cloud-native-meetup/svc-ingress.yaml --namespace=$USER
```
