---
title: Access FactoryInsight outside the cluster
content_type: task
weight: 50
---

<!-- overview -->
This page describes how to access FactoryInsight outside the cluster.

The United Manufacturing Hub is not exposed to the internet, therefore you cannot
use the default Kubernetes Ingress to access FactoryInsight.

Instead, you can create a LoadBalancer service to expose it from the host.

## {{% heading "prerequisites" %}}

{{< include "task-tutorial-prereqs.md" >}}

<!-- steps -->

## Create a LoadBalancer service

1. From UMHLens, click on the **+** icon on the bottom bar and select
   **Create resource**.
2. Copy and paste the following YAML into the editor:

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: exposing-factoryinsight-externally
      namespace: united-manufacturing-hub
    spec:
      type: LoadBalancer
      selector:
        app.kubernetes.io/name: united-manufacturing-hub-factoryinsight
      ports:
        - protocol: TCP
          port: 8081
          targetPort: 80
    ```

3. Click **Create & Close**.

## Access FactoryInsight

1. Go to `http://<host-ip>:8081/` to verify that the service is working.
   You should see the word `online` in the browser.

## {{% heading "discussion" %}}

The service is exposed on port 8081, but you can change it to any other port
that is not already in use.

## {{% heading "seealso" %}}

- See [Access Kafka outside the cluster](/docs/administration/access-kafka-outside-cluster) to
  learn how to access Kafka outside the cluster.