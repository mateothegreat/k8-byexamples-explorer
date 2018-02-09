<!--
#                                 __                 __
#    __  ______  ____ ___  ____ _/ /____  ____  ____/ /
#   / / / / __ \/ __ `__ \/ __ `/ __/ _ \/ __ \/ __  /
#  / /_/ / /_/ / / / / / / /_/ / /_/  __/ /_/ / /_/ /
#  \__, /\____/_/ /_/ /_/\__,_/\__/\___/\____/\__,_/
# /____                     matthewdavis.io, holla!
#
#-->

[![Clickity click](https://img.shields.io/badge/k8s%20by%20example%20yo-limit%20time-ff69b4.svg?style=flat-square)](https://k8.matthewdavis.io)
[![Twitter Follow](https://img.shields.io/twitter/follow/yomateod.svg?label=Follow&style=flat-square)](https://twitter.com/yomateod) [![Skype Contact](https://img.shields.io/badge/skype%20id-appsoa-blue.svg?style=flat-square)](skype:appsoa?chat)

# Container for examining the runtime environment Kubernetes produces for your pods.

> k8 by example -- straight to the point, simple execution.

## Install

```sh
$ make install

[ INSTALLING MANIFESTS/POD.YAML ]: pod "explorer" created
```

## Delete

```sh
$ make delete

[ DELETING MANIFESTS/POD.YAML ]: pod "explorer" deleted
```

## Usage

```sh
$ kubectl create -f examples/explorer/pod.yaml
$ kubectl proxy &
Starting to serve on localhost:8001

$ curl localhost:8001/api/v1/proxy/namespaces/default/pods/explorer:8080/vars/
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=explorer
KIBANA_LOGGING_PORT_5601_TCP_PORT=5601
KUBERNETES_SERVICE_HOST=10.0.0.2
MONITORING_GRAFANA_PORT_80_TCP_PROTO=tcp
MONITORING_INFLUXDB_UI_PORT_80_TCP_PROTO=tcp
KIBANA_LOGGING_SERVICE_PORT=5601
MONITORING_HEAPSTER_PORT_80_TCP_PORT=80
MONITORING_INFLUXDB_UI_PORT_80_TCP_PORT=80
KIBANA_LOGGING_SERVICE_HOST=10.0.204.206
KIBANA_LOGGING_PORT_5601_TCP=tcp://10.0.204.206:5601
KUBERNETES_PORT=tcp://10.0.0.2:443
MONITORING_INFLUXDB_PORT=tcp://10.0.2.30:80
MONITORING_INFLUXDB_PORT_80_TCP_PROTO=tcp
MONITORING_INFLUXDB_UI_PORT=tcp://10.0.36.78:80
KUBE_DNS_PORT_53_UDP=udp://10.0.0.10:53
MONITORING_INFLUXDB_SERVICE_HOST=10.0.2.30
ELASTICSEARCH_LOGGING_PORT=tcp://10.0.48.200:9200
ELASTICSEARCH_LOGGING_PORT_9200_TCP_PORT=9200
KUBERNETES_PORT_443_TCP=tcp://10.0.0.2:443
ELASTICSEARCH_LOGGING_PORT_9200_TCP_PROTO=tcp
KIBANA_LOGGING_PORT_5601_TCP_ADDR=10.0.204.206
KUBE_DNS_PORT_53_UDP_ADDR=10.0.0.10
MONITORING_HEAPSTER_PORT_80_TCP_PROTO=tcp
MONITORING_INFLUXDB_PORT_80_TCP_ADDR=10.0.2.30
KIBANA_LOGGING_PORT=tcp://10.0.204.206:5601
MONITORING_GRAFANA_SERVICE_PORT=80
MONITORING_HEAPSTER_SERVICE_PORT=80
MONITORING_HEAPSTER_PORT_80_TCP=tcp://10.0.150.238:80
ELASTICSEARCH_LOGGING_PORT_9200_TCP=tcp://10.0.48.200:9200
ELASTICSEARCH_LOGGING_PORT_9200_TCP_ADDR=10.0.48.200
MONITORING_GRAFANA_PORT_80_TCP_PORT=80
MONITORING_HEAPSTER_PORT=tcp://10.0.150.238:80
MONITORING_INFLUXDB_PORT_80_TCP=tcp://10.0.2.30:80
KUBE_DNS_SERVICE_PORT=53
KUBE_DNS_PORT_53_UDP_PORT=53
MONITORING_GRAFANA_PORT_80_TCP_ADDR=10.0.100.174
MONITORING_INFLUXDB_UI_SERVICE_HOST=10.0.36.78
KIBANA_LOGGING_PORT_5601_TCP_PROTO=tcp
MONITORING_GRAFANA_PORT=tcp://10.0.100.174:80
MONITORING_INFLUXDB_UI_PORT_80_TCP_ADDR=10.0.36.78
KUBE_DNS_SERVICE_HOST=10.0.0.10
KUBERNETES_PORT_443_TCP_PORT=443
MONITORING_HEAPSTER_PORT_80_TCP_ADDR=10.0.150.238
MONITORING_INFLUXDB_UI_SERVICE_PORT=80
KUBE_DNS_PORT=udp://10.0.0.10:53
ELASTICSEARCH_LOGGING_SERVICE_HOST=10.0.48.200
KUBERNETES_SERVICE_PORT=443
MONITORING_HEAPSTER_SERVICE_HOST=10.0.150.238
MONITORING_INFLUXDB_SERVICE_PORT=80
MONITORING_INFLUXDB_PORT_80_TCP_PORT=80
KUBE_DNS_PORT_53_UDP_PROTO=udp
MONITORING_GRAFANA_PORT_80_TCP=tcp://10.0.100.174:80
ELASTICSEARCH_LOGGING_SERVICE_PORT=9200
MONITORING_GRAFANA_SERVICE_HOST=10.0.100.174
MONITORING_INFLUXDB_UI_PORT_80_TCP=tcp://10.0.36.78:80
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_ADDR=10.0.0.2
HOME=/

$ curl localhost:8001/api/v1/proxy/namespaces/default/pods/explorer:8080/fs/
mount/
var/
.dockerenv
etc/
dev/
proc/
.dockerinit
sys/
README.md
explorer

$ curl localhost:8001/api/v1/proxy/namespaces/default/pods/explorer:8080/dns?q=elasticsearch-logging
<html><head></head><body>
<form action="/api/v1/proxy/namespaces/default/pods/explorer:8080/dns">
<input name="q" type="text" value="elasticsearch-logging"/>
<button type="submit">Lookup</button>
</form>
<br/><br/><pre>LookupNS(elasticsearch-logging):
Result: ([]*net.NS)<nil>
Error: &lt;*&gt;lookup elasticsearch-logging: no such host

LookupTXT(elasticsearch-logging):
Result: ([]string)<nil>
Error: &lt;*&gt;lookup elasticsearch-logging: no such host

LookupSRV(&#34;&#34;, &#34;&#34;, elasticsearch-logging):
cname: elasticsearch-logging.default.svc.cluster.local.
Result: ([]*net.SRV)[&lt;*&gt;{Target:(string)elasticsearch-logging.default.svc.cluster.local. Port:(uint16)9200 Priority:(uint16)10 Weight:(uint16)100}]
Error: <nil>

LookupHost(elasticsearch-logging):
Result: ([]string)[10.0.60.245]
Error: <nil>

LookupIP(elasticsearch-logging):
Result: ([]net.IP)[10.0.60.245]
Error: <nil>

LookupMX(elasticsearch-logging):
Result: ([]*net.MX)<nil>
Error: &lt;*&gt;lookup elasticsearch-logging: no such host

</nil></nil></nil></nil></nil></nil></pre>

</body></html>
```
