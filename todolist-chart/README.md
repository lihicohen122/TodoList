# TodoList Helm Chart

Helm chart for the todolist app with MariaDB and PVC.

## Installation

Install this chart from GitHub Container Registry:

```bash
helm install my-release oci://ghcr.io/lihicohen122/todolist/todolist --set database.password=<YOUR-PASSWORD>
```

Or with a specific version:

```bash
helm install my-release oci://ghcr.io/lihicohen122/todolist/todolist:0.1.0 --set database.password=<YOUR-PASSWORD>
```

## Access the Application

After installation:

1. Start minikube tunnel (as Administrator):
   ```bash
   minikube tunnel
   ```

2. Access the application:
   - Frontend: http://127.0.0.1
   - API: http://127.0.0.1/todos
   - WebUI: http://127.0.0.1/webui

## Configuration

Key configurable parameters in `values.yaml`:

- `database.password` - MySQL root password (required, set via --set)
- `frontend.replicas` - Number of frontend replicas (default: 1)
- `backend.replicas` - Number of backend replicas (default: 1)
- `frontend.serviceType` - Frontend service type (default: LoadBalancer)
- `env.user` - User name (default: lihi-cohen)
- `env.mysqlHost` - MySQL host (default: mariadb-headless)
- `frontend.apiBaseUrl` - API base URL (default: /todos)

## Components

- **StatefulSet**: MariaDB database with headless service and PVC
- **Deployments**: Frontend (todolist-vue), Backend (todos-api), WebUI
- **ConfigMaps**: Configuration for frontend, backend, and webui
- **Secrets**: Database passwords for backend and webui
- **Ingress**: Routes traffic to frontend, backend, and webui
- **Network Policies**: Security policies for all components
- **HPA**: Horizontal Pod Autoscaler for backend and frontend

## Uninstall

```bash
helm uninstall my-release
```

