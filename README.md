# logstack

This `docker-compose.yml` file defines a Docker stack for a logging and monitoring system, composed of the following services:

- Loki: A horizontally scalable, highly available, multi-tenant log aggregation system. It allows you to store, query, and visualize logs from various data sources.
- Promtail: A log collector and processor that integrates with Loki. It can collect logs from various sources and enrich them with labels, which can be used for filtering and querying in Loki.
- Prometheus: A time-series database and monitoring system. It can scrape metrics from various sources, store them in its database, and display them in a web interface.
- cAdvisor: A container monitoring tool. It can collect metrics about the resource usage and performance of Docker containers and their hosts.
- node-exporter: A Prometheus exporter that collects metrics about the system and exports them in the Prometheus format. It can collect various system-level metrics such as CPU, memory, disk usage, and network traffic.
- Grafana: A web-based dashboard and visualization tool which can be used to visualize and analyze metrics from Prometheus, Loki, and other data sources.

With this setup, you can collect logs and metrics from various sources, store them in Loki and Prometheus, and visualize and analyze them in Grafana. This can be useful for monitoring the health and performance of your system, troubleshooting issues, and gaining insights into your applications.

Some common use cases for this setup include:

- Monitoring the health and performance of Kubernetes clusters and applications
- Monitoring the health and performance of Docker containers and hosts
- Collecting and analyzing logs and metrics from microservices architectures
- Troubleshooting issues in distributed systems
- Analyzing user behavior and application usage patterns

The directory tree is as follows:

```
logstack/
├── cadvisor
│   ├── config
│   └── ...
├── grafana
│   └── provisioning
│       ├── dashboards
│       ├── datasources
│       └── ...
├── loki
│   ├── config
│   └── data
├── node-exporter
├── prometheus
│   ├── prometheus.yml
│   └── ...
├── promtail
│   ├── config
│   └── ...
└── docker-compose.yml
```

The compose file exposes (internal to stack) the following ports:

- Loki: port `3100`
- Promtail: port `9080`
- Prometheus: port `9090`
- cAdvisor: port `8080`
- Node Exporter: port `9100`

And one host published port (external to stack) :
- Grafana: port `3000`

To deploy, create the parent directory:
`mkdir logstack`

Deploy using `docker compose` from the `logstack` directory:

`cd logstack`

`docker compose up -d`

Update by recreating and rebuilding clean:

`docker compose up -d --force-recreate --build`
