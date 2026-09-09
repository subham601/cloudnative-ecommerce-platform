# Ecommerce Microservices Platform — DevOps, DevSecOps, Kubernetes, Istio & GitOps

A production-style e-commerce microservices platform designed to demonstrate modern **DevOps, DevSecOps, Kubernetes, GitOps, Service Mesh, Security, Resilience and Observability** practices.

The application contains multiple backend microservices and a frontend deployed on Kubernetes. Istio provides service-mesh capabilities such as traffic management, mTLS, resilience and telemetry. GitHub Actions provides CI and DevSecOps automation, Docker Hub acts as the container registry, and Argo CD provides GitOps-based Kubernetes deployment.

The platform also demonstrates Kubernetes security controls including **RBAC, least-privilege access, Pod Security, Network Policies, Audit Policy, Argo CD RBAC and secret-management configuration**.

---

# Architecture

```text
                         APPLICATION REPOSITORY
                    cloudnative-ecommerce-platform
                                │
                                │ git push
                                ▼
                         GitHub Actions
                                │
                    ┌───────────┴────────────────┐
                    │                            │
                 Build Images               DevSecOps
                    │                            │
                    │                       Trivy Scan
                    │                            │
                    │                       Security Gate
                    │                            │
                    └────────────┬───────────────┘
                                 │
                                 ▼
                             Docker Hub
                                 │
                          Images Available
                                 │
                                 ▼
                          GitOps Deployment
                                 │
                                 ▼
                              Argo CD
                                 │
                      Automated Sync / Self-Heal
                                 │
                                 ▼
                         Kubernetes Cluster
                                 │
                    ┌────────────┼─────────────┐
                    │            │             │
                    ▼            ▼             ▼
                  RBAC      Pod Security   NetworkPolicy
                    │            │             │
                    └────────────┼─────────────┘
                                 │
                                 ▼
                              Istio
                                 │
                    ┌────────────┴────────────┐
                    │                         │
             Traffic Management           Security
                    │                         │
             Canary Routing                  mTLS
             Retries                         Policies
             Timeouts
             Resilience
                    │
                    └────────────┬────────────┘
                                 │
                                 ▼
                          Ecommerce Platform
                                 │
              ┌──────────────────┼──────────────────┐
              │                  │                  │
              ▼                  ▼                  ▼
          Frontend           Microservices     Observability
                                                    │
                             ┌──────────────────────┼──────────────────────┐
                             │                      │                      │
                             ▼                      ▼                      ▼
                         Prometheus              Grafana                Loki
                             │
                             ├──────────────────────► Kiali
                             │
                             └──────────────────────► Jaeger
```

---

# Project Goals

The primary objective of this project is to build and operate a complete cloud-native application platform covering:

* Containerization
* CI/CD
* DevSecOps
* Container security
* Kubernetes
* Kubernetes RBAC
* Least-privilege access
* Pod Security
* Network Security
* Kubernetes auditing
* Secret management
* GitOps
* Argo CD
* Argo CD RBAC
* Service Mesh
* Traffic Management
* mTLS
* Resilience
* Distributed Tracing
* Metrics
* Logging
* Platform Automation
* AI-assisted Self-Healing

The business logic is intentionally simple. The main focus is the infrastructure and platform engineering layer around the application.

---

# Key Features

* 12 backend microservices
* Frontend application
* Docker containerization
* GitHub Actions CI/CD
* DevSecOps pipeline
* Trivy container vulnerability scanning
* Docker Hub image registry
* Kubernetes deployments
* Kubernetes Services
* Kubernetes RBAC
* Role and RoleBinding
* ServiceAccount authorization
* Least-privilege access control
* Namespace-level authorization
* Pod Security Standards
* Kubernetes Network Policies
* Kubernetes Audit Policy
* Kubernetes Secret configuration
* Sealed Secrets configuration
* Argo CD RBAC
* GitOps with Argo CD
* Automated synchronization
* Automated pruning
* Self-healing reconciliation
* Istio 1.30.3 service mesh
* Istio Ingress Gateway
* Envoy sidecars
* Canary traffic splitting
* Strict mTLS
* Retries
* Timeouts
* Connection pool controls
* Outlier detection
* Circuit-breaking behavior
* Distributed tracing with Jaeger
* Metrics with Prometheus
* Dashboards with Grafana
* Logs with Loki
* Service topology with Kiali
* Automated traffic generation
* Future AI-based incident detection and remediation

