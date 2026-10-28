# Docker & Container Security Assessment

## Student Details
- **Name:** Sparsh Singhal
- **Registration Number:** `202401100100250`
- **Port:** `8049`(8050 is already occupied elsewhere)
- **Docker Hub:** [sparsh450/fest-backend](https://hub.docker.com/repository/docker/sparsh450/fest-backend)

## Project Overview
This project demonstrates Docker containerization, security hardening, Docker Compose, vulnerability scanning using Trivy, and image signing using Cosign.


## Docker Hub Images
Repository: repository/docker/sparsh450/fest-backend

- `sparsh450/fest-backend:1.0.0`
- `sparsh450/fest-backend:1.0`
- `sparsh450/fest-backend:1.0.1` — unsigned verification-test image

**Version 1.0.0 digest:**

```
sha256:ae358a0a9e7512c8f043c4767a049220dfbc33f9ad1f5e305277157bf0463aa4
```

## Security Measures
- Backend runs as a non-root user.
- Dependencies are specified in `requirements.txt`.
- Docker Compose uses a dedicated network and persistent database volume.
- Trivy scans the container image for vulnerabilities.
- Cosign signs and verifies the published image by digest.
- `.env` and private signing keys are excluded from Git.

## Trivy Vulnerability Results

| Severity | Before | After |
|---|---:|---:|
| Critical | 0 | 0 |
| High | 6 | 5 |
| Medium | 14 | 2 |
| Low | 4 | 1 |
| **Total** | **24** | **8** |

Reported findings decreased by **66.7%**, from 24 to 8. Five High-severity findings remain and require review.

Detailed reports: `reports/trivy-before.txt` and `reports/trivy-after.txt`.

## Cosign Signing and Verification

### Sign Version 1.0.0

```bash
cosign sign --key cosign.key \
  yashsinghal307/fest-backend@sha256:148ec8566ec5607b91245bd9943ab2ef2c3504b427fb58056716cc6038d48d89
```

### Verify the Signed Image

```bash
cosign verify --key cosign.pub \
  sparsh450/fest-backend@sha256:d7877a7787025a648dd7df89ee3115dae5f139ece31cfd6c98d5099602a916af
```

Verification succeeded for version `1.0.0`.

### Verify the Unsigned Version 1.0.1

```bash
cosign verify --key cosign.pub \
  sparsh450/fest-backend@sha256:sha256:565f822345548b6250a220745cb22fe6ff2ba6484177bceca7f59fae39461d04
```



## AI Tools Disclosure
Gemini was used for technical troubleshooting, Docker and Cosign guidance, interpreting Trivy results, and documentation assistance.

## Conclusion
The project demonstrates container hardening, vulnerability scanning, and image signature verification. Trivy findings decreased from 24 to 8, and Cosign successfully verified the signed image while rejecting the unsigned test image.