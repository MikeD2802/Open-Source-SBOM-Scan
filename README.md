# SBOM Vulnerability Scanning Workflows

This repository is configured to automatically scan Software Bill of Materials (SBOM) files for vulnerabilities using two different tools: **Grype** and **OWASP Dependency-Track Bomber**. Both workflows run in GitHub Actions and are triggered on pushes or manual dispatch.

## Repository Structure

- `sboms/` - Directory for storing SBOM files to be scanned
- `scan-results/` - Directory for storing scan results (in the `sbom-scan-results` branch)
- `.github/workflows/` - Contains the workflow definitions

## Workflows

### 1. Grype SBOM Scan

- **Tool:** [Grype](https://github.com/anchore/grype)
- **Trigger:** Any push to `*.json` or `*.xml` files in the `sboms/` directory, or manual run
- **What it does:**
  - Scans all SBOM JSON and XML files in the `sboms/` directory
  - Generates text and JSON vulnerability reports
  - Stores results in timestamped folders in the `sbom-scan-results` branch

### 2. Bomber SBOM Scan

- **Tool:** [OWASP Dependency-Track Bomber](https://github.com/devops-kung-fu/bomber)
- **Trigger:** Any push to `*.json` or `*.xml` files in the `sboms/` directory, or manual run
- **What it does:**
  - Scans all SBOM JSON and XML files in the `sboms/` directory
  - Generates HTML, JSON, and Markdown vulnerability reports
  - Stores results in timestamped folders in the `sbom-scan-results` branch
  - Requires OSS Index credentials (see below)

## Setup Instructions

### OSS Index Credentials for Bomber

The Bomber workflow requires credentials for the OSS Index vulnerability database:

1. **Create an account** at [OSS Index](https://ossindex.sonatype.org/).
2. **Generate an API token** in your OSS Index account settings.
3. **Add the following secrets** to your GitHub repository:
   - `BOMBER_PROVIDER_USERNAME` (your OSS Index username/email)
   - `BOMBER_PROVIDER_TOKEN` (your OSS Index API token)

Go to **Repository Settings → Secrets and variables → Actions** to add these secrets.

## Results Storage

Scan results are stored in the `sbom-scan-results` branch with the following structure:
```
scan-results/
└── [SBOM_FILENAME]-[TIMESTAMP]/
    ├── [SBOM_FILENAME].scan-results.txt    # Grype text output
    ├── [SBOM_FILENAME].scan-results.json   # Grype JSON output
    ├── [SBOM_FILENAME]-bomber-results.html # Bomber HTML output
    ├── [SBOM_FILENAME]-bomber-results.json # Bomber JSON output
    └── [SBOM_FILENAME]-bomber-results.md   # Bomber Markdown output
```

## Usage

1. Add your SBOM files (JSON or XML) to the `sboms/` directory
2. Push the changes to trigger the workflows
3. Results will be automatically stored in the `sbom-scan-results` branch
4. View results in the timestamped folders under `scan-results/`

## References

- [Grype Documentation](https://github.com/anchore/grype)
- [Bomber Documentation](https://github.com/devops-kung-fu/bomber)
- [OSS Index](https://ossindex.sonatype.org/)
