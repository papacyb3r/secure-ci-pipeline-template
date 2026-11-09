# Secure CI Pipeline Template

A drop-in GitHub Actions workflow that adds three automated security checks to any repository. Copy [.github/workflows/security.yml](.github/workflows/security.yml) into your project.

## What it checks

| Check | Tool | Catches |
|---|---|---|
| Secret scanning | Gitleaks | API keys, tokens and passwords committed to the repository, including history |
| Static analysis (SAST) | Semgrep | Insecure code patterns and common vulnerability classes |
| Vulnerabilities and misconfiguration | Trivy | Known vulnerabilities in dependencies, plus infrastructure-as-code misconfigurations |

The workflow runs on pushes to main, on pull requests, and on demand.

## How to use it

1. Copy the workflow file into .github/workflows/ in your repository.
2. Push. The checks run automatically and appear on pull requests.
3. Make the checks required in branch protection so insecure changes cannot be merged.

## Design choices

- **Least privilege:** the workflow token has read-only access to repository contents.
- **Fail the build:** Semgrep and Trivy return a failing status when they find issues, so problems are visible.
- **Fixable first:** Trivy reports only HIGH and CRITICAL findings that have a fix available, to keep noise down.

## Hardening tips

- Pin actions to a full commit SHA instead of a version tag to reduce supply-chain risk.
- Tune severity thresholds and rules to your risk appetite.
- Add a software bill of materials (SBOM) step and dependency review for pull requests.

## Notes

The included app.py is a trivial sample so the pipeline has something to scan.

## Author

Papa, GRC, Risk & Cybersecurity Compliance Leader. [LinkedIn](https://www.linkedin.com/in/owoahene)
