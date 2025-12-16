# sbomer-platform
Helm Chart for the SBOMer Platform

## How to run locally

- First, make sure Tekton is install on the minikube cluster we install this chart on
- Build the dependencies:
```script
helm dependency update ./
```
- Then install the helm chart with devProfile=true to make sure that Kafka and Apicurio get set up in the cluster:
```script
helm install sbomer-release ./ --set global.includeKafka=true --set global.includeApicurio=true --set global.includeApiGateway=true
```
- Then once all the pods are running, port-forward the api gateway:
```script
kubectl port-forward svc/sbomer-release-gateway 8080:8080 (leave open in terminal)
```
- We can now go into the sbom-service API to trigger a generation:
```script
http://localhost:8080/q/swagger-ui/#/Generation%20Resource/post_api_v1_generations
```