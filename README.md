# Kubernetes Ingress + LoadBalancer Deployment

##  Project Overview
This project demonstrates how to deploy multiple applications in Kubernetes and expose them through a **single LoadBalancer** using the **Nginx Ingress Controller**. Path-based routing is used so each application can be accessed through different URL paths under the same LoadBalancer DNS.

Example:
- `http://<LoadBalancer-DNS>/app1`
- `http://<LoadBalancer-DNS>/app2`

This is a production-style setup commonly used in cloud environments to optimize cost and traffic management.

---

## Architecture Components

### 1. Application Deployments
Two applications were deployed:
- **app1**
- **app2**

Each application is defined using a Kubernetes **Deployment** manifest containing:
- Container image  
- Replica count  
- Labels for selectors  

---

### 2. ClusterIP Services
Both applications were exposed internally using **ClusterIP services**:
- `app1-service`
- `app2-service`

ClusterIP is ideal because it keeps the applications internal, allowing the Ingress to control external access.

---

### 3. Nginx Ingress Controller Installation
The Nginx Ingress Controller was installed to process Ingress rules.

Installing the controller automatically created:
- A Kubernetes **LoadBalancer** service  
- An external DNS / Public IP  
- Link- kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml

This LoadBalancer becomes the main entry point for all external traffic.
![](/images/applyfile.png)

---

### 4. Ingress Resource (Path-Based Routing)
A single **Ingress** resource was created to route incoming traffic to specific services based on URL paths.

Example routing:
- `/app1` → `app1-service`
- `/app2` → `app2-service`

The Nginx Ingress Controller reads these rules and forwards requests accordingly.

---
### 5. Create Load Balancer
- Create application Load Balancer
- When creating Target group using a load balancer service port nunber and add rule

![](/images/LB.png)
![](/images/TargetGrp.png)

---
### 6. Hit on Browser
- Using Load Balancer DNS
- /app1
- /app2

![](/images/app1.png)
![](/images/app2.png)

- Conclusion

   This project successfully showcases how to expose multiple applications in Kubernetes using a single LoadBalancer with Ingress path-based routing. It provides a clean, scalable, and cost-efficient architecture while improving my understanding of Kubernetes networking and traffic management.
___