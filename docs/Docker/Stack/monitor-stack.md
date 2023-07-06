# Monitor 集群监视服务

## 准备工作

创建配置文件

=== "Docker stack 配置文件"

    ```yaml title='monitor-stack.yml'
    version: "3.9"

    services:
      cadvisor:
        image: gcr.io/cadvisor/cadvisor
        networks:
          - exporter_network
        volumes:
          - /var/run/docker.sock:/tmp/docker.sock:ro
          - /:/rootfs:ro
          - /var/run:/var/run:ro
          - /sys:/sys:ro
          - /var/lib/docker/:/var/lib/docker:ro
          - /dev/disk/:/dev/disk:ro
        command:
          - --docker_only=true
        deploy:
          mode: global

      prometheus:
        image: prom/prometheus
        user: root
        networks:
          - exporter_network
          - proxy_network
        # ports:
        #   - 9090:9090
        volumes:
          - prometheus_data:/prometheus
        command:
          - --storage.tsdb.retention.time=30d
        deploy:
          mode: replicated
          replicas: 1
          placement:
            constraints: [node.role == manager]
          labels:
            - traefik.enable=true
            - traefik.http.routers.prometheus.entryPoints=web
            - traefik.http.routers.prometheus.rule=HostRegexp(`{host:^prometheus.*}`)
            - traefik.http.services.prometheus.loadbalancer.server.port=9090

      grafana:
        image: grafana/grafana
        user: root
        networks:
          - exporter_network
          - proxy_network
        # ports:
        #   - 3000:3000
        volumes:
          - grafana_data:/var/lib/grafana
        environment:
          - GF_AUTH_ANONYMOUS_ENABLED=true
        deploy:
          mode: replicated
          replicas: 2
          # placement:
          #   constraints: [node.role == manager]
          labels:
            - traefik.enable=true
            - traefik.http.routers.grafana.entryPoints=web
            - traefik.http.routers.grafana.rule=HostRegexp(`{host:^grafana.*}`)
            - traefik.http.services.grafana.loadbalancer.server.port=3000

    networks:
      exporter_network:
        driver: overlay
        attachable: true
      proxy_network:
        external: true

    volumes:
      prometheus_data:
        driver_opts:
          type: nfs
          o: addr=10.0.0.30,rw,nfsvers=4
          device: :/nfs/volumes-dev/prometheus_data
      grafana_data:
        driver_opts:
          type: nfs
          o: addr=10.0.0.30,rw,nfsvers=4
          device: :/nfs/volumes-dev/grafana_data
    ```

=== "Prometheus 配置文件"

    ```yaml title='prometheus.yml'
    # my global config
    global:
      scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
      evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
      # scrape_timeout is set to the global default (10s).

    # Alertmanager configuration
    alerting:
      alertmanagers:
        - static_configs:
            - targets:
              # - alertmanager:9093

    # Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
    rule_files:
      # - "first_rules.yml"
      # - "second_rules.yml"

    # A scrape configuration containing exactly one endpoint to scrape:
    # Here it's Prometheus itself.
    scrape_configs:
      # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
      - job_name: 'cadvisor'
        # metrics_path: '/metrics'
        dns_sd_configs:
        - names:
          - 'tasks.cadvisor'
          type: 'A'
          port: 8080
    ```

## 部署运行

!!! info "cadvisor 镜像仓库不能直接访问"

可从 [Github Releases](https://github.com/google/cadvisor/releases) 下载

```bash
docker stack deploy -c monitor-stack.yml monitor
```