---

# Microservices

The platform contains the following backend services:

```text
cart-service
catalog-service
logistics-service
notification-service
order-processing-service
order-taking-service
payment-service
recommendation-service
search-service
user-service
warehouse-service
wishlist-service
```

Frontend:

```text
ecommerce-frontend
```

The backend services follow a shared FastAPI application pattern.

Service identity and version are configured through environment variables such as:

```text
SERVICE_NAME
SERVICE_VERSION
```

This keeps the application code simple while allowing the infrastructure layer to demonstrate routing, canary deployments and service-mesh behavior.

---

# Technology Stack

| Category          | Technology                          |
| ----------------- | ----------------------------------- |
| Application       | Python / FastAPI                    |
| Frontend          | Vite / TypeScript                   |
| Containers        | Docker                              |
| CI/CD             | GitHub Actions                      |
| DevSecOps         | Trivy                               |
| Registry          | Docker Hub                          |
| Orchestration     | Kubernetes                          |
| Authorization     | Kubernetes RBAC                     |
| Workload Security | Pod Security Standards              |
| Network Security  | Kubernetes NetworkPolicy            |
| Audit             | Kubernetes Audit Policy             |
| Secrets           | Kubernetes Secrets / Sealed Secrets |
| GitOps            | Argo CD                             |
| GitOps Security   | Argo CD RBAC                        |
| Service Mesh      | Istio 1.30.3                        |
| Proxy             | Envoy                               |
| Service Security  | Istio mTLS                          |
| Metrics           | Prometheus                          |
| Dashboards        | Grafana                             |
| Logging           | Loki                                |
| Tracing           | Jaeger                              |
| Service Mesh UI   | Kiali                               |
| Configuration     | Kubernetes YAML / Kustomize         |

---

# DevSecOps Pipeline

Security is integrated directly into the CI pipeline.

The pipeline follows:

```text
Developer
    │
    │ git push
    ▼
  GitHub
    │
    ▼
GitHub Actions
    │
    ├── Checkout Source
    │
    ├── Build Docker Images
    │
    ├── Trivy Vulnerability Scan
    │
    ├── Security Gate
    │
    └── Push Verified Images
            │
            ▼
        Docker Hub
```

The objective is to identify container vulnerabilities **before the image progresses toward deployment**.

---

## DevSecOps Controls

| Stage           | Tool           | Purpose                                         |
| --------------- | -------------- | ----------------------------------------------- |
| Source Control  | GitHub         | Manage application source                       |
| CI              | GitHub Actions | Automate build and validation                   |
| Container Build | Docker         | Build application images                        |
| Security Scan   | Trivy          | Detect known vulnerabilities                    |
| Security Gate   | CI workflow    | Prevent failed security checks from progressing |
| Registry        | Docker Hub     | Store container images                          |
| Deployment      | Argo CD        | GitOps-based Kubernetes deployment              |

---

# Trivy Security Scanning

Trivy is integrated into the CI pipeline to scan Docker images for known vulnerabilities.

```text
Source Code
     │
     ▼
Docker Build
     │
     ▼
Trivy Scan
     │
 ┌───┴────┐
 │        │
PASS     FAIL
 │        │
 ▼        ▼
Push    Pipeline
Image   Stops
```

This provides a basic **shift-left security** approach by moving container security checks into the CI pipeline.

---

# Docker Images

Container images are published to Docker Hub using the following naming convention:

```text
shubham379/<service>:latest
```

Examples:

```text
shubham379/frontend:latest
shubham379/cart-service:latest
shubham379/catalog-service:latest
shubham379/payment-service:latest
shubham379/search-service:latest
```

