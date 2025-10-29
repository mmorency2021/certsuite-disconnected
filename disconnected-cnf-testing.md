# CNF Testing in Disconnected Environments

This guide provides step-by-step instructions for running CNF (Cloud Native Function) testing tools in disconnected/air-gapped environments.

## Table of Contents
- [Certsuite Testing](#certsuite-testing)
- [Chart Verifier Testing](#chart-verifier-testing)
- [Preflight Container Image Testing](#preflight-container-image-testing)

---

## Certsuite Testing

Certsuite is a test suite for validating CNF best practices and compliance in Kubernetes environments.

### Prerequisites
- Access to a private container registry
- `podman` or `docker` installed
- `certsuite` CLI tool installed (see installation steps below)
- Valid kubeconfig file
- Go 1.21+ (if building from source)

### Installing Certsuite Binary

You can install the certsuite binary using several methods:

#### Method 1: Download Pre-compiled Binary (Recommended)

Download the latest release from the GitHub releases page:

```bash
# Set the version you want to download (check latest releases)
CERTSUITE_VERSION="v5.5.7"

# Download for Linux x86_64
curl -L -o certsuite "https://github.com/redhat-best-practices-for-k8s/certsuite/releases/download/${CERTSUITE_VERSION}/certsuite-${CERTSUITE_VERSION}-linux-amd64"

# Make it executable
chmod +x certsuite

# Move to a directory in your PATH
sudo mv certsuite /usr/local/bin/

# Verify installation
certsuite version
```

#### Method 2: Build from Source

If you need the latest features or want to build for disconnected environments:

```bash
# Clone the repository
git clone https://github.com/redhat-best-practices-for-k8s/certsuite.git
cd certsuite

# Build the binary
make build-certsuite-tool

# The binary will be created in the current directory
# Move it to your PATH
sudo cp ./certsuite /usr/local/bin/

# Verify installation
certsuite version
```

#### Method 3: Install via Go (Development)

For developers or if you want the latest development version:

```bash
# Install directly with Go
go install github.com/redhat-best-practices-for-k8s/certsuite/cmd/certsuite@latest

# Verify installation (ensure $GOPATH/bin is in your PATH)
certsuite version
```

#### OCP >= 4.12 Setup

For OpenShift Container Platform 4.12 and later, add required labels to the default namespace:

```bash
oc label namespace/default pod-security.kubernetes.io/enforce=privileged
oc label namespace/default pod-security.kubernetes.io/enforce-version=latest
```

### Step 1: Prepare Probe Image for Private Registry

First, pull the certsuite probe image from the public registry and push it to your private registry:

```bash
# Pull the latest probe image
podman pull quay.io/redhat-best-practices-for-k8s/certsuite-probe:latest

# Tag the image for your private registry
podman tag quay.io/redhat-best-practices-for-k8s/certsuite-probe:latest myregistry.com/test/certsuite-probe:latest

# Push to your private registry
podman push myregistry.com/test/certsuite-probe:latest
```

### Step 2: Setup Configuration Directories

Create directories for configuration and results:

```bash
# Create directories for configuration and results
mkdir -p ~/certsuite-config
mkdir -p ~/certsuite-results

# Copy your kubeconfig
cp ~/.kube/config ~/certsuite-config/kubeconfig

# Copy Docker credentials (if needed for Preflight tests)
cp ~/.docker/config.json ~/certsuite-config/dockerconfig
```

### Step 3: Prepare Certsuite Configuration File

Create a comprehensive configuration file (`~/certsuite-config/certsuite_config.yml`) to specify your test parameters:

```yaml
targetNameSpaces:
  - name: 5g-nssf
podsUnderTestLabels: []
  # Uncomment and modify as needed:
  # - 'redhat-best-practices-for-k8s.com/generic: target'
operatorsUnderTestLabels:
  - "app.kubernetes.io/name: your-operator"
targetCrdFilters: []
managedDeployments: []
managedStatefulsets: []
acceptedKernelTaints: []
skipScalingTestDeployments: []
skipScalingTestStatefulsets: []
skipHelmChartList: []
validProtocolNames: []
servicesignorelist: []
executedBy: ""
partnerName: ""
collectorAppPassword: ""
collectorAppEndpoint: "http://claims-collector.cnf-certifications.sysdeseng.com"
connectAPIConfig:
  baseURL: "https://access.redhat.com/hydra/cwe/rest/v1.0"
  apiKey: ""
  projectID: ""
  proxyURL: ""
  proxyPort: ""
```

### Step 4: Run Certsuite Tests

Execute the certsuite with your custom probe image and configuration:

#### Using Binary with Custom Probe Image:

```bash
# Run certsuite with custom probe image for disconnected environment
certsuite run \
  --certsuite-probe-image myregistry.com/test/certsuite-probe:latest \
  --label-filter common,telco,extended \
  --config-file ~/certsuite-config/certsuite_config.yml \
  --kubeconfig ~/certsuite-config/kubeconfig \
  --output-dir ~/certsuite-results \
  --non-intrusive-only
```

#### Alternative Command Options:

```bash
# Run specific test suites only
certsuite run \
  --config-file ~/certsuite-config/certsuite_config.yml \
  --kubeconfig ~/certsuite-config/kubeconfig \
  --output-dir ~/certsuite-results \
  --label-filter networking,lifecycle \
  --non-intrusive-only

# Run all tests with debug logging
certsuite run \
  --config-file ~/certsuite-config/certsuite_config.yml \
  --kubeconfig ~/certsuite-config/kubeconfig \
  --output-dir ~/certsuite-results \
  --log-level debug \
  --non-intrusive-only
```

**Parameters Explained:**
- `--certsuite-probe-image`: Points to your private registry probe image
- `--label-filter`: Test suites to run (common, telco, extended, networking, lifecycle, etc.)
- `--config-file`: Path to your configuration file
- `--kubeconfig`: Path to your kubeconfig file
- `--output-dir`: Output directory for test results and logs
- `--non-intrusive-only`: Run only non-intrusive tests (recommended for production)
- `--log-level`: Logging verbosity (debug, info, warn, error)

### Available Test Suites

| Suite                    | Description                              | Tests                            |
| ------------------------ | ---------------------------------------- | -------------------------------- |
| access-control           | Service account, RBAC, security contexts | Security and access controls     |
| affiliated-certification | Red Hat certification status             | Container/operator certification |
| lifecycle                | Pod deployment, creation, shutdown       | Application lifecycle            |
| networking               | Connectivity and network configuration   | Network policies, services       |
| operator                 | Kubernetes Operator functionality        | Operator best practices          |
| platform-alteration      | Platform configuration modifications     | Platform integrity               |
| observability            | Logging and monitoring practices         | Logs, metrics, CRD status        |
| common                   | Basic compliance tests                   | Essential best practices         |
| telco                    | Telco-specific requirements              | Telco CNF requirements           |
| extended                 | Extended test coverage                   | Additional compliance tests      |

**Note:** The output directory will contain all certsuite log files, test results in JSON format, HTML reports, and a compressed archive for easy sharing.

---

## Chart Verifier Testing

Chart verifier validates Helm charts against best practices and compliance requirements.

### Prerequisites
- `chart-verifier` CLI tool installed
- `oc` or `kubectl` CLI tools
- Access to the target Kubernetes cluster
- Helm charts to be tested

### Step 1: Prepare Configuration File

Create a configuration file (`5g-cnf-config.yaml`) for chart testing:

```yaml
chart-testing:
  buildId: 1.241022.9208240
  upgrade: false
  skipMissingValues: true
  namespace: 5g-cnf
  releaseLabel: "app.kubernetes.io/instance"
```

### Step 2: Set CNF Project as Default in Kubeconfig

Set your CNF project as the default namespace in your kubeconfig:

```bash
oc project 5g-cnf
```

### Step 3: Run Helm Chart Test

Execute the chart verifier with your configuration and chart files:

```bash
chart-verifier verify --config 5g-cnf-config.yaml 5g-cnf-global-25a/ \
  -F 5g-cnf-global-24a/values_rhocp.yaml \
  -F 5g-cnf-global-24a/5g-cnf.yaml \
  --helm-install-timeout 10m0s
```

**Parameters Explained:**
- `--config`: Path to your chart-verifier configuration file
- `5g-cnf-global-25a/`: Path to the Helm chart directory
- `-F`: Values files to use during chart installation
- `--helm-install-timeout`: Maximum time to wait for Helm installation

### Chart Verifier Behavior

**Important Note:**
Chart-verifier will **tear down the CNF** once it finishes testing. If you want to leave the CNF running after testing, add the `-c` flag to the end of the chart-verifier command:

```bash
chart-verifier verify --config 5g-cnf-config.yaml 5g-cnf-global-25a/ \
  -F 5g-cnf-global-24a/values_rhocp.yaml \
  -F 5g-cnf-global-24a/5g-cnf.yaml \
  --helm-install-timeout 10m0s \
  -c
```

---

## Preflight Container Image Testing

Preflight is used to validate container images for compliance and best practices before deployment.

### Prerequisites
- `preflight` CLI tool installed
- Access to container images (either in registry or locally)
- Valid Red Hat credentials (if checking Red Hat certification requirements)

### Step 1: Basic Container Image Check

Run preflight against a container image:

```bash
preflight check container <image-reference>
```

### Step 2: Check Container Image from Private Registry

For images in private registries, you may need authentication:

```bash
# Using podman/docker credentials
preflight check container myregistry.com/myproject/myimage:latest

# With specific credentials
preflight check container myregistry.com/myproject/myimage:latest \
  --docker-config ~/.docker/config.json
```

### Step 3: Generate Compliance Reports

Generate detailed reports for certification purposes:

```bash
preflight check container myregistry.com/myproject/myimage:latest \
  --output-format json \
  --output-file preflight-results.json
```

### Step 4: Check Multiple Images

For batch processing multiple container images:

```bash
#!/bin/bash
images=(
  "myregistry.com/project/image1:latest"
  "myregistry.com/project/image2:latest"
  "myregistry.com/project/image3:latest"
)

for image in "${images[@]}"; do
  echo "Checking image: $image"
  preflight check container "$image" \
    --output-format json \
    --output-file "preflight-$(basename $image .latest).json"
done
```

---

## Best Practices for Disconnected Environments

### General Recommendations

1. **Image Management:**
   - Maintain a local mirror of all required container images
   - Use consistent tagging strategies across environments
   - Implement image scanning and vulnerability management

2. **Configuration Management:**
   - Store all configuration files in version control
   - Use environment-specific configuration files
   - Document all custom configurations and their purposes

3. **Testing Strategy:**
   - Run tests in staging environments that mirror production
   - Automate testing workflows where possible
   - Maintain test result archives for compliance auditing

4. **Troubleshooting:**
   - Enable verbose logging during initial setup
   - Keep detailed logs of all testing activities
   - Document any custom workarounds for disconnected environments

### Common Issues and Solutions

- **Image Pull Failures:** Ensure all required images are available in your private registry
- **Network Connectivity:** Verify that your testing tools can reach the private registry
- **Authentication Issues:** Confirm that proper credentials are configured for registry access
- **Timeout Issues:** Increase timeout values for operations in slower disconnected environments

---

## Additional Resources

- [Certsuite Official Documentation](https://redhat-best-practices-for-k8s.github.io/certsuite/)
- [Certsuite Source Repository](https://github.com/redhat-best-practices-for-k8s/certsuite)
- [Certsuite Test Catalog](https://github.com/redhat-best-practices-for-k8s/certsuite/blob/main/CATALOG.md)
- [Running Certsuite Guide](https://github.com/mmorency2021/running-certsuite?tab=readme-ov-file#scenario-2-running-certsuite-with-binary)
- [Chart Verifier Documentation](https://github.com/redhat-certification/chart-verifier)
- [Preflight Documentation](https://github.com/redhat-openshift-ecosystem/openshift-preflight)
- [Red Hat Partner Connect Portal](https://connect.redhat.com/)