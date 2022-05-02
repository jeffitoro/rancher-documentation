---
layout: default
title: Cert manager
nav_order: 4
---

# Cert manager: generate your certification ssl
Installation cert manager in kubernetes with kubectl.

---

## Installation with documentation
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/installation-cluster-cert-manager.png" />](/assets/images/cert-manager/installation-cluster-cert-manager.png)

## Launch kubectl with terminal
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/kubectl-cluster-install-cert-manager.png" />](/assets/images/cert-manager/kubectl-cluster-install-cert-manager.png)

## Make your manager for certification in production
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/build-cert-manager-production-cert-manager.png" />](/assets/images/cert-manager/build-cert-manager-production-cert-manager.png)

```yaml
kubectl apply -f - <<EOF
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-production
  namespace: default
spec:
  acme:
    # The ACME server URL
    server: https://acme-v02.api.letsencrypt.org/directory
    # Email address used for ACME registration
    email: server@molengeek.com
    # Name of a secret used to store the ACME account private key
    privateKeySecretRef:
      name: letsencrypt-production
    # Enable the HTTP-01 challenge provider
    solvers:
    # An empty 'selector' means that this solver matches all domains
    - selector: {}
      http01:
        ingress:
          class: nginx
EOF
```

## Check services cert manager in cluster
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/services-rancher-system-cert-manager.png" />](/assets/images/cert-manager/services-rancher-system-cert-manager.png)

---

# Make certification ssl

---

## Redirect your server dnsNames to your server node with project
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/dns-cert-manager.png" />](/assets/images/cert-manager/dns-cert-manager.png)

## Verify your redirection ip with ping
You can verify your connexion on https://ping.eu/ping with ip put in records de type A on Godaddy.
If your serverName redirect to your ip, you can continue.

## Request your manager for certificates ssl in production
```yaml
apiVersion: cert-manager.io/v1 
kind: Certificate
metadata:
  name: crt-tech
spec:
  secretName: crt-tech-secret
  dnsNames:
    - domain.com
  privateKey:
    rotationPolicy: Always
  issuerRef:
    name: letsencrypt-production
    kind: ClusterIssuer
```
Import this code in rancher, Exemple: 
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/import-yaml-cert-manager.png" />](/assets/images/cert-manager/import-yaml-cert-manager.png)

## If your request for certicate ssl is running
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/acme-cert-manager.png" />](/assets/images/cert-manager/acme-cert-manager.png)

## After one time, your certificate is generate. You can verify this in section certificates
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/cert-manager/certification-cert-manager.png" />](/assets/images/cert-manager/certification-cert-manager.png)
