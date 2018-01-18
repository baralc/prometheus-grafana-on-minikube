# Prometheus-workshop

## Setup 

1. Install kubectl (https://kubernetes.io/docs/tasks/tools/install-kubectl/)
  * On MacOs: `brew install kubectl`

2. Install minikube ([https://github.com/kubernetes/minikube]()).
  * On MacOs `brew cask install minikube`

3. Add aliases to /ect/hosts for simple access:
  * Determine actual ip with `minikube ip`

```
192.168.99.100  minikube.local
192.168.99.100  prometheus.local
192.168.99.100  alertmanager.local
192.168.99.100  grafana.local
```

4. Install helm ([https://docs.helm.sh/using_helm/#installing-helm]())
  * On MacOs `brew install kubernetes-helm`
  * Install helm on the minikube: `helm init`

5. Install/Deploy Prometheus on Minikube:
  * `helm install -n monitoring -f prometheus/values.yaml ./prometheus`

6. Install Grafana ([https://grafana.com/grafana]())
  * `helm install -n grafana -f grafana/values.yaml stable/grafana`
  * get the password for admin: `kubectl get secret --namespace default grafana-grafana -o jsonpath="{.data.grafana-admin-password}" | base64 --decode ; echo`

7. Configure Prometheus as datasource for Grafana:
  * Open [http://grafana.local]() 
  * Click on `Add Datasource`
  	* give it a name
	* select `Type`: `Prometheus` 
	* add Url `http://prometheus.local`
	* select `Access`: `direct`
	* Click `Add`



### Some helpful Notes:
Force reload prometheus config:
`curl -X POST http://prometheus.local/-/reload`

