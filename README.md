SBOM Vulnerability Scanning Workflows
This repository is configured to automatically scan Software Bill of Materials (SBOM) files for vulnerabilities using two different tools: Grype and OWASP Dependency-Track Bomber. Both workflows run in GitHub Actions and are triggered on pushes or manual dispatch.
Workflows
1. Grype SBOM Scan
Tool: Grype
Trigger: Any push to *.json or *.xml files, or manual run
What it does:
Scans all SBOM JSON and XML files in the repository
Generates vulnerability reports and a summary table
Uploads results as workflow artifacts
2. Bomber SBOM Scan
Tool: OWASP Dependency-Track Bomber
Trigger: Any push to *.json or *-sbom.xml files, or manual run
What it does:
Scans all SBOM JSON and SBOM XML files in the repository
Generates HTML, JSON, and Markdown vulnerability reports
Uploads results as workflow artifacts
Requires OSS Index credentials (see below)
Setup Instructions
OSS Index Credentials for Bomber
The Bomber workflow requires credentials for the OSS Index vulnerability database:
Create an account at OSS Index.
Generate an API token in your OSS Index account settings.
Add the following secrets to your GitHub repository:
BOMBER_PROVIDER_USERNAME (your OSS Index username/email)
BOMBER_PROVIDER_TOKEN (your OSS Index API token)
Go to Repository Settings → Secrets and variables → Actions to add these secrets.
Artifacts
After each scan, results are uploaded as workflow artifacts. You can download these from the "Actions" tab in your repository after a workflow run.
Customization
You can adjust the file patterns in the workflow YAMLs to match your SBOM naming conventions.
Both workflows can be triggered manually from the GitHub Actions UI.
References
Grype Documentation
Bomber Documentation
OSS Index
