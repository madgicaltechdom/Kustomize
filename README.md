# Kubernetes Configuration Management with Kustomize

## Introduction

This repository demonstrates how to manage Kubernetes configurations using Kustomize. It includes an original directory with standard Kubernetes manifests and a solution directory with Kustomize-based configurations for better scalability and maintainability. The solution is structured with a base configuration and overlays for different environments (dev and prod).

## Prerequisites

Before proceeding, ensure you have the following installed:

- kubectl
- Kustomize(If you have kubernetes version greater than 1.21, it already installed)
- A running Kubernetes/Minikube cluster

## Practical Example: Using Kustomize in Kubernetes Deployment
To demonstrate Kustomize in action, we structured the repository as follows:
```
.
├── original
│   ├── configmap.yaml
│   ├── deployment.yaml
│   └── service.yaml
├── README.md
└── solution
    ├── base
    │   ├── config.properties
    │   ├── deployment.yaml
    │   ├── kustomization.yaml
    │   └── service.yaml
    └── overlays
        ├── dev
        │   ├── config.properties
        │   ├── kustomization.yaml
        │   └── replicas.yaml
        └── prod
            ├── config.properties
            ├── kustomization.yaml
            └── replicas.yaml
```

Look at this step-by-step user guide [video](https://drive.google.com/file/d/1UlcIo0npBkFMk31Q5HQ5TceYHHu1ppVx/view).

1. Clone the Repository

   ```
   git clone https://github.com/madgicaltechdom/Kustomize.git
   cd Kustomize
   ```

2. Deploy the Original Kubernetes Manifests

- To deploy the original Kubernetes configurations without Kustomize:

   ```
   kubectl apply -f original/
   ```

3. Deploy with Kustomize

- To see the overall code preview run the below command:

  ```
  kubectl kustomize solution/base
  ```

- Apply the base configuration:

  ```
  kubectl apply -k solution/base
  ```

- Apply the development environment configuration:

  ```
  kubectl apply -k solution/overlays/dev
  ```

  In this, I am deploying the base things with 2 replicas.

- Apply the production environment configuration:
  ```
  kubectl apply -k solution/overlays/prod
  ```
  In this, I am deploying the base things with 5 replicas.

4. Verify the Deployment

   Check if the pods and services are running:

   ```
   kubectl get pods
   kubectl get services
   ```

## NOTE:-

   - The original directory contains the common Kubernetes Manifests files.
   - The base directory contains the common configuration applied across all environments.
   - The overlays directory contains modifications for different environments.

## Conclusion

This repository demonstrates how to manage Kubernetes configurations using Kustomize effectively. By leveraging base and overlay configurations, teams can maintain consistency across different environments while reducing duplication.

## License

This project is licensed under the MIT License.