The platform currently contains images for the frontend and backend services.

---

# Kubernetes

The application runs on Kubernetes using:

* Deployments
* Services
* Namespaces
* ConfigMaps where required
* Secrets where required
* Istio sidecar injection
* Traffic generator
* Rolling deployments
* RBAC
* Pod Security
* Network Policies

Current local Kubernetes cluster:

```text
dev-cluster-control-plane
dev-cluster-worker
dev-cluster-worker2
```

Kubernetes version used in the current environment:

```text
v1.34.0
```

---

# Kubernetes Security

The platform includes security controls at the Kubernetes layer to provide authorization, workload isolation, network control and auditability.

Security controls include:

```text
Kubernetes RBAC
      │
      ├── Users
      ├── Groups
      ├── ServiceAccounts
      ├── Roles
      └── RoleBindings

Pod Security
      │
      ├── Workload restrictions
      ├── Security context
      └── Privilege control

Network Security
      │
      └── NetworkPolicy

Audit
      │
      └── Kubernetes Audit Policy

Secret Management
      │
      ├── Kubernetes Secrets
      └── Sealed Secrets configuration
```

---

# Kubernetes RBAC

Role-Based Access Control is used to control access to Kubernetes resources.

The authorization model follows:

```text
User / ServiceAccount
        │
        ▼
      Role
        │
        ▼
   RoleBinding
        │
        ▼
 Kubernetes API
```

RBAC controls operations such as:

```text
get
list
watch
create
update
patch
delete
```

Permissions can be restricted based on:

* Namespace
* Resource
* API group
* Kubernetes verb

Examples of controlled resources include:

```text
Pods
Deployments
Services
ConfigMaps
Secrets
Jobs
StatefulSets
ServiceAccounts
```

---

# Least-Privilege Access

The platform separates administrative access from application-level access.

A workload should receive only the Kubernetes permissions required to perform its function.

Example:

```text
Application
     │
     ▼
ServiceAccount
     │
     ▼
Role
     │
     ▼
RoleBinding
     │
     ▼
Required API Permissions Only
```

This follows the **principle of least privilege**.

Cluster administrators can have cluster-wide privileges while restricted users and application identities receive only required permissions.

---

# ServiceAccount Security

Application workloads can use dedicated Kubernetes ServiceAccounts rather than relying on broad administrative identities.

Example:

```text
ecommerce namespace
        │
        ▼
ecommerce-services
   ServiceAccount
        │
        ▼
ecommerce-services-role
        │
        ▼
Required Kubernetes permissions
```

ServiceAccount authorization can be explicitly tested with:

```bash
kubectl auth can-i list pods \
  --as=system:serviceaccount:ecommerce:ecommerce-services \
  -n ecommerce
```

This allows application permissions to be validated independently from administrator access.

---

# RBAC Verification

Kubernetes authorization can be tested directly using `kubectl auth can-i`.

Examples:

```bash
kubectl auth can-i get pods -n ecommerce
```

```bash
kubectl auth can-i list pods -n ecommerce
```

```bash
kubectl auth can-i create pods -n ecommerce
```

```bash
kubectl auth can-i delete pods -n ecommerce
```

ServiceAccount permissions:

```bash
kubectl auth can-i list pods \
  --as=system:serviceaccount:ecommerce:ecommerce-services \
  -n ecommerce
```

This provides a direct way to verify that RBAC policies are enforcing the intended permissions.

---

# Pod Security

Pod Security controls are included to reduce the risk of insecure workloads running inside the cluster.

The security model covers areas such as:

* Privileged workload restrictions
* Security context
* Workload isolation
* Container privilege control
* Namespace-level security enforcement

Conceptually:

```text
Application Namespace
        │
        ▼
 Pod Security Controls
        │
   ┌────┴────┐
   │         │
Validate   Restrict
   │         │
   └────┬────┘
        ▼
 Secure Workload
```

The goal is to prevent unnecessarily privileged workloads from running in the application environment.

