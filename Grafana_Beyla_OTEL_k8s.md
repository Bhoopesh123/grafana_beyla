
# 1. Install Prometheus Node Exporter on Minikube Cluster  

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm upgrade --install node-exporter prometheus-community/prometheus-node-exporter

# 2. Install and OpenTelemetry on Minikube Cluster  

    helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts  

    helm upgrade --install my-opentelemetry-collector open-telemetry/opentelemetry-collector -f otel-values.yaml

# 3. Install and Configure Grafana Beyla on cluster for Auto Instrumentation

    helm repo add grafana https://grafana.github.io/helm-charts
    helm upgrade --install beyla grafana/beyla -f helm-beyla-otel.yaml

# 4. Install Application on Minikube cluster    
Please refer the below page to install Prometheus on Cluster: 

    cd app_traces
    kubectl apply -f .

# 5. Validate the metrics on Grafana

To Search all of the time series data points grouping by job  in query  

    count({__name__=~".+"}) by (job)

# 6. Add the Beyla Dashboard  

Add the below dashboard id
    19923