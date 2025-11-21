## **🚀 Beginner-Level Monitoring & Logging Questions (1-20)**  

#### *(Prometheus, Grafana, ELK Stack)*  

### **Prometheus Questions**  

### **1. What is Prometheus, and why is it used?**  

**Answer:**  
Prometheus is an **open-source monitoring and alerting** system used to collect **metrics** from applications and infrastructure. It is widely used because of its **pull-based model**, **powerful query language (PromQL)**, and **time-series database** capabilities.  

Example Use Case:  

- Monitoring **CPU, memory, and network** usage  
- Collecting **application performance metrics**  
- Alerting on high error rates or latency  

---

### **2. How does Prometheus collect data?**  

**Answer:**  
Prometheus **pulls metrics** from target endpoints exposed via HTTP at `/metrics`. The targets can be defined in a static configuration or discovered dynamically (e.g., Kubernetes service discovery).  

Example scrape configuration (`prometheus.yml`):  

```yaml
scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```

---

### **3. What is PromQL?**  

**Answer:**  
PromQL (Prometheus Query Language) is used to **query and analyze** metrics stored in Prometheus. It enables users to create alerts, dashboards, and graphs.  

Example Queries:  

- **CPU usage:**  

  ```promql
  node_cpu_seconds_total{mode="user"} / sum(node_cpu_seconds_total) * 100
  ```

- **Request rate:**  

  ```promql
  rate(http_requests_total[5m])
  ```

---

### **4. What are Prometheus exporters?**  

**Answer:**  
Exporters are **agents** that collect and expose metrics from various applications and systems.  

Common Exporters:  

- **Node Exporter** (system metrics)  
- **Blackbox Exporter** (network probes)  
- **MySQL Exporter** (database metrics)  

---

### **5. How do you set up an alert in Prometheus?**  

**Answer:**  
Alerts are configured in `alerting_rules.yml` and evaluated by the **Alertmanager**.  

Example Rule:  

```yaml
groups:
  - name: instance_down
    rules:
      - alert: InstanceDown
        expr: up == 0
        for: 5m
        labels:
          severity: critical
        annotations:
          description: "Instance {{ $labels.instance }} is down."
```

---

### **Grafana Questions**  

### **6. What is Grafana?**  

**Answer:**  
Grafana is an **open-source analytics and visualization** tool used to create **interactive dashboards** for monitoring data from **Prometheus, ELK, and other sources**.  

---

### **7. How do you connect Grafana to Prometheus?**  

**Answer:**  

1. **Login to Grafana** (`http://localhost:3000`).  
2. Navigate to **"Configuration" → "Data Sources"**.  
3. Select **Prometheus** as the data source.  
4. Enter **Prometheus URL (`http://localhost:9090`)**.  
5. Click **Save & Test**.  

---

### **8. What are Grafana Panels?**  

**Answer:**  
Panels are **visual components** in Grafana used to display data in various formats:  

- **Graph Panel:** Time-series data visualization  
- **Single Stat Panel:** Displays a single numeric value  
- **Table Panel:** Tabular data display  

---

### **9. How do you create alerts in Grafana?**  

**Answer:**  

1. Select a **panel**.  
2. Click **"Edit" → "Alert"**.  
3. Define a condition using **PromQL queries**.  
4. Set the evaluation interval (e.g., every **1m**).  
5. Configure the alert notification (Slack, Email, etc.).  

---

### **10. How do you configure a Grafana dashboard using JSON?**  

**Answer:**  
Export and import dashboards using JSON files.  

Example JSON snippet:  

```json
{
  "panels": [
    {
      "type": "graph",
      "title": "CPU Usage",
      "targets": [
        { "expr": "node_cpu_seconds_total", "format": "time_series" }
      ]
    }
  ]
}
```

---

### **ELK Stack Questions (Elasticsearch, Logstash, Kibana)**  

### **11. What is the ELK Stack?**  

