# Cloud Native Meetup Bern Demo

## Setup

```sh
git clone https://github.com/tim-koko/kubevirt-demo.git
```

1. Create the artefacts before the presentation and only start and observe them

```sh
kubectl create secret generic fedora-vm --from-file=userdata=kubevirt-demo/cloud-native-meetup/cloudinit-userdata-2.yaml --namespace=$USER
kubectl apply -f kubevirt-demo/cloud-native-meetup/svc-ingress.yaml --namespace=$USER
kubectl apply -f kubevirt-demo/cloud-native-meetup/vm.yaml --namespace=$USER
```

## Demo

* go through the secret artefact
* go through the vm artefact
* start the vm

```sh
virtctl start fedora-vm --namespace=$USER
```
* connect to the console and log in

```sh
virtctl console fedora-vm --namespace=$USER
```
* execute curl to verify the running nginx
* explore the service and ingress

## live migration

Terminal 1
```sh
while true; do sleep 1; echo -n `date +"[%H:%M:%S,%3N] "`; echo -n " "; curl --max-time 1 --connect-timeout 0.8 https://cloudnative-meetup.training.cluster.acend.ch/; echo ""; done
```

Terminal 2
```sh
virtctl migrate vm --namespace=$USER
kubectl get vmi -w --namespace=$USER
```

## reset

```sh

kubectl delete secret fedora-vm  --namespace=$USER
kubectl delete -f kubevirt-demo/cloud-native-meetup/vm.yaml --namespace=$USER
kubectl delete -f kubevirt-demo/cloud-native-meetup/svc-ingress.yaml --namespace=$USER
```