---

# Kubernetes Network Security

Network Policies are used to control pod-to-pod communication.

Traffic can be restricted based on:

* Namespace
* Pod labels
* Ports
* Protocols
* Ingress traffic
* Egress traffic

Conceptually:

```text
Frontend
   │
   │ Allowed
   ▼
Backend Service
   │
   │ Allowed
   ▼
Required Dependency

Unnecessary Traffic
       │
       ▼
     DENIED
```

This provides an additional security boundary around the microservices architecture.

---

# Kubernetes Audit Policy

A Kubernetes Audit Policy is included to provide visibility into Kubernetes API activity.

Audit events can help identify:

* Who performed an operation
* Which resource was accessed
* Which namespace was affected
* Which Kubernetes API operation was executed
* When the operation occurred

Audit flow:

```text
User / ServiceAccount
        │
        ▼
 Kubernetes API Server
        │
        ▼
   Audit Policy
        │
        ▼
   Audit Event
        │
        ▼
Security / Operations Analysis
```

This improves operational visibility and supports security investigation.

---

# Argo CD RBAC

Argo CD access is managed separately from Kubernetes cluster administration.

Argo CD RBAC can control access to:

* Applications
* Projects
* Application resources
* Sync operations
* GitOps operations

Conceptually:

```text
User / Group
     │
     ▼
 Argo CD RBAC
     │
     ├── Application access
     ├── Project access
     └── Resource operations
```

This prevents every GitOps user from automatically receiving unrestricted Argo CD privileges.

---

# Secret Management

Secret-related Kubernetes configuration is separated from normal application configuration.

The project includes configuration for:

```text
Kubernetes Secrets
Docker registry credentials
Sealed Secrets configuration
```

Sensitive credentials should not be committed to Git in plain text.

The intended GitOps pattern is:

```text
Encrypted Secret
       │
       ▼
      Git
       │
       ▼
    Argo CD
       │
       ▼
 Kubernetes
       │
       ▼
Application Secret
```

Actual credentials should remain outside the public repository.

---

# Security Hardening Architecture

Security is implemented across multiple layers:

```text
                    Security Layers
                          │
        ┌─────────────────┼──────────────────┐
        │                 │                  │
        ▼                 ▼                  ▼
   CI Security       Kubernetes        Service Mesh
        │              Security             │
        │                 │                 │
      Trivy             RBAC               mTLS
        │           Pod Security        Authorization
        │         NetworkPolicy             │
        │           Audit Policy             │
        └─────────────────┼──────────────────┘
                          ▼
                  Secure Platform
```

The security approach therefore covers:

* Source and CI security
* Container image security
* Kubernetes authorization
* Workload security
* Network security
* Service-to-service security
* GitOps access control
* Secret management
* Auditability

---

# GitOps with Argo CD

Argo CD is used to manage Kubernetes deployments through GitOps.

The repository contains application Kubernetes manifests and Istio configuration.

```text
cloudnative-ecommerce-platform/
│
├── k8s/
│   └── Kubernetes application resources
│
└── istio/
    └── Istio configuration
```

Argo CD applications:

```text
ecommerce
ecommerce-istio
```

Current synchronization model:

```text
Git Repository
      │
      ▼
    Argo CD
      │
      ├── ecommerce
      │      └── k8s/
      │
      └── ecommerce-istio
             └── istio/
      │
      ▼
 Kubernetes Cluster
```

Both applications use:

* Automated synchronization
* Automatic pruning
* Self-healing

The Git repository acts as the desired-state source for the deployment configuration.

---

# GitOps Deployment Flow

```text
Developer
    │
    │ git push
    ▼
GitHub
    │
    ▼
Application / DevSecOps Pipeline
    │
    ├── Build
    ├── Security Scan
    └── Publish Image
            │
            ▼
        Docker Hub
            │
            ▼
       GitOps Configuration
            │
            ▼
          Argo CD
            │
            ▼
       Kubernetes
```

---

# Istio Service Mesh