**Answer:**  
The ELK Stack consists of:  

- **Elasticsearch** (search and analytics engine)  
- **Logstash** (log processing pipeline)  
- **Kibana** (visualization tool)  

---

### **12. What is the role of Elasticsearch in ELK?**  

**Answer:**  
Elasticsearch is a **NoSQL, distributed search engine** used to store, search, and analyze log data.  

---

### **13. How does Logstash work?**  

**Answer:**  
Logstash processes logs using a **pipeline**:  

- **Input:** Reads logs (from files, databases, Kafka, etc.)  
- **Filter:** Transforms logs (parse JSON, remove sensitive data)  
- **Output:** Sends logs to Elasticsearch or other storage  

Example Logstash Configuration:  

```yaml
input { file { path => "/var/log/syslog" } }
filter { grok { match => { "message" => "%{SYSLOGTIMESTAMP:timestamp}" } } }
output { elasticsearch { hosts => ["localhost:9200"] } }
```

---

### **14. What is Kibana used for?**  

**Answer:**  
Kibana is used to **visualize and explore log data** stored in Elasticsearch. It provides features like:  

- **Dashboards:** Custom data visualizations  
- **Discover:** Search raw logs  
- **Alerts:** Set up log-based alerts  

---

### **15. How do you install the ELK stack?**  

**Answer:**  
Install Elasticsearch, Logstash, and Kibana:  

```sh
# Install Elasticsearch
sudo apt install elasticsearch

# Install Logstash
sudo apt install logstash

# Install Kibana
sudo apt install kibana
```

Start services:  

```sh
sudo systemctl start elasticsearch logstash kibana
```

---

### **16. What is an Index in Elasticsearch?**  

**Answer:**  
An index in Elasticsearch is like a **database table** that stores documents.  

Example:  

```sh
curl -X PUT "localhost:9200/logs"
```

---

### **17. How do you send logs from Logstash to Elasticsearch?**  

**Answer:**  
Define an **output plugin** in Logstash configuration:  

```yaml
output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "logs-%{+YYYY.MM.dd}"
  }
}
```

---

### **18. What is a Kibana Visualization?**  

**Answer:**  
A Kibana Visualization is a **graph, chart, or table** displaying log data.  

Example Visualizations:  

- **Bar Chart** (Logs per hour)  
- **Pie Chart** (Error types distribution)  
- **Line Chart** (CPU usage over time)  

---

### **19. What is Filebeat?**  

**Answer:**  
Filebeat is a lightweight log shipper that **forwards logs to Logstash or Elasticsearch**.  

Example Filebeat Configuration:  

```yaml
filebeat.inputs:
  - type: log
    paths:
      - "/var/log/syslog"
output.elasticsearch:
  hosts: ["localhost:9200"]
```

---

### **20. What is the difference between Logstash and Filebeat?**  

**Answer:**  

- **Logstash:** Heavyweight, processes logs with complex transformations  
- **Filebeat:** Lightweight, only forwards logs with minimal processing  

---

## **🚀 Intermediate-Level Monitoring & Logging Questions (21-40)**  

#### *(Prometheus, Grafana, ELK Stack)*  

### **Prometheus Questions**  

### **21. What is the difference between Pull and Push monitoring models?**  

**Answer:**  

- **Pull Model (Prometheus)** → The monitoring system **requests data** from targets at regular intervals.  
- **Push Model (StatsD, InfluxDB)** → The target system **sends data** to a central monitoring system.  

**Prometheus uses a pull model** because it provides better control over scraping intervals, avoids data duplication, and reduces unnecessary load on monitored systems. However, in some cases (e.g., short-lived jobs), Prometheus **Pushgateway** can be used to support push-based metrics.  

---

### **22. How does Prometheus handle high-cardinality data?**  

**Answer:**  
Prometheus stores time-series data efficiently, but **high-cardinality metrics (many unique label combinations)** can cause excessive memory and storage usage. Best practices include:  

