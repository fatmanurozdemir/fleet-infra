# fleet-infra

This repository contains the configuration and resources required to manage the deployment of applications and infrastructure in a Kubernetes cluster using **Flux** and GitOps principles.

---

## Overview

**fleet-infra** serves as the central repository for managing cluster configurations, Helm releases, and GitOps workflows. It integrates with Flux to ensure the cluster state reflects the desired configurations defined in this repository.

---

## Prerequisites

1. **Kubernetes Cluster**: Ensure a Kubernetes cluster is available and accessible.
2. **Flux Installed**: Flux must be installed and configured in the cluster.
3. **Git Repository Access**: The cluster must have access to this Git repository for synchronization.

---

## How to Use

### 1. Set Up the Repository
1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/fleet-infra.git
   cd fleet-infra
   ```

2. Modify or add cluster-specific configurations under the `clusters/` directory.

### 2. Deploy Flux
1. Install Flux in your cluster:
   ```bash
   flux install
   ```

2. Point Flux to this repository:
   ```bash
   flux create source git fleet-infra \
     --url=https://github.com/<your-username>/fleet-infra \
     --branch=main \
     --interval=1m \
     --export > ./clusters/<cluster-name>/flux-system/gitrepository.yaml
   ```

3. Apply the Flux configuration:
   ```bash
   kubectl apply -k ./clusters/<cluster-name>/flux-system
   ```
