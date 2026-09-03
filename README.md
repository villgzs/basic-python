[Official release is here: https://github.com/home-assistant/docker/releases/tag/2026.07.0](https://github.com/home-assistant/docker-base/releases/tag/2026.06.1)

# THIS IS NOT OFFICIAL RELEASE !

---
⚠️ **IMPORTANT DISCLAIMER**

  Unofficial Build: This repository is not created or supported by the official Home Assistant team. Please do not submit issue reports or complaints to Home Assistant developers.

  32-bit Deprecation: Official support for 32-bit systems (armv7) has ended. This repository was created strictly for experimental/testing purposes following official build instructions.

  No Warranty & No Support: This repository is untested and unmaintained. Do not run this in a production environment.

  Limitation of Liability: The creator of this repository assumes no responsibility or liability for any failures, data loss, or damage to hardware. No claims or demands for damages will be entertained.

USE AT YOUR OWN RISK.
---

Prereq.: STEP No.1 (Basic-Alpine)

### Step No.2 

# Alpine Home Assistant Base Image with Python extension - for arm 32bit platforms

Multi-stage Docker image based on Alpine Linux with:

- **jemalloc** (memory allocator)
- **s6-overlay** (process supervisor)
- **bashio** (Home Assistant bash helpers)
- **tempio** (templating tool)

## Supported platforms

- `linux/arm/v7`
- `linux/arm/v6`

## Quick start

### Local build (single architecture)

```bash
docker buildx build \
  --platform linux/amd64 \
  -t my-base:local \
  --load \
  .
```

### Multi-arch build + push to GHCR

A GitHub Actions workflow is already included (`.github/workflows/docker-build.yml`).

1. Push the repository to GitHub.
2. Enable GitHub Packages (or just use the default GITHUB_TOKEN permissions).
3. On every push to `main`/`master` or on tags (`v*`) the image is automatically built and pushed to:

```
ghcr.io/<your-username>/<repo-name>
```

### Manual trigger

You can also run the workflow manually from the **Actions** tab and choose:

- which platforms to build
- whether to push the image or not

## Image tags

| Tag pattern              | Description                          |
|--------------------------|--------------------------------------|
| `latest`                 | Latest build from `main`/`master`    |
| `sha-<commit>`           | Specific commit                      |
| `v1.2.3` / `1.2` / `1`   | Semantic version tags                |
| branch name              | Branch builds                        |

## Usage example

```dockerfile
FROM ghcr.io/<your-username>/<repo-name>:latest

# your addon / application layers...
```

## Root filesystem

Place any files you want in the final image under the `rootfs/` directory.
They will be copied into the image root (`/`).

## Notes

- The Dockerfile requires **Docker BuildKit** (enabled by default in modern Docker and GitHub Actions).
- `TARGETARCH` and `TARGETVARIANT` are automatically provided by Buildx.
- Cache is shared via GitHub Actions cache for faster rebuilds.