- **Avoid unnecessary labels** (e.g., `user_id` or `request_id`).  
- **Use histograms and summaries** instead of tracking individual events.  
- **Enable retention policies and downsampling** for old data.  

---

### **23. What are Recording Rules in Prometheus?**  

**Answer:**  
Recording Rules allow precomputing and storing frequently used queries as new time-series metrics. This improves query performance.  

Example:  

```yaml
groups:
  - name: response_time_rules
    rules:
      - record: instance:response_time:avg
        expr: avg(rate(http_request_duration_seconds[5m]))
```

This stores the average request duration as `instance:response_time:avg`, making future queries faster.  

---

### **24. What is Thanos, and how does it complement Prometheus?**  

**Answer:**  
Thanos extends Prometheus for **scalability, long-term storage, and high availability**. It:  

- **Provides deduplication** across multiple Prometheus instances.  
- **Enables object storage support** (e.g., S3, GCS).  
- **Allows querying across multiple Prometheus servers** via a single query layer.  

Thanos is useful in **multi-cluster environments** where Prometheus instances are spread across multiple regions or clouds.  

---

### **25. How do you handle Prometheus high availability (HA)?**  

**Answer:**  
Prometheus is a single-node system by design, but HA can be achieved by:  

- **Running multiple Prometheus replicas** (scraping the same targets).  
- Using **Thanos or Cortex** for deduplication and query federation.  
- **Storing time-series data externally** (e.g., in S3, Bigtable).  

---

### **Grafana Questions**  

### **26. How do you enable authentication in Grafana?**  

**Answer:**  
Grafana supports **multiple authentication methods**:  

- **Basic authentication** (default).  
- **OAuth providers** (Google, GitHub, Azure AD, etc.).  
- **LDAP authentication** for enterprise use.  

To enable OAuth authentication, modify `grafana.ini`:  

```ini
[auth.github]
enabled = true
client_id = YOUR_CLIENT_ID
client_secret = YOUR_CLIENT_SECRET
```

---

### **27. What are Templating Variables in Grafana?**  

**Answer:**  
Templating allows users to create **dynamic dashboards** by using variables. Instead of hardcoding values, users can select values from dropdown menus.  

Example:  

```promql
rate(http_requests_total{job="$service"}[5m])
```

Here, `$service` is a variable that can be selected from a dropdown list in Grafana.  

---

### **28. How do you set up Grafana provisioning?**  

**Answer:**  
Grafana supports **automated provisioning** of dashboards and data sources using YAML configuration files.  

Example `datasource.yaml`:  

```yaml
apiVersion: 1
datasources:
  - name: Prometheus
    type: prometheus
    url: http://prometheus:9090
    access: proxy
```

---

### **29. What are Grafana Loki and Promtail?**  

**Answer:**  

- **Loki** is Grafana's log aggregation system, similar to Elasticsearch but optimized for Kubernetes and microservices.  
- **Promtail** is the log collection agent for **pushing logs to Loki**.  

Promtail collects logs from `/var/log` and forwards them to Loki.  

---

### **30. How can you monitor Kubernetes with Grafana?**  

**Answer:**  
Use **kube-prometheus-stack**, which includes:  

- **Prometheus Operator** (for Kubernetes metrics).  
- **Grafana dashboards** for cluster monitoring.  
- **Node Exporter and Kube-State-Metrics** for detailed node/pod-level metrics.  

---

### **ELK Stack Questions (Elasticsearch, Logstash, Kibana)**  

### **31. What is an Elasticsearch Shard, and why is it important?**  

**Answer:**  
An Elasticsearch **shard** is a **subdivision of an index**. Each index is split into shards to allow parallel processing and redundancy.  

- **Primary Shards:** Store original data.  
- **Replica Shards:** Duplicates of primary shards for fault tolerance.  

Example:  

```sh
curl -X PUT "localhost:9200/logs?pretty" -H 'Content-Type: application/json' -d'
{
  "settings": { "number_of_shards": 3, "number_of_replicas": 2 }
}'
```

