# Usage

## Installation from Image on minikube

This installation method will use the latest version of the operator image that has been built and published to quay.io.

1. Deploy the custom resource definition (CRD):
```
kubectl apply -f deploy/crds/dobtech.io_qiskitplaygrounds_crd.yaml
```
2. Deploy the RBAC configuration:
```
kubectl apply -f deploy/role.yaml
kubectl apply -f deploy/service_account.yaml
kubectl apply -f deploy/role_binding.yaml
```
3. Deploy the operator itself:
```
kubectl apply -f deploy/operator.yaml
```
4. Wait for the operator pod deployment to complete:
```
watch kubectl get pods
```
5. Deploy an instance of the custom resource:
```
kubectl apply -f deploy/crds/dobtech.io_v1_qiskitplayground_cr.yaml
```
6. Find the node port assigned to the service:
```
kubectl get service/example-playground
```
7. The notebook is found using the minikube IP and the service port from above.
