# Service Startup, Stabilizing, Backup & Restore

## **Service Startup**

Typically, Services will fail during startup. This is normal as long as there is at least one copy of a Service in a running state at the end of startup. You can always check on the current state in your Terminal by running either: **``` docker service ls ```**

OR

**``` docker stack ps infrastructure docker stack ps core docker stack ps samples docker stack ps azure docker stack ps arbots ```**

## Service Stabilization & Performance Metrics

To determine if the system is in a stable state, go to the prometheus page at: http://&lt;cluster name&gt;:9090

Under Status/Targets verify that SAQ is reporting green. Note that it is normal for Docker to report as unavailable.

Performance Metrics are available on the Public IP Address at: http://&lt;cluster name&gt;:4000

{% hint style="info" %}
**Note:** the default login credentials for this page will be admin/admin, it is recommended that you change these credentials immediately following your first login.
{% endhint %}

## Service Deployment - Backup & Restore

In order to handle instances where the platform URL changes between backup & restore, services in the system check URIs when adding files, images, and services for the deployment's public URL \(environment variable `PUBLIC_BACKEND_URI`\). If found, it is replaced with the environment variable `BACKEND_URI_TAG` \(default value `%PUBLIC_BACKEND_URI%`\).

This string will be seen on raw instances within the system. However, when files, images, and services are queried via resolvers for those types, the `BACKEND_URI_TAG` will be replaced with the value of `PUBLIC_BACKEND_URI` in the response.

