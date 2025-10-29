# Certsuite Disconnected Environment Guide

This repository contains comprehensive documentation for running CNF (Cloud Native Function) testing tools in disconnected/air-gapped environments.

## 📚 Documentation

- **[CNF Testing in Disconnected Environments](disconnected-cnf-testing.md)** - Complete guide for Certsuite, Chart Verifier, and Preflight testing

## 🛠️ Tools Covered

- **Certsuite**: Red Hat Best Practices Test Suite for Kubernetes
  - Binary installation methods
  - Disconnected environment configuration
  - Custom probe image setup
  - Comprehensive test suite coverage

- **Chart Verifier**: Helm chart validation tool
  - Configuration setup for 5g-cnf environments
  - Chart testing with custom values
  - CNF lifecycle management

- **Preflight**: Container image compliance testing
  - Private registry authentication
  - Batch image processing
  - Compliance report generation

## 🚀 Quick Start

1. **Install Tools**: Follow the installation guides for each tool
2. **Setup Private Registry**: Mirror required images to your private registry
3. **Configure Environment**: Set up kubeconfig and configuration files
4. **Run Tests**: Execute testing workflows in your disconnected environment

## 📋 Prerequisites

- Access to a private container registry
- Kubernetes/OpenShift cluster access
- Valid kubeconfig file
- `podman` or `docker` installed

## 🔗 Additional Resources

- [Certsuite Official Documentation](https://redhat-best-practices-for-k8s.github.io/certsuite/)
- [Chart Verifier Documentation](https://github.com/redhat-certification/chart-verifier)
- [Preflight Documentation](https://github.com/redhat-openshift-ecosystem/openshift-preflight)
- [Red Hat Partner Connect Portal](https://connect.redhat.com/)

## 📄 Usage

See the [main documentation file](disconnected-cnf-testing.md) for detailed installation and usage instructions.

## 🤝 Contributing

This documentation is maintained to help teams successfully implement CNF testing in disconnected environments. Feel free to submit issues or improvements.