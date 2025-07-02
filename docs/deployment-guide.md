# Deployment Guide

## Prerequisites

1. EKS cluster with Istio installed
2. ArgoCD installed and configured
3. PostgreSQL RDS instance
4. GitHub repository access

## Deployment Steps

### 1. Apply ArgoCD Application

```bash
kubectl apply -f argocd-apps/istio-app-production.yaml
```

### 2. Verify Deployment

```bash
# Check ArgoCD application
kubectl get applications -n argocd

# Check application pods
kubectl get pods -n istio-app

# Check Istio configuration
kubectl get gateway,virtualservice,destinationrule -n istio-app
```

### 3. Access Application

Get the Istio ingress gateway URL:

```bash
kubectl get svc istio-ingressgateway -n istio-system
```

### 4. Monitor Deployment

- ArgoCD UI: Check sync status
- Kubernetes: Monitor pod health
- Istio: Verify service mesh metrics

## Troubleshooting

### Common Issues

1. **Pods not starting**: Check resource limits
2. **Gateway not accessible**: Verify Istio configuration
3. **ArgoCD sync issues**: Check repository access

### Verification Commands

```bash
# Check Istio proxy status
istioctl proxy-status

# Verify mTLS
istioctl proxy-config cluster <pod-name> -n istio-app

# Check ArgoCD sync
argocd app get istio-app-production
```
