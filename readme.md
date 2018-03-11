
## Documentation

In order to deploy Kafka Cluster with 3 brokers on Kubernetes, we used ansible to setup a cloud9 IDE :

**Prerequisites :**
 1. Install python
 2. Install aws cli
 3. Install ansible 4.0.0

**Configure aws credentials :**
 1. Create new aws credentials https://console.aws.amazon.com/iam/home#/security_credential
 2. Run : `aws configure`

**Creating Cloud9 IDE : **
 1. Run : `ansible-playbook cloud9.yml`
 2. Wait until the IDE is UP (check the output for the url)
 3. Open the IDE via the url and **disable AWS  managed temporary credentials**  (via Preference => Aws Settings)

**Creating kubernetes cluster with Kafka : **
 1. Run : `ansible-playbook run-cluster.yml`


**Creating kubernetes cluster with Kafka : **
 1. Run : `ansible-playbook run-cluster.yml`






## Testing

To test the container :

 1. Run `kubectl get pods` & copy the broker-name
 2. Run `kubectl get svc` & copy the broker service name & zk service name
 3. List topics: `kubectl exec -ti k8sclustrkafka-kafka-0 -- kafka-topics --zookeeper k8sclustrkafka-zookeeper:2181 --list`
 4. Produce to test topic : `kubectl exec -ti k8sclustrkafka-kafka-0 -- kafka-console-producer  --broker-list k8sclustrkafka-kafka:9092 --topic test`
 5. Consume from test topic: `kubectl exec -ti k8sclustrkafka-kafka-0 -- kafka-console-consumer --topic test --bootstrap-server k8sclustrkafka-kafka:9092 --from-beginning`
