# eth2-grafana
Grafana dashboards for Eth2. This dashboard was written and tested for use with Prysm.

Single source version is for users with a single instance of Prometheus, a single beacon chain, and a single validator. Multiple source version uses variables to allow selection of Prometheus source, beacon chain source, validator source, and host/server source.

![Eth2 Grafana Dashboard for Multiple Sources](https://raw.githubusercontent.com/metanull-operator/eth2-grafana/master/images/eth2-grafana-dashboard-multiple-sources.png)

Host stats require Prometheus node_exporter.

Ping requires Prometheus blackbox_exporter.
