# Event Driven Automation Collection - nats.eda

This collection contain eda plugin for nats / jetstream

## Plugins

The following plugins are included in the collection

| Name              | Description                             |
| ----------------- | ----------------------------------------|
| nats.eda.nats     | Configure Nats listener for events      |
| nats.eda.nats_js  | Configure Jetstream listener for events |


### Params

#### nats_js

| Name              | Description                                                            |
| ----------------- | -----------------------------------------------------------------------|
|    host           | The host where the stream is hosted can contain the full url with port |
|    username       | The optional username to be used                                       |
|    password       | The optional password to be used                                       |
|    token          | The optional token to be used                                          |
|    stream         | The stream name                                                        |
|    subject        | The subject name                                                       |
|    durable        | The name of the durable consumer                                       |
|    queue          | The queue name of subscription for distributing requests               |
|    deliver_policy | The Policy for deliver msg on start can be all|last|new, default all   |

#### nats

| Name              | Description                                                            |
| ----------------- | -----------------------------------------------------------------------|
|    host           | The host where the stream is hosted can contain the full url with port |
|    username       | The optional username to be used                                       |
|    password       | The optional password to be used                                       |
|    token          | The optional token to be used                                          |
|    subject        | The subject name                                                       |
|    queue          | The queue name of subscription for distributing requests               |

### Usage

```yaml
- name: listen for events
  hosts: all

  sources:
    - ansible.eda.nats_js:
        host: nats://nats:4222
        username: admin
        password: mypassword
        subject: foo
        stream: eda
        durable: eda_test
        deliver_policy: all

  rules:
    - name: test
      condition: event.payload.message == "eda"
      action:
        run_playbook:
          name: test.yml
```

```yaml
- name: listen for events
  hosts: all

  sources:
    - ansible.eda.nats:
        host: nats://nats:4222
        token: mytoken
        subject: foo
  rules:
    - name: teste
      condition: event.payload.message == "eda"
      action:
        run_playbook:
          name: test.yml
```