# Certsuite Disconnected Environment Guide

This repository contains comprehensive documentation for running CNF (Cloud Native Function) testing tools in disconnected/air-gapped environments and creating Red Hat validation listings.

## 📚 Documentation

- **[CNF Testing in Disconnected Environments](disconnected-cnf-testing.md)** - Complete guide for Certsuite, Chart Verifier, and Preflight testing
- **[CNF Validation Listing Guide](cnf-validation-listing-guide.md)** - Step-by-step process for Red Hat Connect validation and catalog publication

## 🛠️ Tools Covered

### Testing Tools
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

### Validation & Certification
- **Red Hat Connect**: CNF validation listing creation
  - Product and component setup
  - Validation questionnaire completion
  - Red Hat catalog publication process
  - Post-publication maintenance

## 🚀 Quick Start

### For CNF Testing
1. **Install Tools**: Follow the installation guides for each testing tool
2. **Setup Private Registry**: Mirror required images to your private registry
3. **Configure Environment**: Set up kubeconfig and configuration files
4. **Run Tests**: Execute testing workflows in your disconnected environment

### For CNF Validation Listing
1. **Complete Testing**: Run all required CNF tests (certsuite, chart-verifier, preflight)
2. **Gather Results**: Collect test reports and compliance evidence
3. **Create Listing**: Follow the Red Hat Connect validation process
4. **Publish**: Submit for review and publish to Red Hat CNF catalog

## 📋 Prerequisites

- Access to a private container registry
- Kubernetes/OpenShift cluster access
- Valid kubeconfig file
- `podman` or `docker` installed
- Red Hat Partner Connect account (for validation listing)

## 🔗 Additional Resources

- [Certsuite Official Documentation](https://redhat-best-practices-for-k8s.github.io/certsuite/)
- [Chart Verifier Documentation](https://github.com/redhat-certification/chart-verifier)
- [Preflight Documentation](https://github.com/redhat-openshift-ecosystem/openshift-preflight)
- [Red Hat Partner Connect Portal](https://connect.redhat.com/)
- [Red Hat CNF Catalog](https://catalog.redhat.com/software/containers/search?category=Networking)

## 📄 Usage

### Testing Workflow
1. Start with [CNF Testing Guide](disconnected-cnf-testing.md) for comprehensive testing instructions
2. Complete all required validations in your disconnected environment
3. Gather test results and compliance reports

### Validation Workflow  
1. Use [CNF Validation Listing Guide](cnf-validation-listing-guide.md) to create Red Hat Connect listings
2. Submit test evidence and complete validation questionnaire
3. Publish to Red Hat CNF catalog after approval

## 🤝 Contributing

This documentation is maintained to help teams successfully implement CNF testing in disconnected environments and navigate the Red Hat validation process. Feel free to submit issues or improvements.

## 📋 Repository Structure

```
├── README.md                           # This file
├── disconnected-cnf-testing.md         # CNF testing in disconnected environments
└── cnf-validation-listing-guide.md     # Red Hat Connect validation process
```