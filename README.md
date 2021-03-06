# Base Java Microservice

## Introduction
This chart creates a deployment designed to be used as template with Java microservices.

## Installing the Chart
```bash
git clone https://git.paradigmadigital.com/helm/base-java-microservice/
cd base-java-microservice

# Before install of module, you need configurate file my-values.yaml
helm install . --values my-values.yaml --name my-release
```

## Variables

* `msName`: Microservice's name. **Required**.
* `dockerImage`: Which docker image to run. **Required**.
* `javaOpts`: Java options. [Default: -Djava.security.egd=file:/dev/./urandom
  -Xms256m -Xmx512M]
* `javaParameters`: Java parameters. [Default: Not set]
* `springbootProfile`: The SpringBoot profile to be used. The profile per se
  it's empty because it's usually used with environments, and that shouldn't be
  hardcoded. When `environment` is not set, this variable is also not set, so
  SpingBoot can use it's local profile. [Default: --spring.profiles.active=]
* `netflix`: Set to yes if you want to define a config-server or eureka-server
  environment variables. [Default: no]
* `configServer`: Config server url. Needs the previous variable set to `yes`.
  [Default: http://config-server:8080]
* `listenPort`: Port opened in the load balancer. [Default: 80]
* `containerPort`: Container port to bind the webserver. [Default: 8080]
* `readinessPath`: Path to test if pod is ready. [Default: /manage/health]
* `readinessDelay`: Number of seconds to wait to test if the pod is ready.
  [Default: 60]
* `readinessTimeout`: Number of seconds to wait to mark as invalid a readiness
  test. [Default: 5]
* `readinessPeriod`: Interval of seconds to wait between readiness tests.
  [Default: 10]
* `readinessSuccess`: Number of tests to do until consider the pod is ready.
  [Default: 1]
* `readinessFailure`: Number of tests to fail until consider the pod is not
  ready. [Default: 6]
* `livenessPath`: Path to test if pod is alive. [Default: /manage/health]
* `livenessDelay`: Number of seconds to wait to test if the pod is alive.
  [Default: 120]
* `livenessTimeout`: Number of seconds to wait to mark as invalid an alive test.
  [Default: 5]
* `livenessPeriod`: Interval of seconds to wait between liveness tests.
  [Default: 10]
* `livenessFailure`: Number of tests to fail until consider the pod is not
  alive. [Default: 6]
* `requestsCpu`: CPU aproximated use. [Default: 100Mi]
* `requestsMemory`: Memory aproximated use. [Default: 512Mi]
* `limitsCpu`: CPU limit use. [Default: 200Mi]
* `limitsMemory`: CPU Memory use. [Default: 800Mi]
* `externalBalancer`: Create an external load balancer or internal. [Default:
  no]
* `isConfigServer`: If set to yes, sets the `eureka-server` url, if set to no,
  the `config-server` url. [Default: no]
* `minReplicas`: The minimal number of pods that will be running. [Default: 1]
* `maxReplicas`: The maximal number of pods that will be running. [Default: 3]
* `targetCpu`: In which point should the ms autoscale. [Default: 50]
* `environment`: The environment in which to be deployed. This is used toguether
  with `springbootProfile`. [Default: local]
* `imagePullPolicy`: Protocol to download the docker image. [Default:
  IfNotPresent]
* `configMapName`: The name of the file to mount. [Default: False]
* `configMapPath`: The path in which to mount the configmap. [Default: False]
* `configMapContent`: The content of the configmap. [Default: False]
* `nodeAffinityInstanceGroup`: The node's label to assign pod affinity
* `nodeAntiAffInityInstanceGroup`: The node's label to assign pod affinity
* `serviceMonitor.enabled`: Enable Prometheu's ServiceMonitor. [Default: False]
* `serviceMonitor.prometheus`: Label for prometheus to identify it's
  ServiceMonitors. [Default: kube-prometheus]
* `serviceMonitor.metricsPath`: Metrics endpoint in the microservice. [Default:
  /actuator/prometheus]
* `serviceMonitor.interval`: Interval of time between petitions to the metrics
  endpoint. [Default: 60s]
* `serviceMonitor.targetPort`: Port of the webserver that exposes the metrics.
  [Default: 8080]

## Tests

```bash
helm unittest .
```
