# TME : Prometheus

### Exercise 1: Deploying Prometheus Manually
#### Objectives:
- Deploy Prometheus on Kubernetes without using Helm charts.
- Configure Prometheus to monitor Kubernetes cluster components.

#### Tasks:
1. **Create Prometheus Configuration**:
    - Write a Prometheus configuration file (`prometheus.yml`) to specify scrape targets.
    - Use a ConfigMap to store the Prometheus configuration in Kubernetes.

2. **Deploy Prometheus**:
    - Create a Kubernetes deployment for Prometheus using a Docker Prometheus image.
    - Expose Prometheus using a Kubernetes service (NodePort or LoadBalancer).

3. **Verify Prometheus Deployment**:
    - Access the Prometheus UI through the exposed service to verify it's running.

### Exercise 2: Deploying Grafana Manually
#### Objectives:
- Deploy Grafana on Kubernetes without using Helm charts.
- Configure Grafana to use Prometheus as a data source.

#### Tasks:
1. **Deploy Grafana**:
    - Create a Kubernetes deployment for Grafana using the official Grafana Docker image.
    - Expose Grafana using a Kubernetes service (NodePort or LoadBalancer).

2. **Configure Grafana**:
    - Access the Grafana UI through the exposed service.
    - Add Prometheus as a data source within Grafana.
    - Import or create a dashboard to visualize metrics from Prometheus.

### Exercise 3: Monitoring Cluster Components
#### Objectives:
- Utilize Prometheus and Grafana to monitor Kubernetes cluster components.
- Create alerts based on specific metrics thresholds.

#### Tasks:
1. **Create Monitoring Targets**:
    - Configure Prometheus to scrape metrics from Kubernetes system components (e.g., kubelet, kube-apiserver).

2. **Visualize Metrics in Grafana**:
    - Create or import dashboards in Grafana to visualize Kubernetes metrics.
    - Use the query editor to display specific metrics like CPU and memory usage.

3. **Configure Alerts**:
    - Set up alert rules in Prometheus for critical metrics thresholds.
    - Configure Grafana to send notifications based on the alerts triggered by Prometheus.