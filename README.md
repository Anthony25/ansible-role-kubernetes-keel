Ansible Role: Keel for Kubernetes
=================================

Ansible role to install Keel on Kubernetes, allowing to autoupdate Kubernetes
deployments.

Role Variables
--------------

```yaml
# Namespace
kubernetes_keel_namespace: "kube-system"
# App name (used as selector)
kubernetes_keel_app: "keel"
# Deployment name
kubernetes_keel_deployment: "keel-deployment"
# Configmap name
kubernetes_keel_configmap: "keel"
# Service account
kubernetes_keel_service_account: "keel"
# Secret name
kubernetes_keel_secret: "keel"
# Service name
kubernetes_keel_service: "keel"

# Number of replicas
kubernetes_keel_replicas: 1
kubernetes_keel_revision_history: 1

# Node selector
kubernetes_keel_node_selector: {}

kubernetes_keel_resources:
  limits:
    memory: "256Mi"
  requests:
    memory: "64Mi"

# Setup ingress for keel
kubernetes_keel_setup_ingress: false
kubernetes_keel_ingress:
  name: "keel-ingress"
  host: "keel.example.com"
  annotations:
  tls:

### Keel options ###

# Enable or not the polling
kubernetes_keel_poll: 1

# Enable or not the helm provider
kubernetes_keel_helm_provider: 0

# Enable integration with Google Container
kubernetes_keel_pubsub: ""
# Google Container project ID
kubernetes_keel_project_id: ""

# Provide an endpoint where Keel should send notifications
kubernetes_keel_webhook_endpoint: ""

# Slack token where Keel should send notifications
kubernetes_keel_slack_token: ""
# Slack channels where Kell should send notifications
kubernetes_keel_slack_channels: ""
```

Dependencies
------------

Kubectl needs to be installed on the host targeted by the role.


Example Playbook
----------------

```yaml

- hosts: kube-master
  run_once: true
  vars:
    kubernetes_keel_setup_ingress: true
    kubernetes_keel_ingress:
      name: "keel-ingress"
      host: "keel.example.com"
      annotations:
        kubernetes.io/tls-acme: "true"
      tls:
        - secretName: "keel-ingress-tls"
          hosts:
            - "keel.example.com"
  roles:
    - role: Anthony25.kubernetes-keel
```

Use `run_once` to run the role on only one available master in the cluster.

License
-------

Tool under the BSD license. Do not hesitate to report bugs, ask me some
questions or do some pull request if you want to!
