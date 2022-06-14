# wallarm-sidecar

A Helm chart for Wallarm sidecar controller components

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| admissionWebhook | object | *See below for details* | Configuration sidecar injector module |
| admissionWebhook.affinity | object | `{}` | Node affinity for webhook pod and helper Jobs |
| admissionWebhook.annotations | object | `{}` | Annotations to be added to admission webhook resources |
| admissionWebhook.failurePolicy | string | `"Fail"` | Admission webhook failure policy |
| admissionWebhook.image.image | string | `"dmitriev/sidecar-injector"` | Image repository |
| admissionWebhook.image.pullPolicy | string | `"IfNotPresent"` | Image pullPolicy |
| admissionWebhook.image.registry | string | `"quay.io"` | Image registry |
| admissionWebhook.image.tag | string | `"0.1.0"` | Image tag |
| admissionWebhook.labels | object | `{}` | Labels to be added to admission webhook resources |
| admissionWebhook.nodeSelector | object | `{}` | Node selector for webhook pod and helper Jobs |
| admissionWebhook.patch | object | *See below for details* | Configuration for certgen and patch helper Jobs |
| admissionWebhook.patch.image.image | string | `"ingress-nginx/kube-webhook-certgen"` | Image repository |
| admissionWebhook.patch.image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| admissionWebhook.patch.image.registry | string | `"k8s.gcr.io"` | Image registry |
| admissionWebhook.patch.image.tag | string | `"v1.1.1"` | Image tag |
| admissionWebhook.patch.resources | object | `{}` | Resources for certgen and patch helper Jobs |
| admissionWebhook.port | int | `8443` | Admission webhook listening port |
| admissionWebhook.replicaCount | int | `1` | Replica count of admission webhook deployment |
| admissionWebhook.resources | object | `{}` | Resources for admission webhook Pod |
| admissionWebhook.service.annotations | object | `{}` | Annotations to be added to admission webhook service |
| admissionWebhook.tolerations | list | `[]` | Node tolerations for webhook pod and helper Jobs |
| fullnameOverride | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `""` |  |
| postanalytics | object | *See below for details* | Configuration for post-analytics module |
| postanalytics.affinity | object | `{}` | Node affinity for post-analytics pod |
| postanalytics.annotations | object | `{}` | Annotations to be added to admission webhook resources |
| postanalytics.helpers.addnode.resources | object | `{}` | Resources for `addnode` init container |
| postanalytics.helpers.appstructure.resources | object | `{}` | Resources for `appstructure` helper container |
| postanalytics.helpers.cron.jobs | object | *See below for details* | Cron jobs configuration |
| postanalytics.helpers.cron.jobs.bruteDetect | object | *See below for details* | Parameters for `brute detect` job |
| postanalytics.helpers.cron.jobs.bruteDetect.schedule | string | `"* * * * *"` | Job schedule in cron format |
| postanalytics.helpers.cron.jobs.bruteDetect.timeout | string | `"6m"` | Job timeout |
| postanalytics.helpers.cron.jobs.exportAttacks | object | *See below for details* | Parameters for `export attacks` job |
| postanalytics.helpers.cron.jobs.exportAttacks.schedule | string | `"* * * * *"` | Job schedule in cron format |
| postanalytics.helpers.cron.jobs.exportAttacks.timeout | string | `"3h"` | Job timeout |
| postanalytics.helpers.cron.jobs.exportCounters | object | *See below for details* | Parameters for `export counters` job |
| postanalytics.helpers.cron.jobs.exportCounters.schedule | string | `"* * * * *"` | Job schedule in cron format |
| postanalytics.helpers.cron.jobs.exportCounters.timeout | string | `"11m"` | Job timeout |
| postanalytics.helpers.cron.jobs.exportEnvironment | object | *See below for details* | Parameters for `export environment` job |
| postanalytics.helpers.cron.jobs.exportEnvironment.schedule | string | `"0 */1 * * *"` | Job schedule in cron format |
| postanalytics.helpers.cron.jobs.exportEnvironment.timeout | string | `"10m"` | Job timeout |
| postanalytics.helpers.cron.jobs.syncMarkers | object | *See below for details* | Parameters for `sync markers` job |
| postanalytics.helpers.cron.jobs.syncMarkers.schedule | string | `"* * * * *"` | Job schedule in cron format |
| postanalytics.helpers.cron.jobs.syncMarkers.timeout | string | `"1h"` | Job timeout |
| postanalytics.helpers.cron.resources | object | `{}` | Resources for `cron` helper container |
| postanalytics.helpers.exportenv.resources | object | `{}` | Resources for `exportenv` init container |
| postanalytics.helpers.heartbeat.resources | object | `{}` | Resources for `heartbeat` helper container |
| postanalytics.labels | object | `{}` | Labels to be added to admission webhook resources |
| postanalytics.nodeSelector | object | `{}` | Node selector for post-analytics pod |
| postanalytics.tarantool.arena | string | `"0.5"` | The allocated memory size in GB for Tarantool in-memory storage |
| postanalytics.tarantool.image.image | string | `"wallarm/ingress-tarantool"` | Image repository |
| postanalytics.tarantool.image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| postanalytics.tarantool.image.registry | string | `"docker.io"` | Image registry |
| postanalytics.tarantool.image.tag | string | `"4.0.3-1"` | Image tag |
| postanalytics.tarantool.livenessProbe | object | *See below for details* | Configuration of TCP liveness probe for `tarantool` container |
| postanalytics.tarantool.resources | object | `{}` | Resources for `tarantool` container |
| postanalytics.tarantool.service.annotations | object | `{}` | Annotations to be added to Tarantool service |
| postanalytics.tolerations | list | `[]` | Node tolerations for post-analytics pod |
| sidecarDefaults.container.helper | object | *See below for details* | Default configuration for helper container |
| sidecarDefaults.container.helper.resources | object | `{}` | Resources for `helper` container. Applicable if `sidecarDefaults.deployment.scheme` is set to `split` |
| sidecarDefaults.container.init | object | *See below for details* | Default configuration for init-containers |
| sidecarDefaults.container.init.helper.resources | object | `{}` | Resources for `init-helper` container. Applicable if `sidecarDefaults.deployment.scheme` is set to `split` |
| sidecarDefaults.container.init.iptables.resources | object | `{}` | Resources for `init-iptables` container. Applicable if `sidecarDefaults.deployment.iptablesEnable` is set to `true` |
| sidecarDefaults.container.proxy | object | *See below for details* | Default configuration for proxy container |
| sidecarDefaults.container.proxy.image.image | string | `"quay.io/dmitriev/sidecar-proxy:4.0.3-1"` | Image for all containers in sidecar scheme |
| sidecarDefaults.container.proxy.image.pullPolicy | string | `"IfNotPresent"` | Image pullPolicy |
| sidecarDefaults.container.proxy.livenessProbe | object | *See below for details* | Parameters for httpGet liveness probe configuration. Applicable if "sidecarDefaults.container.proxy.livenessProbeEnable: true" |
| sidecarDefaults.container.proxy.livenessProbe.failureThreshold | int | `3` | Probe failure threshold |
| sidecarDefaults.container.proxy.livenessProbe.initialDelaySeconds | int | `60` | Initial delay in seconds. Do not set initial delay below 60. It's time for bootstrapping sidecar and connecting to the cloud |
| sidecarDefaults.container.proxy.livenessProbe.periodSeconds | int | `10` | Probe period in seconds |
| sidecarDefaults.container.proxy.livenessProbe.successThreshold | int | `1` | Probe success threshold |
| sidecarDefaults.container.proxy.livenessProbe.timeoutSeconds | int | `1` | Probe timeout in seconds |
| sidecarDefaults.container.proxy.livenessProbeEnable | bool | `true` | Enable httpGet liveness probe to path "sidecarDefaults.nginx.healthPath" |
| sidecarDefaults.container.proxy.single.resources | object | `{}` | Default resources for `proxy` container in `single` deployment scheme. Applicable only if `sidecarDefaults.deployment.scheme: single` |
| sidecarDefaults.container.proxy.split.resources | object | `{}` | Default resources for `proxy` container in `split` deployment scheme. Applicable if `sidecarDefaults.deployment.scheme` is set to `split` |
| sidecarDefaults.deployment.iptablesEnable | bool | `true` | Enable or disable `iptables` init container for port redirection |
| sidecarDefaults.deployment.scheme | string | `"single"` | Sidecar deployment scheme: `single` or `split` |
| sidecarDefaults.nginx | object | *See below for details* | Default parameters for Nginx configuration of sidecar proxy container. Parameters in this section can be overwritten individually for each pod using its `.metadata.annotations` |
| sidecarDefaults.nginx.healthPath | string | `"/health"` | Path to Nginx health check endpoint |
| sidecarDefaults.nginx.listenPort | int | `8080` | Port listening by sidecar proxy container. Can't be the same as nginx.proxyPassPort. |
| sidecarDefaults.nginx.proxyPassPort | int | `80` | Port listening by application container |
| sidecarDefaults.nginx.statusPath | string | `"/status"` | Path to Nginx status endpoint |
| sidecarDefaults.nginx.statusPort | int | `10246` | Port for Wallarm status, Nginx stats and health check endpoint |
| sidecarDefaults.nginx.wallarmMetricsPath | string | `"/wallarm-metrics"` | Port to Wallarm metrics endpoint. Metrics provide in Prometheus format. |
| sidecarDefaults.nginx.wallarmMetricsPort | int | `18080` | Port for Wallarm metrics endpoint |
| sidecarDefaults.nginx.wallarmStatusPath | string | `"/wallarm-status"` | Path to Wallarm status endpoint, JSON format |
| sidecarDefaults.wallarm | object | *See below for details* | Wallarm node configuration. Parameters in this section can be overwritten individually for each pod using its `metadata.annotations` |
| sidecarDefaults.wallarm.mode | string | `"monitoring"` | Wallarm mode: `monitoring, `block` or `off` |
| sidecarDefaults.wallarm.modeAllowOverride | string | `"on"` | Manages the ability to override the wallarm_mode values via filtering in the Cloud (custom ruleset): `on`, `off` or `strict` |
| sidecarDefaults.wallarm.parseResponse | string | `"on"` | Whether to analyze the application responses for attacks: `on` or `off` |
| sidecarDefaults.wallarm.parseWebsocket | string | `"off"` | Whether to analyze WebSocket's messages for attacks: `on` or `off` |
| sidecarDefaults.wallarm.unpackResponse | string | `"on"` | Whether to decompress compressed data returned in the application response: `on` or `off` |
| sidecarDefaults.wallarm.upstream.connectAttempts | int | `10` | Defines the number of immediate reconnects to the Tarantool or Wallarm API |
| sidecarDefaults.wallarm.upstream.reconnectInterval | string | `"15s"` | Defines the interval between attempts to reconnect to the Tarantool or Wallarm API |
| wallarmApi | object | *See below for details* | Wallarm API settings for post-analytics module and sidecar containers. |
| wallarmApi.host | string | `"api.wallarm.com"` | Address of Wallarm API service |
| wallarmApi.port | int | `443` | Port of Wallarm API service |
| wallarmApi.token | string | `""` | Token to authorize in the Wallarm Cloud |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.9.1](https://github.com/norwoodj/helm-docs/releases/v1.9.1)