Istio 1.30.3 is used as the service mesh.

Istio provides:

* Service-to-service traffic management
* mTLS
* Canary releases
* Retries
* Timeouts
* Outlier detection
* Circuit breaking
* Telemetry
* Ingress routing

Architecture:

```text
                     Istio Ingress Gateway
                              │
                              ▼
                      Ecommerce Gateway
                              │
               ┌──────────────┴──────────────┐
               │                             │
               ▼                             ▼
           Frontend                    Backend Services
                                             │
                                       Envoy Sidecars
                                             │
                                             ▼
                                           Istiod
```

---

# Istio Control Plane

Current Istio version:

```text
1.30.3
```

Check the version:

```bash
./istio-1.30.3/bin/istioctl version
```

Expected:

```text
client version: 1.30.3
control plane version: 1.30.3
data plane version: 1.30.3
```

---

# Istio Data Plane

The current platform has Envoy sidecars deployed with application workloads.

Verify the data plane:

```bash
./istio-1.30.3/bin/istioctl proxy-status
```

The proxies receive:

```text
CDS
LDS
EDS
RDS
```

configuration from Istiod.

---

# Istio Gateway

The application uses:

```text
ecommerce-gateway
```

The Istio Ingress Gateway exposes the application to incoming HTTP traffic.

For local development:

```bash
kubectl port-forward \
  -n istio-system \
  svc/istio-ingressgateway 8081:80
```

Then test:

```bash
curl -I http://localhost:8081
```

Expected response:

```text
HTTP/1.1 200 OK
server: istio-envoy
```

---

# Traffic Management

Istio manages traffic through:

```text
Gateway
VirtualService
DestinationRule
```

The platform demonstrates both ingress and service-to-service routing.

---

# Canary Deployment

The catalog service contains two versions:

```text
catalog-service-v1
catalog-service-v2
```

Traffic can be distributed using weighted routing.

Example:

```text
                 catalog-service
                       │
                 ┌─────┴─────┐
                 │           │
                 ▼           ▼
               v1 90%      v2 10%
```

This provides a foundation for:

* Canary releases
* Progressive delivery
* A/B testing
* Controlled version rollout

---

# Resilience

Istio provides resilience without requiring networking and retry logic inside every application.

Configured mechanisms include:

* Request retries
* Request timeouts
* Connection pool limits
* Outlier detection
* Circuit-breaking behavior

Example:

```text
Service
   │
   ▼
Envoy
   │
   ├── Retry
   ├── Timeout
   ├── Connection Pool
   └── Outlier Detection
```

---

# Outlier Detection

The platform uses Istio outlier detection to isolate unhealthy service endpoints.

Conceptually:

```text
Repeated 5xx errors
        │
        ▼
Endpoint detected unhealthy
        │
        ▼
Endpoint ejected
        │
        ▼
Traffic reduced / stopped
        │
        ▼
Endpoint returns after ejection period
```

This prevents unhealthy instances from continuously receiving traffic.

---

# Security — Mutual TLS

Strict mTLS is enabled using:

```text
PeerAuthentication
mode: STRICT
```

Service-to-service communication is protected by Istio.

```text
Service A
    │
    ▼
 Envoy
    │
    │ encrypted + authenticated mTLS
    ▼
 Envoy
    │
    ▼
Service B
```

This provides:

* Encryption
* Workload identity
* Mutual authentication
* Secure service-to-service communication

---

# Observability

The platform provides a complete observability stack:

```text
                    Ecommerce Platform
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
          Metrics         Logs         Traces
             │             │             │
             ▼             ▼             ▼
        Prometheus        Loki         Jaeger
             │
             ▼
          Grafana
             │
             ▼
           Kiali
```

---

# Prometheus

Prometheus collects metrics from Kubernetes and Istio workloads.

Istio Envoy sidecars expose Prometheus-compatible metrics.

Prometheus can be accessed locally using:

```bash
kubectl -n istio-system port-forward svc/prometheus 9090:9090
```

---

# Grafana