This creates an index with **3 primary and 2 replica shards**.  

---

### **32. What is Index Lifecycle Management (ILM) in Elasticsearch?**  

**Answer:**  
ILM automates **index retention policies**, ensuring efficient storage use. Stages include:  

1. **Hot Phase:** Frequent reads/writes.  
2. **Warm Phase:** Less frequent queries.  
3. **Cold Phase:** Rarely accessed data.  
4. **Delete Phase:** Data deletion.  

ILM is useful for managing **log retention** in ELK stacks.  

---

### **33. How do you configure Logstash pipelines?**  

**Answer:**  
Logstash uses a pipeline of **input → filter → output**.  

Example `logstash.conf`:  

```yaml
input {
  beats {
    port => 5044
  }
}
filter {
  grok { match => { "message" => "%{TIMESTAMP_ISO8601:timestamp}" } }
}
output {
  elasticsearch { hosts => ["localhost:9200"] }
}
```

This pipeline processes logs from **Filebeat → Logstash → Elasticsearch**.  

---

### **34. What are Kibana Canvas and Lens?**  

**Answer:**  

- **Canvas** → Used for creating custom, highly stylized reports and presentations.  
- **Lens** → Drag-and-drop interface for creating advanced visualizations easily.  

---

### **35. How do you configure Kibana security?**  

**Answer:**  
Enable authentication in `kibana.yml`:  

```yaml
xpack.security.enabled: true
elasticsearch.username: "kibana"
elasticsearch.password: "changeme"
```

Use **role-based access control (RBAC)** to restrict access.  

---

### **36. What is Beats in the ELK stack?**  

**Answer:**  
Beats are **lightweight data shippers** for sending logs, metrics, and security data to ELK.  

- **Filebeat:** Log shipping.  
- **Metricbeat:** System metrics.  
- **Packetbeat:** Network monitoring.  

---

### **37. What is Curator in Elasticsearch?**  

**Answer:**  
Curator is a tool for **managing Elasticsearch indices**, used for deleting old indices, snapshot backups, and optimizing performance.  

---

### **38. How do you integrate Prometheus and ELK Stack?**  

**Answer:**  
Use **Metricbeat** to collect system metrics and send them to **Elasticsearch**, while **Prometheus Node Exporter** collects Prometheus-compatible metrics.  

---

### **39. What is a Slow Query in Elasticsearch?**  

**Answer:**  
A **slow query** is a query that takes too long to execute, often due to large data scans or missing indexes. Enable slow query logs to debug:  

```sh
PUT _settings
{
  "index.search.slowlog.threshold.query.warn": "2s"
}
```

---

### **40. What is the ELK alternative to Prometheus and Grafana?**  

**Answer:**  

- **Prometheus + Grafana** → Metrics-based monitoring.  
- **ELK Stack (Elasticsearch, Logstash, Kibana)** → Log-based monitoring.  
- Alternative: **OpenTelemetry**, **Loki**, and **InfluxDB**.  

---

## **🚀 Advanced-Level Monitoring & Logging Questions (41-60)**  

#### *(Prometheus, Grafana, ELK Stack)*  

---

### **Prometheus Questions**  

### **41. How do you scale Prometheus for a large environment?**  

**Answer:**  
Prometheus is a **single-node** system, so for large environments:  

- **Use multiple Prometheus instances** scraping different targets.  
- **Federation:** Create a parent Prometheus that scrapes **aggregated** metrics from child Prometheus instances.  
- **Remote storage:** Use **Thanos, Cortex, or Mimir** to store metrics in scalable object storage (S3, GCS).  
- **Sharding:** Distribute scraping targets across Prometheus instances using load balancing tools like **Kube StatefulSets**.  

---

### **42. How does Prometheus handle stale or missing metrics?**  

**Answer:**  

