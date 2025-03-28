# KEDA

KEDA (Kubernetes Event-Driven Autoscaling) is an open-source project that enables Kubernetes workloads to scale based on external events. It acts as an autoscaler that works alongside the Kubernetes Horizontal Pod Autoscaler (HPA) but extends its capabilities by supporting event-driven scaling from various external sources.

### Key Features of KEDA

1. Event-Driven Scaling
   * KEDA scales applications based on events from external sources like message queues, databases, monitoring systems, and cloud services.

2. Supports Various Scalers
   * It has built-in scalers for AWS SQS, Azure Service Bus, Kafka, RabbitMQ, Prometheus, PostgreSQL, MySQL, Redis, and many more.

3. Works with Kubernetes HPA
   * KEDA works alongside HPA and extends its functionality by allowing scaling based on external metrics.

4. Efficient Resource Management
   * It can scale workloads to zero when there are no events to process, saving resources and costs.

5. Easy Deployment
   * KEDA can be installed as a lightweight custom resource definition (CRD) in Kubernetes.


### How KEDA Works

1. KEDA continuously monitors the event source (e.g., a message queue).
2. When an event threshold is met, KEDA activates the workload by scaling the number of pods accordingly.
3. Once events decrease, KEDA scales the workload back down (even to zero).


### Example Use Cases

1. KEDA can be leveraged to dynamically scale image processing pods based on messages in an Apache Kafka topic or RabbitMQ queue or AWS SQS queue.
2. KEDA can be leveraged to dynamically scale data processing pods based on Prometheus metrics indicating that memory consumption surpasses 80%.
3. KEDA can be leveraged to dynamically scale e-commerce order processing pods based on the message backlog in an Apache Kafka topic during sales events.
   This is a common use case for handling fluctuating workloads, especially during high-traffic sales events.


### Precondition

  - Kubernetes Cluster


### Installation

1. Install KEDA via Helm:

    ```sh
    helm repo add kedacore https://kedacore.github.io/charts
    helm repo update
    helm install keda kedacore/keda --namespace keda --create-namespace
    ```

2. Install RabbitMQ Server

    ```sh
    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm install rabbitmq --set auth.username=guest --set auth.password=guest bitnami/rabbitmq --wait
    ```

    - Access to the RabbitMQ AMQP port:

        ```sh
        kubectl port-forward --namespace default svc/rabbitmq 5672:5672
        ```

    - Access to the RabbitMQ Management interface:

        ```sh
        kubectl port-forward --namespace default svc/rabbitmq 5672:5672
        ```