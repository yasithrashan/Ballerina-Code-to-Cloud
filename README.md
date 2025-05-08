# Ballerina Code to Cloud

This repository demonstrates how to use Ballerina's code-to-cloud features to automatically generate Docker and Kubernetes artifacts from your Ballerina code with minimal configuration.

## Getting Started

### Prerequisites

- [Ballerina](https://ballerina.io/downloads/) (1.2.13 or later)
- [Docker](https://www.docker.com/get-started/)
- [Kubernetes](https://kubernetes.io/docs/setup/) (for hello_k8s example)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

### Build and Run Docker Example

1. Navigate to the hello_docker directory:
   ```bash
   cd hello_docker
   ```

2. Create a message.txt file in the files directory:
   ```bash
   mkdir -p files
   echo "World" > files/message.txt
   ```

3. Build the project:
   ```bash
   bal build
   ```

4. Run the Docker container:
   ```bash
   docker run -p 9090:9090 yasithrashan/hello-world:0.1.0
   ```

5. Test the service:
   ```bash
   curl http://localhost:9090/sayHello
   ```
   
   Output should be: `hello World`

### Build and Deploy Kubernetes Example

1. Navigate to the hello_k8s directory:
   ```bash
   cd hello_k8s
   ```

2. Build the project:
   ```bash
   bal build
   ```

3. Deploy to Kubernetes:
   ```bash
   kubectl apply -f target/kubernetes/hello_k8s
   ```

4. Get the service URL:
   ```bash
   kubectl get svc
   ```

5. Test the service (use the external IP from the previous command):
   ```bash
   curl http://<EXTERNAL-IP>:9090/sayHello
   ```
   
   Output should be: `hello Kubernetes`

## How it Works

Ballerina's code-to-cloud feature automatically:

1. Generates Dockerfiles based on your Ballerina code
2. Creates Docker images with the necessary dependencies
3. For Kubernetes, generates YAML files for deploying your services
4. Copies static files to the container as specified in Cloud.toml

The `Cloud.toml` file provides configuration options for customizing the Docker image and Kubernetes deployment.

### Docker Configuration

In the `Cloud.toml` file, you can specify:
- Docker image repository, name, and tag
- Files to copy into the container
- Environment variables
- Container ports

### Kubernetes Configuration

For Kubernetes deployments, you can configure:
- Replica count
- Service type
- Resource limits
- Probes
- ConfigMaps and Secrets

## Additional Configuration Options

For more advanced configuration options, check out the following resources:
- [Ballerina Docker Guide](https://ballerina.io/learn/user-guide/deployment/docker/)
- [Ballerina Kubernetes Guide](https://ballerina.io/learn/user-guide/deployment/kubernetes/)

## License

This project is licensed under the MIT License - see the LICENSE file for details.
