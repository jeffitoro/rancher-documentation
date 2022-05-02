---
layout: default
title: Load balancing
nav_order: 6
---

# Load balancing
Add load balancing to your application with your certificate ssl.

---

### Configure load balancing
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/loadbalancing/ingress-loadbalancing.png" />](/assets/images/loadbalancing/ingress-loadbalancing.png)

### Check your loads balancings
[<img alt="alt_text" src="{{site.baseurl}}/assets/images/loadbalancing/result-loadbalancing.png" />](/assets/images/loadbalancing/result-loadbalancing.png)

### Annotations
```yaml
nginx.ingress.kubernetes.io/proxy-body-size=0
nginx.ingress.kubernetes.io/proxy-connect-timeout=160
nginx.ingress.kubernetes.io/proxy-read-timeout=1600
nginx.ingress.kubernetes.io/proxy-send-timeout=1600
nginx.ingress.kubernetes.io/ssl-redirect=false
nginx.org/accept_mutex=on
nginx.org/client-max-body-size=100m
nginx.org/keepalive-requests=100
nginx.org/keepalive_timeout=100
nginx.org/worker-connections=4096
```