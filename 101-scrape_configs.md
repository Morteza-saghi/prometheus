### 1. Static Configuration
You manually specify the target(s) in the config.

```
scrape_configs:
  - job_name: 'my_app'
    static_configs:
      - targets: ['localhost:9100', '192.168.1.100:9100']

```

also can be done like this:


```
scrape_configs:
  - job_name: 'my_static_job'
    static_configs:
      - targets:
          - '192.168.1.10:9100'
          - '10.0.0.5:9100'
```

### 2. File-Based Service Discovery
You provide a separate JSON or YAML file that Prometheus watches for target updates.

```
scrape_configs:
  - job_name: 'my_dynamic_targets'
    file_sd_configs:
      - files:
          - 'targets/*.json'
```

Example targets/targets.json:

```
[
  {
    "targets": ["localhost:9100"],
    "labels": {
      "env": "dev"
    }
  }
]

```

### 3. DNS-Based Service Discovery
Prometheus queries a DNS record for a list of targets.

```
scrape_configs:
  - job_name: 'dns_sd'
    dns_sd_configs:
      - names:
          - 'my-service.local'
        type: 'A'
        port: 9100
```

### 4. Consul Service Discovery
If you use Consul for service discovery, Prometheus can query it.

```

scrape_configs:
  - job_name: 'consul_services'
    consul_sd_configs:
      - server: 'localhost:8500'
```

### 5. Kubernetes Service Discovery
Prometheus can discover targets in a Kubernetes cluster.

```
scrape_configs:
  - job_name: 'kubernetes-nodes'
    kubernetes_sd_configs:
      - role: node
```

also we can do this for other Kubernetes roles Like: pod, service, endpoints, ingress