Grafana is used for metrics visualization and dashboards.

Access:

```bash
kubectl -n istio-system port-forward svc/grafana 3000:3000
```

---

# Loki

Loki provides centralized log aggregation for Kubernetes workloads.

Logs can be used for:

* Application troubleshooting
* Pod failure investigation
* Error analysis
* Operational monitoring

---

# Jaeger

Jaeger provides distributed tracing across the microservices.

Example request flow:

```text
order-taking
      │
      ▼
order-processing
      │
 ┌────┼───────────────┐
 ▼    ▼               ▼
payment warehouse   logistics
                         │
                         ▼
                    notification
```

A distributed trace can show the request path across multiple services.

Access:

```bash
kubectl -n istio-system port-forward svc/tracing 16686:80
```

---

# Kiali

Kiali provides a visual representation of the Istio service mesh.

It can be used to inspect:

* Service topology
* Workload relationships
* Request traffic
* Success/error rates
* mTLS status
* Istio configuration

Access:

```bash
kubectl -n istio-system port-forward svc/kiali 20001:20001
```

---

# Application Routing

The Istio Gateway provides path-based routing.

| Path                         | Service                  |
| ---------------------------- | ------------------------ |
| `/`                          | ecommerce-frontend       |
| `/catalog/products`          | catalog-service          |
| `/search?q=`                 | search-service           |
| `/recommendations/{user_id}` | recommendation-service   |
| `/cart/{user_id}`            | cart-service             |
| `/wishlist/{user_id}`        | wishlist-service         |
| `/orders`                    | order-taking-service     |
| `/order-processing`          | order-processing-service |
| `/payments`                  | payment-service          |
| `/logistics`                 | logistics-service        |
| `/warehouse/{product_id}`    | warehouse-service        |
| `/notifications`             | notification-service     |
| `/users/{user_id}`           | user-service             |

---

# Project Structure

```text
cloudnative-ecommerce-platform/
│
├── .github/
│   └── workflows/
│       ├── ci.yml
│       └── oldci.yml
│
├── frontend/
│   ├── src/
│   ├── Dockerfile
│   ├── nginx.conf
│   ├── package.json
│   ├── package-lock.json
│   └── vite.config.ts
│
├── services/
│   ├── common/
│   ├── cart-service/
│   ├── catalog-service/
│   ├── logistics-service/
│   ├── notification-service/
│   ├── order-processing-service/
│   ├── order-taking-service/
│   ├── payment-service/
│   ├── recommendation-service/
│   ├── search-service/
│   ├── user-service/
│   ├── warehouse-service/
│   └── wishlist-service/
│
├── k8s/
│   ├── namespace.yaml
│   ├── apps.yaml
│   ├── frontend.yaml
│   ├── traffic-generator.yaml
│   └── kustomization.yaml
│
├── istio/
│   ├── gateway.yaml
│   ├── catalog-routing.yaml
│   ├── resilience.yaml
│   ├── peer-authentication.yaml
│   ├── telemetry.yaml
│   └── kustomization.yaml
│
├── scripts/
│   ├── install-istio.sh
│   ├── deploy.sh
│   ├── generate-traffic.sh
│   └── verify.sh
│
├── argocd-rbac.yaml
├── audit-policy.yaml
├── network-policies.yaml
├── pod-security.yaml
├── pod-security-standards.yaml
├── rbac.yaml
├── sealed-docker-secret.yaml
│
├── README.md
└── requirements.txt
```

---

# Kubernetes Verification

Check cluster:

```bash
kubectl get nodes -o wide
```

Check application:

```bash
kubectl get pods -n ecommerce -o wide
```

Check services:

```bash
kubectl get svc -n ecommerce
```

Check RBAC:

```bash
kubectl get roles -n ecommerce
```

```bash
kubectl get rolebindings -n ecommerce
```

Check ServiceAccounts:

```bash
kubectl get serviceaccounts -n ecommerce
```

Check NetworkPolicies:

```bash
kubectl get networkpolicy -n ecommerce
```

