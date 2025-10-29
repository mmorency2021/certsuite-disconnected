# How to Create CNF Validation Listing

This guide provides step-by-step instructions for creating a CNF validation listing on Red Hat Connect to get your CNF certified and published in the Red Hat CNF catalog.

## Overview

The Red Hat Connect platform allows CNF vendors to validate and certify their containerized network functions for Red Hat OpenShift. This process ensures your CNF meets Red Hat's standards and can be published in the official Red Hat CNF catalog.

## Prerequisites

- Red Hat Partner Connect account
- Completed CNF testing (certsuite, chart-verifier, preflight)
- CNF container images and Helm charts
- Technical contact information

## Step 1: Create Product Listing

1. **Navigate to Red Hat Connect**
   - Go to: https://connect.redhat.com/manage/products

2. **Create New Product**
   - Click on **"Create Product"** (blue button at the top)
   - Enter your **Product Name**
   - Select **"Containerized Application"**
   - Click **"Create Product"**

3. **Complete Product Details**
   - Click **"Start"** under **"Complete product listing details"**
   - Fill out all required product marketing details including:
     - Product description
     - Key features and benefits
     - Use cases
     - Technical specifications
     - Documentation links
   - Return to **"Overview"** when completed

4. **Accept Legal Agreements**
   - Review and accept any necessary legal agreements if prompted

## Step 2: Add Product Components & Begin Validation

1. **Add Component**
   - Click **"Start"** next to **"add at least one product component"**
   - Click **"Add component"**

2. **Configure Component Details**
   - Fill out your **component Name** using the recommended naming convention:
     ```
     <container-name>-<product-version>-<ocp-version>
     ```
     **Example:** `mycontainer-v1.23-OCP4.15`
   
   - Select **"CNF"** as the component type
   - Click **"Create new component"**

## Step 3: Complete Validation Workflow

1. **Start Component Validation**
   - Click on your newly created component to begin the validation/certification workflow

2. **Complete Validation Questionnaire**
   - Click on **"Complete questionnaire"**
   - Answer all required questions about your CNF including:
     - Technical specifications
     - Supported OpenShift versions
     - Resource requirements
     - Network requirements
     - Security considerations
     - Testing methodology

3. **Provide Contact Information**
   - Click on **"Contact Info"**
   - Fill out your **Technical contact email address**
   - Ensure this contact can respond to Red Hat technical inquiries

## Step 4: Submit for Review

After completing all required sections:

1. **Review Submission**
   - Verify all information is accurate and complete
   - Ensure all required fields are filled out
   - Double-check component naming and technical details

2. **Submit for Red Hat Review**
   - Submit your completed validation listing
   - Red Hat will review your submission for completeness and accuracy

## Step 5: Publication

1. **Await Approval**
   - Red Hat will review your submission
   - You will be notified via email once the review is complete

2. **Publish to Catalog**
   - Once approved, you will receive notification
   - Click the **"Publish"** button to make your CNF listing live
   - Your CNF will appear in the Red Hat CNF catalog

## Best Practices for CNF Validation Listing

### Component Naming Convention

Use descriptive and consistent naming:
```
Format: <cnf-name>-<version>-<ocp-version>
Examples:
- 5g-nssf-v2.1.0-OCP4.15
- voice-gateway-v1.5.2-OCP4.14
- ran-du-v3.0.1-OCP4.16
```

### Required Information Checklist

**Product Marketing Details:**
- [ ] Clear product description
- [ ] Key features and benefits
- [ ] Target use cases
- [ ] Competitive advantages
- [ ] Documentation links
- [ ] Support information

**Technical Component Details:**
- [ ] Container image references
- [ ] Helm chart information
- [ ] Resource requirements (CPU, memory, storage)
- [ ] Network requirements
- [ ] Supported OpenShift versions
- [ ] Security considerations
- [ ] Performance characteristics

**Testing Evidence:**
- [ ] Certsuite test results
- [ ] Chart verifier validation
- [ ] Preflight container checks
- [ ] Performance test results
- [ ] Security scan results

### Common Pitfalls to Avoid

1. **Incomplete Information**
   - Ensure all required fields are completed
   - Provide comprehensive technical specifications

2. **Poor Component Naming**
   - Avoid generic names like "component1"
   - Use version-specific naming conventions

3. **Missing Test Results**
   - Include all required validation test results
   - Ensure tests were run on supported OpenShift versions

4. **Inadequate Documentation**
   - Provide clear installation and configuration guides
   - Include troubleshooting information

## Timeline Expectations

| Phase | Typical Duration | Notes |
|-------|-----------------|-------|
| Product Creation | 1-2 hours | Initial setup and basic information |
| Component Configuration | 2-4 hours | Detailed technical specifications |
| Questionnaire Completion | 1-3 hours | Depends on CNF complexity |
| Red Hat Review | 5-10 business days | May require additional information |
| Publication | Immediate | Once approved by Red Hat |

## Support and Resources

- **Red Hat Connect Support**: Available through the platform
- **Documentation**: https://connect.redhat.com/support
- **Partner Success Team**: Contact for complex validation scenarios
- **Technical Reviews**: Red Hat engineering team reviews

## Post-Publication Maintenance

1. **Update Listings**
   - Keep product information current
   - Update for new OpenShift versions
   - Refresh test results periodically

2. **Monitor Performance**
   - Track download metrics
   - Monitor customer feedback
   - Address any reported issues

3. **Version Management**
   - Create new components for major versions
   - Maintain backward compatibility information
   - Sunset older versions appropriately

## Integration with CNF Testing

This validation listing process is the final step after completing your CNF testing workflow:

1. **Complete Testing Phase**
   - Run [Certsuite testing](disconnected-cnf-testing.md#certsuite-testing) for compliance validation
   - Execute [Chart Verifier testing](disconnected-cnf-testing.md#chart-verifier-testing) for Helm chart validation
   - Perform [Preflight testing](disconnected-cnf-testing.md#preflight-container-image-testing) for container image compliance

2. **Gather Test Results**
   - Collect all test reports and logs
   - Document any remediation steps taken
   - Prepare evidence packages for submission

3. **Submit for Validation**
   - Use this guide to create your Red Hat Connect listing
   - Upload test results as supporting evidence
   - Complete the validation questionnaire with test data

## Additional Resources

- [Red Hat Partner Connect Portal](https://connect.redhat.com/)
- [CNF Validation Process Guide](https://docs.google.com/document/d/1agqr0WkrnXAt8ZKXb5N7nr0B-tTpiPsuDn7kB80vv3A/edit?tab=t.0)
- [Red Hat Connect Support](https://connect.redhat.com/support)
- [CNF Testing Guide](disconnected-cnf-testing.md)
- [Red Hat CNF Catalog](https://catalog.redhat.com/software/containers/search?category=Networking)

## Troubleshooting Common Issues

### Login Issues
- Ensure you have a valid Red Hat Partner Connect account
- Verify your account has the necessary permissions
- Contact Red Hat Partner Success if you need account assistance

### Component Creation Problems
- Double-check naming conventions
- Ensure all required fields are completed
- Verify CNF selection is correct

### Validation Questionnaire Difficulties
- Review all test results before starting
- Have technical specifications readily available
- Contact Red Hat support for clarification on specific questions

### Review Process Delays
- Ensure all required information is provided
- Respond promptly to Red Hat inquiries
- Keep contact information current and monitored