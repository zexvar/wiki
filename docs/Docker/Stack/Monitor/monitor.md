# Monitor 集群监视

## 准备工作

创建配置文件

```yaml title='monitor-stack.yml'
version: "3.9"

services:
  cadvisor:
    # image: gcr.dockerproxy.com/cadvisor/cadvisor
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
      - --disable_metrics=advtcp,sched,cpu_topology,resctrl,memory_numa,tcp,hugetlb,referenced_memory,udp,process,accelerator,disk,diskIO,percpu
    deploy:
      mode: global

  vmware_exporter:
    image: pryorda/vmware_exporter
    networks:
      - exporter_network
    environment:
      - VSPHERE_USER=${VSPHERE_USERNAME}
      - VSPHERE_PASSWORD=${VSPHERE_PASSWORD}
      - VSPHERE_HOST=${VSPHERE_HOST}
      - VSPHERE_IGNORE_SSL=True
      - VSPHERE_SPECS_SIZE=2000
    deploy:
      mode: replicated
      replicas: 1

  prometheus:
    image: prom/prometheus
    user: root
    networks:
      - exporter_network
      - proxy
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
      - proxy
    volumes:
      - grafana_data:/var/lib/grafana
    environment:
      - GF_AUTH_ANONYMOUS_ENABLED=true
    deploy:
      mode: replicated
      replicas: 1
      labels:
        - traefik.enable=true
        - traefik.http.routers.grafana.entryPoints=web
        - traefik.http.routers.grafana.rule=HostRegexp(`{host:^grafana.*}`)
        - traefik.http.services.grafana.loadbalancer.server.port=3000

networks:
  exporter_network:
    driver: overlay
    attachable: true
  proxy:
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

## 部署运行

!!! info "cadvisor 镜像仓库不能直接访问"

可从 [Github Releases](https://github.com/google/cadvisor/releases) 下载
或从 dockerproxy 提供的镜像网站获取cadvisor

``` bash
export VSPHERE_USER=root
export VSPHERE_PASSWORD=123456
export VSPHERE_HOST=10.0.0.100
docker stack deploy -c monitor-stack.yml monitor
```
