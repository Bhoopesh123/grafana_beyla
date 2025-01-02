
# 1. Install Prometheus Node Exporter on Minikube Cluster  

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm install node-exporter prometheus-community/prometheus-node-exporter

# 2. Install and Configure Alloy on Minikube Cluster  

Make sure to update the node_exporter service ip in alloy configuration in configmap.alloy file before creating configmap

    kubectl create configmap --namespace opentelemetry-demo alloy-config "--from-file=config_k8s_beyla.alloy=./config_k8s_beyla.alloy"

    helm  upgrade --install --namespace opentelemetry-demo alloy grafana/alloy -f beyla_k8s_values.yaml

# 3. Install and Configure Grafana Beyla on cluster  

    helm repo add grafana https://grafana.github.io/helm-charts
    helm upgrade --install beyla grafana/beyla -f helm-beyla.yaml


# 4. Install Application on Minikube cluster    
Please refer the below page to install Prometheus on Cluster: 

    cd app_logs 
    kubectl apply -f .

# 5. Install nginx application on Minikube cluster    
Please refer the below page to install Prometheus on Cluster: 

    kubectl apply -f nginx_deployment.yaml

# 6. Validate the metrics on Grafana

To Search all of the time series data points grouping by job  in query  

    count({__name__=~".+"}) by (job)

# 7. Add the Beyla Dashboard  

Add the below dashboard id
    19923