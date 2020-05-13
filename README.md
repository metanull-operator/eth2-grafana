# eth2-grafana
Grafana dashboards for Eth2. This dashboard was written and tested for use with Prysm.

Single source version is for users with a single instance of Prometheus, a single beacon chain, and a single validator. Multiple source version uses variables to allow selection of Prometheus source, beacon chain source, validator source, and host/server source.

![Eth2 Grafana Dashboard for Multiple Sources](https://raw.githubusercontent.com/metanull-operator/eth2-grafana/master/images/eth2-grafana-dashboard-multiple-sources.png)

Host stats require Prometheus node_exporter.

Sample Prometheus configuration for node_exporter:
```
  - job_name: 'node_exporter_beacon01'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
```

Ping requires Prometheus blackbox_exporter.

Sample prometheus configuration for mulitple pings using blackbox_exporter:
```
  - job_name: 'beacon01_ping_google'
    metrics_path: /probe
    params:
      module: [icmp]
    static_configs:
            - targets:
              - 8.8.8.8
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 127.0.0.1:9115  # The blackbox exporter's real hostname:port.
  - job_name: 'beacon01_ping_cloudflare'
    metrics_path: /probe
    params:
      module: [icmp]
    static_configs:
            - targets:
              - 1.1.1.1
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 127.0.0.1:9115  # The blackbox exporter's real hostname:port.
  - job_name: 'beacon01_ping_centurylink'
    metrics_path: /probe
    params:
      module: [icmp]
    static_configs:
            - targets:
              - XXX.XXX.XXX.XXX
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 127.0.0.1:9115  # The blackbox exporter's real hostname:port.
```

Sample blackbox_exporter configuration for pings:
```
modules:
        icmp:
                prober: icmp
                timeout: 5s
                icmp:
                        preferred_ip_protocol: ipv4
```
