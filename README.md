# istio

```
Component	Description
Envoy Proxy	Sidecar proxy injected into each pod, handles all network traffic
Pilot	Manages and configures proxies
Istiod	Core control plane component (manages discovery, security, and configs)
Mixer (deprecated)	Used to handle policies and telemetry, phased out
Ingress/Egress Gateway	Handles traffic entering/leaving the mesh
✅ Typical Use Cases

    Secure service-to-service traffic with mTLS

    Deploying canary releases

    Adding rate limits per service

    Enforcing zero-trust policies

    Visualizing traffic with Kiali or Grafana

⚙️ Deploy Istio on EKS (Quick Start)
1. Install istioctl

curl -L https://istio.io/downloadIstio | sh -
cd istio-*
export PATH=$PWD/bin:$PATH

2. Install Istio on Your Cluster

istioctl install --set profile=demo -y

You can choose other profiles: default, minimal, preview, remote.
3. Label Your Namespace

kubectl label namespace default istio-injection=enabled

This enables automatic sidecar injection (adds Envoy proxy).
4. Deploy a Sample App

kubectl apply -f samples/bookinfo/platform/kube/bookinfo.yaml

Then expose it with a Gateway:

kubectl apply -f samples/bookinfo/networking/bookinfo-gateway.yaml

5. Access the App

Get the external IP:

kubectl get svc istio-ingressgateway -n istio-system

Then access: http://<EXTERNAL-IP>/productpage
🔐 mTLS Example (Security)

Enable strict mTLS between services:

apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: default
  namespace: default
spec:
  mtls:
    mode: STRICT

📊 Observability (Optional Add-ons)

Install Istio add-ons for monitoring:

kubectl apply -f samples/addons

Tools included:

    🔍 Kiali – Service mesh visualizer

    📊 Grafana – Metrics dashboard

    🔬 Jaeger – Distributed tracing

    📈 Prometheus – Metrics collection

Access Kiali:

kubectl port-forward svc/kiali -n istio-system 20001:20001

Then go to http://localhost:20001.
💡 Istio vs Linkerd vs AWS App Mesh
Feature	Istio	Linkerd	AWS App Mesh
Complexity	High	Low	Medium
mTLS	Yes	Yes (on by default)	Yes
Cloud native	Kubernetes-focused	Lightweight	AWS-integrated
Observability	Excellent	Good	Moderate
🧩 Integration with AWS Services

    Use AWS ALB/NLB in front of Istio ingress

    Secure ingress traffic with ACM (SSL) and Route 53

    Use IAM Roles for Service Accounts (IRSA) if Istio services call AWS APIs

Would you like help deploying Istio with a real-world app, integrating with AWS ALB, or setting up strict mTLS and RBAC? I can build out a full YAML or Terraform plan.
```
