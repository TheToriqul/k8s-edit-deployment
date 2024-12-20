# Kubernetes Deployment Management Command Reference

### Project Content Table
- [Core Operations](#core-operations)
- [Deployment Management](#deployment-management)
- [Troubleshooting](#troubleshooting)
- [Advanced Operations](#advanced-operations)

> **Author**: [Md Toriqul Islam](https://linkedin.com/in/thetoriqul)  
> **Description**: Comprehensive command reference for Kubernetes deployment management  
> **Note**: Review commands carefully before execution in your environment

## Core Operations

### Creating the Initial Deployment
```bash
# Create a new deployment with Nginx
kubectl create deployment my-nginx --image=nginx:1.28 --replicas=3

# Verify deployment creation
kubectl get deployments
kubectl get pods

# Check deployment details
kubectl describe deployment my-nginx
```

### Deployment Inspection
```bash
# Get detailed deployment information
kubectl get deployment my-nginx -o wide

# Export deployment configuration to YAML
kubectl get deployment my-nginx -o yaml > my-nginx-deployment.yaml

# View deployment events
kubectl describe deployment my-nginx

# Check pod status and events
kubectl describe pods
```

## Deployment Management

### Modifying Deployments
```bash
# Edit deployment directly (opens default editor)
kubectl edit deployment my-nginx

# Apply changes from a modified YAML file
kubectl apply -f my-nginx-deployment.yaml

# Update container image
kubectl set image deployment/my-nginx nginx=nginx:latest

# Scale deployment
kubectl scale deployment my-nginx --replicas=5
```

### Rollout Management
```bash
# Check rollout status
kubectl rollout status deployment/my-nginx

# View rollout history
kubectl rollout history deployment/my-nginx

# Rollback to previous version
kubectl rollout undo deployment/my-nginx

# Rollback to specific revision
kubectl rollout undo deployment/my-nginx --to-revision=2
```

## Troubleshooting

### Pod Inspection
```bash
# Get pod logs
kubectl logs <pod-name>

# Get logs from previous instance
kubectl logs <pod-name> --previous

# Stream pod logs
kubectl logs -f <pod-name>

# Check pod events
kubectl describe pod <pod-name>
```

### Resource Cleanup
```bash
# Delete specific deployment
kubectl delete deployment my-nginx

# Delete using YAML file
kubectl delete -f my-nginx-deployment.yaml

# Force delete stuck resources
kubectl delete pod <pod-name> --grace-period=0 --force
```

## Advanced Operations

### Resource Management
```bash
# Get resource usage
kubectl top pods

# View pod details in JSON format
kubectl get pod <pod-name> -o json

# Watch for changes
kubectl get pods -w
```

### Debugging Tools
```bash
# Execute command in container
kubectl exec -it <pod-name> -- /bin/bash

# Copy files from/to pod
kubectl cp <pod-name>:/path/to/file ./local/path

# Port forwarding
kubectl port-forward <pod-name> 8080:80
```

## Learning Notes

1. Always verify deployment status after changes
2. Use `--record` flag to track command history
3. Implement rolling updates for zero-downtime deployments
4. Regular backup of deployment configurations is recommended
5. Monitor resource usage during scaling operations

---

> 💡 **Best Practice**: Always use version control for deployment configurations

> ⚠️ **Warning**: Test changes in development environment first

> 📝 **Note**: Keep deployment configurations as code for reproducibility