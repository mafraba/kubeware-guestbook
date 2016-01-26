## Guestbook Example

This example shows how to build a simple, multi-tier web application using [Kubernetes](http://kubernetes.io/), [Docker](https://www.docker.com/) and [KDeploy](https://github.com/flexiant/kdeploy).

**Table of Contents**
<!-- BEGIN MUNGE: GENERATED_TOC -->

  - [Guestbook Example](#guestbook-example)
    - [Prerequisites](#prerequisites)
    - [Quick Start](#quick-start)


The example consists of:

- A web frontend
- A [redis](http://redis.io/) master (for storage), and a replicated set of redis 'slaves'.

The web frontend interacts with the redis master via javascript redis API calls.

### Prerequisites

This example requires a running Kubernetes cluster and installation of Kdeploy tool. See the [Getting Started guides](https://github.com/flexiant/kubernetes/docs/getting-started-guides/) for how to get started. And follow the [Prerequisites](https://github.com/flexiant/kubernetes/docs/user-guide/prereqs.md) to make sure your `kubectl` is ok. In the case of KDeploy follow the installation process described in the following web [https://github.com/flexiant/kdeploy](https://github.com/flexiant/kdeploy)

### Quick Start

This section shows the simplest way to get the example work.

Start the guestbook with one command:

```console
$ kdeploy deploy --kubeware "https://github.com/flexiant/kubeware-guestbook"
service "redis-master" created
replicationcontroller "redis-master" created
service "redis-slave" created
replicationcontroller "redis-slave" created
service "frontend" created
replicationcontroller "frontend" created
```

Then, list all your kubewares:

```console
$ kdeploy list
NAME            CLUSTER_IP     EXTERNAL_FQDN                     PORT(S)   SELECTOR                   AGE
Guestbook       10.0.93.211    guestbook.example.concerto.io     80/TCP    kubeware=guestbook         1h
```

Now you can access the guestbook on each node with frontend service's `<ClusterIP>:Port`, e.g. `10.0.93.211:80` in this guide. `<ClusterIP>` is a cluster-internal IP. If you want to access the guestbook from outside of the cluster, add in your attribute list  `svc/frontend/balancer` to `LoadBalancer`. Then you can access the guestbook with external fqdn from outside of the cluster on those cloud providers which support external load balancers.

Clean up the guestbook:

```console
$ kdeploy delete --kubeware "guestbook"
```