---

# Argo CD Verification

List applications:

```bash
argocd app list
```

Expected:

```text
ecommerce        Synced    Healthy
ecommerce-istio  Synced    Healthy
```

Application details:

```bash
argocd app get ecommerce
```

```bash
argocd app get ecommerce-istio
```

---

# Istio Verification

Check Istio installation:

```bash
kubectl get pods -n istio-system
```

Check Istio resources:

```bash
kubectl get gateway \
  -n ecommerce
```

```bash
kubectl get virtualservice,destinationrule \
  -n ecommerce
```

Check Envoy proxies:

```bash
./istio-1.30.3/bin/istioctl proxy-status
```

Check mTLS configuration:

```bash
kubectl get peerauthentication \
  -n ecommerce
```

---

# Security Verification

RBAC:

```bash
kubectl auth can-i get pods -n ecommerce
kubectl auth can-i list pods -n ecommerce
kubectl auth can-i create pods -n ecommerce
kubectl auth can-i delete pods -n ecommerce
```

ServiceAccount:

```bash
kubectl auth can-i list pods \
  --as=system:serviceaccount:ecommerce:ecommerce-services \
  -n ecommerce
```

Network Policy:

```bash
kubectl get networkpolicy -n ecommerce
```

Pod Security:

```bash
kubectl get namespace ecommerce \
  --show-labels
```

Argo CD RBAC configuration:

```bash
kubectl get configmap \
  argocd-rbac-cm \
  -n argocd
```

---

# End-to-End Verification

The complete platform can be verified through the following flow:

```text
GitHub
   │
   ▼
GitHub Actions
   │
   ├── Build
   ├── Trivy Scan
   └── Docker Hub
          │
          ▼
       Argo CD
          │
          ▼
      Kubernetes
          │
          ▼
        Istio
          │
          ▼
    Ingress Gateway
          │
          ▼
    Ecommerce Frontend
```

Local ingress test:

```bash
kubectl port-forward \
  -n istio-system \
  svc/istio-ingressgateway 8081:80
```

Then:

```bash
curl -I http://localhost:8081
```

Expected:

```text
HTTP/1.1 200 OK
server: istio-envoy
```

---

# Useful Commands

## Kubernetes

```bash
kubectl get nodes
kubectl get pods -n ecommerce
kubectl get svc -n ecommerce
kubectl get deployments -n ecommerce
```

## Kubernetes Security

```bash
kubectl get roles -n ecommerce
kubectl get rolebindings -n ecommerce
kubectl get serviceaccounts -n ecommerce
kubectl get networkpolicy -n ecommerce
```

## RBAC Authorization

```bash
kubectl auth can-i get pods -n ecommerce
kubectl auth can-i list pods -n ecommerce
kubectl auth can-i create pods -n ecommerce
kubectl auth can-i delete pods -n ecommerce
```

## Istio

```bash
./istio-1.30.3/bin/istioctl version
./istio-1.30.3/bin/istioctl proxy-status
```

## Istio Resources

```bash
kubectl get gateway,virtualservice,destinationrule \
  -n ecommerce
```

## Argo CD

```bash
argocd app list
argocd app get ecommerce
argocd app get ecommerce-istio
```

---

# Current Platform Status

```text
Application Code              ✅
Frontend                       ✅
Docker Images                  ✅
GitHub Actions CI              ✅
DevSecOps Pipeline             ✅
Trivy Security Scan            ✅
Docker Hub Registry             ✅

Kubernetes                     ✅
Kubernetes RBAC                ✅
Role / RoleBinding              ✅
ServiceAccount Security        ✅
Least-Privilege Access         ✅
Pod Security                   ✅
Network Policies               ✅
Audit Policy                   ✅
Secret Management              ✅
Sealed Secrets Configuration   ✅

GitOps                         ✅
Argo CD                        ✅
Argo CD RBAC                   ✅
Automated Sync                 ✅
Auto Prune                     ✅
Self-Healing                   ✅

Istio 1.30.3                   ✅
Istio Gateway                  ✅
Envoy Proxies                  ✅
Canary Routing                 ✅
Strict mTLS                    ✅
Resilience Policies            ✅

Prometheus                     ✅
Grafana                        ✅
Loki                           ✅
Jaeger                         ✅
Kiali                          ✅
End-to-End Ingress             ✅

AI Detection                   🔄
AI Root Cause Analysis         🔄
AI Self-Healing                🔄
```

