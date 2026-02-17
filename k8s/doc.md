# PicoClaw Kubernetes Manifests

This directory contains Kubernetes manifest files for running PicoClaw on Kubernetes.

## Prerequisites

- Kubernetes cluster (v1.20 or higher recommended)
- `kubectl` command-line tool
- PicoClaw Docker image (`picoclaw:latest`)

## Deployment Steps

### 1. Configure ConfigMap

Edit `configmap.yaml` and add the contents of `config/config.json`:

```yaml
data:
  config.json: |
    {
      "your": "configuration"
    }
```

### 2. Deploy with Kustomize

Deploy all resources (namespace, configmap, pvc, and gateway) at once:

```bash
kubectl apply -k .
```

### 3. Run Agent Job (Optional)

If you need to run a one-shot query with the agent:

```bash
kubectl apply -f agent-job.yaml
```

## Cleanup

Delete all resources using Kustomize:

```bash
kubectl delete -k .
```

## Notes

- PersistentVolumeClaim uses `ReadWriteOnce` mode, so it cannot be mounted by multiple Pods simultaneously
- Gateway Deployment replica count is set to 1
- You may need to specify `storageClassName` depending on your environment
