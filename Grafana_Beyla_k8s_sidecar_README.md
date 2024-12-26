
# 1. Install Prometheus Node Exporter on Minikube Cluster  

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm install node-exporter prometheus-community/prometheus-node-exporter

# 2. Install and Configure Alloy on Minikube Cluster  

Make sure to update the node_exporter service ip in alloy configuration in configmap.alloy file before creating configmap

    kubectl create configmap --namespace opentelemetry-demo alloy-config "--from-file=config_k8s_beyla.alloy=./config_k8s_beyla.alloy"
    helm  upgrade --install --namespace opentelemetry-demo alloy grafana/alloy -f beyla_k8s_values.yaml

# 3. Install and Configure Grafana Beyla on cluster  

    cd sidecar
    kubectl apply -f .

# 5. Validate the metrics on Grafana

To Search all of the time series data points grouping by job  in query  

    count({__name__=~".+"}) by (job)

# 6. Add the Beyla Dashboard  

Add the below dashboard id
    19923