- **Stale markers:** Prometheus marks time-series data as **stale** if a target stops reporting metrics.  
- **Absent function (`absent()`)**: Used in PromQL to detect missing metrics.  
- **Dead Man’s Switch**: A constant alert (e.g., `ALWAYS_ON`) ensures the alerting system is functional.  

Example:  

```promql
absent(up{job="my_service"})
```

Triggers an alert if `up{job="my_service"}` is missing.  

---

### **43. What is Prometheus WAL (Write-Ahead Log) and its purpose?**  

**Answer:**  
The **Write-Ahead Log (WAL)** in Prometheus:  

- **Stores data on disk before committing it to TSDB (Time-Series Database).**  
- Reduces data loss during crashes.  
- WAL files are stored in **/data/wal/** and help recover metrics quickly after a restart.  

---

### **44. What are Histogram and Summary metrics in Prometheus?**  

**Answer:**  
Both are used for measuring **latency and response time**:  

- **Histogram:** Buckets data into **predefined ranges**, allowing percentiles to be calculated later.  
- **Summary:** Precomputes percentiles but cannot be aggregated across instances.  

Example (Histogram metric):  

```promql
histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))
```

This calculates the **95th percentile response time**.  

---

### **45. How do you secure Prometheus endpoints?**  

**Answer:**  

- **Enable authentication & TLS** via a reverse proxy (Nginx, Traefik).  
- **Use RBAC (Role-Based Access Control)** in Kubernetes for limiting access.  
- **Set up network policies** to restrict Prometheus access.  

Example: Using basic auth with Nginx:  

```nginx
server {
  listen 9090;
  location / {
    auth_basic "Restricted";
    auth_basic_user_file /etc/nginx/.htpasswd;
  }
}
```

---

### **Grafana Questions**  

### **46. How do you monitor Prometheus itself using Grafana?**  

**Answer:**  

- Enable the built-in Prometheus **self-metrics endpoint (`/metrics`)**.  
- Use dashboards to monitor **scrape latency, TSDB memory usage, query duration**.  
- Use the **Prometheus Federation API** to get meta-metrics.  

---

### **47. What are Grafana Annotations and how are they useful?**  

**Answer:**  
Annotations mark **events (deployments, incidents, downtimes)** on Grafana graphs for better visualization.  
Example: Mark a **Kubernetes deployment** event in Grafana.  

---

### **48. How do you configure Grafana for multi-tenancy?**  

**Answer:**  

- **Organizations:** Create multiple teams with separate dashboards.  
- **Data source permissions:** Restrict access at the **data-source level**.  
- **Multi-instance deployment:** Run **separate Grafana instances** for different teams.  

---

### **49. What is Alerting in Grafana and how does it work?**  

**Answer:**  

- **Grafana alerts** monitor query conditions.  
- Alert states: **OK, Pending, Alerting, No Data**.  
- **Notification channels:** Slack, PagerDuty, Email, Webhooks.  

Example Grafana alert condition:  

- `avg(http_requests_total) > 1000` → Sends an alert if requests exceed 1000.  

---

### **50. How does Loki compare with Elasticsearch for logging?**  

**Answer:**  

| Feature  | Loki | Elasticsearch |  
|----------|------|--------------|  
| Storage  | Compressed logs | Full-text index |  
| Querying | Label-based | Query DSL |  
| Performance | Faster (optimized for Kubernetes) | Heavy resource usage |  

**Loki is recommended for lightweight, Kubernetes-native logging**, while **Elasticsearch is better for complex log analysis**.  

---

### **ELK Stack Questions**  

### **51. What is the Hot-Warm-Cold architecture in Elasticsearch?**  

**Answer:**  
This strategy optimizes storage cost:  

- **Hot Nodes** → Store recent, frequently queried data.  
- **Warm Nodes** → Store older logs with infrequent access.  
- **Cold Nodes** → Store archived logs for long-term retention.  

---

### **52. How do you reduce indexing pressure in Elasticsearch?**  

**Answer:**  

- **Use ILM (Index Lifecycle Management).**  
- **Optimize shard count** (Avoid too many small shards).  
- **Increase refresh intervals (`index.refresh_interval: 30s`).**  

---

### **53. How does Logstash manage backpressure?**  

**Answer:**  

- **Persistent Queues** → Buffer data before sending to Elasticsearch.  
- **Dead Letter Queue (DLQ)** → Stores failed events for reprocessing.  

Example:  

```yaml
queue.type: persisted
queue.max_bytes: 1gb
```

---

### **54. What are Query Caching strategies in Elasticsearch?**  

**Answer:**  

- **Request cache:** Stores query results.  
- **Shard request cache:** Caches **aggregations and filters**.  
- **Doc value cache:** Optimizes **sorting and aggregations**.  

---

### **55. How do you use Kibana for anomaly detection?**  

**Answer:**  

- **Machine Learning Jobs** → Identify unusual trends in logs.  
- **SIEM (Security Information and Event Management)** → Detect security threats.  

Example anomaly detection job:  

```json
{
  "analysis_config": {
    "bucket_span": "15m",
    "detectors": [{ "function": "mean", "field_name": "cpu_usage" }]
  }
}
```

---

### **56. How do you secure Elasticsearch clusters?**  

**Answer:**  

- **Enable TLS (`xpack.security.enabled: true`).**  
- **Use API Key authentication.**  
- **Implement firewall rules to restrict access.**  

---

### **57. How do you integrate Prometheus with Elasticsearch?**  

**Answer:**  

- Use **Metricbeat** to push Prometheus data into **Elasticsearch**.  
- Use **Grafana to visualize both Prometheus & ELK logs.**  

Example Metricbeat configuration:  

```yaml
metricbeat.modules:
  - module: prometheus
    metricsets: ["collector"]
    host: "localhost:9090"
```

---

### **58. How do you optimize Elasticsearch queries for performance?**  

**Answer:**  

- **Use filters (`term`, `match_phrase`) instead of full-text search.**  
- **Avoid wildcard (`*`) searches.**  
- **Use `doc_values` for sorting and aggregations.**  

---

### **59. How do you implement centralized logging in Kubernetes?**  

**Answer:**  

- **Use Fluentd/Filebeat** to collect logs.  
- **Send logs to Elasticsearch or Loki.**  
- **Monitor logs via Kibana or Grafana dashboards.**  

Example Fluentd configuration:  

```yaml
<match kubernetes.**>
  @type elasticsearch
  host elasticsearch
  logstash_format true
</match>
```

---

### **60. What are the best practices for log retention and compliance?**  

**Answer:**  

- **Use ILM to delete old logs automatically.**  
- **Encrypt sensitive logs (`xpack.security`).**  
- **Mask PII data before indexing logs.**  
- **Set audit logs for security compliance.**  

---

## **📢 Contribute & Stay Updated**  

💡 **Want to contribute?**  
We **welcome contributions!** If you have insights, new tools, or improvements, feel free to submit a **pull request**.  

📌 **How to Contribute?**

- Read the **[CONTRIBUTING.md](https://github.com/abhilash/DevOps-Interview-Questions/blob/master/CONTRIBUTING.md)** guide.  
- Fix errors, add missing topics, or suggest improvements.  
- Submit a **pull request** with your updates.  

📢 **Stay Updated:**  
⭐ **Star the repository** to get notified about new updates and additions.  
💬 **Join discussions** in **[GitHub Issues](https://github.com/abhilash/DevOps-Interview-Questions/issues)** to suggest improvements.  

---

## **🌍 Community & Support**  

🔗 **GitHub:** [@abhilash](https://github.com/abhilash)  
📝 **Blog:** [ProDevOpsGuy](https://blog.prodevopsguy.xyz)  
💬 **Telegram Community:** [Join Here](https://t.me/prodevopsguy)  

