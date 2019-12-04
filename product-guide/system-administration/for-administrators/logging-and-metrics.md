# Logging & Metrics

## Logging <a id="logging"></a>

Logs on the Maana Q platform are aggregated to a Graylog stack running in the cluster. This provides a wholistic view of the platform, rather than a snapshot view of a single service or container.

### Accessing the logs <a id="accessing-the-logs"></a>

For Azure clusters, access Graylog via [https://{host}:8443/graylog/ui/](https://{host}:8443/graylog/ui/).

* Example: [https://latest.knowledge.maana.io:8443/graylog/ui/](https://latest.knowledge.maana.io:8443/graylog/ui/)​
* Credentials \(recommend changing the default\): admin:admin

{% hint style="info" %}
**Important Note:** Containers that are sending logs to Graylog will not give output using command 'docker service logs'{service\_name}’’. Please refer to authoritative documentation for Graylog search: [http://docs.graylog.org/en/2.4/pages/queries.html](http://docs.graylog.org/en/2.4/pages/queries.html)​
{% endhint %}

### Search Time Period <a id="search-time-period"></a>

The UI default search has a limited timeframe that can be changed with the select interface. Be aware, this defaults to 5 minutes.

### Search Log Level <a id="search-log-level"></a>

Viewing messages by log level can be cumbersome, in that log level is represented by a number rather than name \(i.e.ERROR/WARN/INFO\).This number may not be consistent across services due to different logging frameworks. It is possible to search based on log level. For example 'level: 3' as shown here:

![Example &apos;level 3&apos;](../../../.gitbook/assets/image%20%2818%29.png)

### Search Tag \(Service Name\) <a id="search-tag-service-name"></a>

All services include a tag that can be used as a filter. For example tag:maana−admin as shown here:

![Example Tag](../../../.gitbook/assets/image%20%2862%29.png)

## Reporting Issues <a id="reporting-issues"></a>

To report problems or bugs with the system, please use [JIRA](https://jira.corp.maana.io/secure/WelcomeToJIRA.jspa). Also, try to identify any issues that happened in the logs at the time. A screen shot can suffice, but it is strongly encouraged when coming across errors, export the information to a CSV file from Graylog.

Details of how to do this can be found in the documentation: [http://docs.graylog.org/en/2.4/pages/queries.html\#export-results-as-csv](http://docs.graylog.org/en/2.4/pages/queries.html)​

## Metrics <a id="metrics"></a>

Maana Q Metrics are based on a combination of [Prometheus](https://prometheus.io/) and [Grafana](https://grafana.com/). Prometheus provides scraping and storage, Grafana provides visualizations/dashboards. As of Q v3.1.0, there are several preconfigured dashboards are available to indicate platform health. The provided metrics are also gathered from [cAdvisor](https://github.com/google/cadvisor).

* Prometheus uses a pull model to collect metrics, so in Maana Q, metrics are collected from each service every 15 seconds.
* New services with metrics are identified by polling the running containers once per minute.
* See here for metric definitions for Prometheus: [https://github.com/google/cadvisor/blob/master/docs/storage/prometheus.md](https://github.com/google/cadvisor/blob/master/docs/storage/prometheus.md)

### Accessing <a id="accessing"></a>

All clusters currently expose access to [Grafana](https://grafana.com/) on port 4000.

* Example: [http://stable.knowledge.maana.io:4000/](http://stable.knowledge.maana.io:4000/)​
* Credentials - admin:admin

### Platform Discovery of Metrics Providers <a id="platform-discovery-of-metrics-providers"></a>

For your metrics to be available from Grafana, you must identify your service by adding a label to the docker compose file.

```text
maana-core:
  image: ${DOCKERPREFIX-maanainc/}maana-core:latest
  labels:
    MetricsPort: 32100
  deploy:
      ....
```

The MetricsPort label declares the port on which the metrics server is exposed.

* For all Node applications this should be 32100.
* Do not add the label to your service if it does not provide metrics.

### Node based Services <a id="node-based-services"></a>

Import the metrics functions:

```text
import { initMetrics, counter } from 'io.maana.shared'
```

Initialize metrics exactly once in your service, call initMetrics with a service name:

```text
initMetrics(SELF)
```

Add counters for each of the metrics you wish to track, they can be declared where they are used, provide a name and a description:

```text
const graphqlRequestCounter = counter('graphqlRequests', 'GraphQL request count')
```

Increment the counter when the event occurs:

```text
graphqlRequestCounter.inc()
// or
graphqlRequestCounter.inc(7)
```

This is an example of inserting a piece of middleware into express to track all requests through an endpoint:

```text
app.use(
  '/graphql',
  (req, res, next) => {
    graphqlRequestCounter.inc()
    next()
  },
  bodyParser.json(),
  httpMiddleware
)
```

[    
](https://maana-ue.gitbook.io/product/role-guide/administrator-guide/service-startup-stabilizing-and-metrics)