---

# Future Architecture — AI Self-Healing

The next evolution of the platform is an AI-driven operations and self-healing layer.

```text
                 Kubernetes
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
    Prometheus      Loki      K8s Events
        │            │            │
        └────────────┼────────────┘
                     ▼
              AI Analysis Layer
                     │
                     ▼
             Anomaly Detection
                     │
                     ▼
              Root Cause Analysis
                     │
                     ▼
             Remediation Decision
                     │
                     ▼
              Safety Validation
                     │
                     ▼
              Kubernetes / Argo CD
                     │
                     ▼
              Self-Healing Action
                     │
                     ▼
                 Verification
```

Planned capabilities:

* Automated anomaly detection
* Kubernetes failure detection
* Pod crash analysis
* Log-based root cause analysis
* Resource anomaly detection
* AI-assisted incident diagnosis
* Automated remediation
* Safe GitOps-based recovery
* Incident summarization
* Post-remediation verification

---

# Roadmap

```text
Phase 1  → Containerization                 ✅
Phase 2  → Kubernetes                       ✅
Phase 3  → CI/CD                            ✅
Phase 4  → DevSecOps / Trivy                ✅
Phase 5  → Docker Registry                  ✅
Phase 6  → GitOps / Argo CD                 ✅
Phase 7  → Istio Service Mesh               ✅
Phase 8  → Traffic Management               ✅
Phase 9  → Security / mTLS                  ✅
Phase 10 → Kubernetes RBAC                  ✅
Phase 11 → Pod Security                     ✅
Phase 12 → Network Security                 ✅
Phase 13 → Audit & Secret Security          ✅
Phase 14 → Observability                    ✅
Phase 15 → AI Detection                     🔄
Phase 16 → AI Root Cause Analysis           🔄
Phase 17 → Automated Self-Healing           🔄
```

---

# Engineering Scope

This project focuses on **DevOps, DevSecOps and Platform Engineering** rather than complex business functionality.

Primary engineering areas:

* DevOps
* DevSecOps
* CI/CD
* Docker
* Kubernetes
* Kubernetes RBAC
* Least-Privilege Security
* Pod Security
* Network Security
* Kubernetes Auditing
* Secret Management
* GitOps
* Argo CD
* Argo CD RBAC
* Istio
* Service Mesh
* mTLS
* Canary Deployment
* Traffic Management
* Resilience
* Observability
* Infrastructure Automation
* AI-assisted Operations
* Self-Healing Kubernetes

---

# Final Platform Flow

```text
Developer
    │
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ├── Build
    ├── Trivy Security Scan
    └── Push Images
            │
            ▼
        Docker Hub
            │
            ▼
       GitOps Configuration
            │
            ▼
          Argo CD
            │
            ├── RBAC
            │
            ▼
       Kubernetes Cluster
            │
            ├── Kubernetes RBAC
            ├── Pod Security
            ├── NetworkPolicy
            ├── Audit Policy
            └── Secret Management
            │
            ▼
          Istio Mesh
            │
            ├── mTLS
            ├── Canary
            ├── Retry
            ├── Timeout
            └── Resilience
            │
            ▼
       Ecommerce Platform
            │
            ▼
     Observability Stack
            │
     ┌──────┼────────┐
     ▼      ▼        ▼
 Prometheus Loki    Jaeger
     │               │
     ▼               ▼
 Grafana           Kiali
            │
            ▼
       Future AI Layer
            │
            ▼
      Self-Healing
```

---

# Author

**Subham Rathore**

DevOps / Kubernetes / Platform Engineering Project
