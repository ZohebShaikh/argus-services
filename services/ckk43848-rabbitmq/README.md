# RabbitMQ Setup

Follow the steps below to configure RabbitMQ for the `argus` namespace.

## 1.  Create Secrets

Create two sealed secrets using kubeseal: one for `rabbitmq-password`, which is required to log in to the admin portal, and another for `rabbitmq-erlang-cookie`, which is used to maintain state and prevent RabbitMQ restarting prematurely.

Use [`kubeseal`](https://github.com/bitnami-labs/sealed-secrets?tab=readme-ov-file#raw-mode-experimental) in raw mode to seal each secret.
This command generates a random string and seals it with kubeseal which are then safe to commit to public repositories.

```bash
head -c 500 /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 16 | head -n 1 | kubeseal --raw --namespace argus --name rabbitmq-secrets
```

This will output a sealed string. Add the resulting output into the appropriate fields in `templates/secret.yaml`:
* `rabbitmq-password`
* `rabbitmq-erlang-cookie`

---

## 2. Configure Domain Name (Recommended)

Request a static IP mapped from a DNS entry from the Scientific Computing help desk.

Once assigned, set the static IP under the `loadBalancerIP` field in your `values.yaml` file.

`ckk43848-rabbitmq-daq.diamond.ac.uk -> Static IP ` this mapping allows processes outside of the namespace e.g. Analysis to access data from rabbitmq.
