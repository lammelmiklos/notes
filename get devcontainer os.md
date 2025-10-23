# Get the OS version of a devcontainer

```bash
IMG="mcr.microsoft.com/devcontainers/universal:latest"
REPO="devcontainers/universal"
REF="${IMG##*:}"   # "latest"

# 1) Get the multi-arch index (manifest list) and pick linux/amd64
IDX_JSON=$(curl -fsSL \
  -H 'Accept: application/vnd.oci.image.index.v1+json, application/vnd.docker.distribution.manifest.list.v2+json' \
  "https://mcr.microsoft.com/v2/${REPO}/manifests/${REF}")

IMG_MANIFEST_DIGEST=$(echo "$IDX_JSON" \
  | jq -r '.manifests[] | select(.platform.os=="linux" and .platform.architecture=="amd64") | .digest')

# 2) Get that image manifest, then read its config digest
CFG_DIGEST=$(curl -fsSL \
  -H 'Accept: application/vnd.oci.image.manifest.v1+json, application/vnd.docker.distribution.manifest.v2+json' \
  "https://mcr.microsoft.com/v2/${REPO}/manifests/${IMG_MANIFEST_DIGEST}" \
  | jq -r '.config.digest')

# 3) Fetch the config blob and print labels (often includes the base OS tag)
curl -fsSL "https://mcr.microsoft.com/v2/${REPO}/blobs/${CFG_DIGEST}" \
  | jq '.config.Labels'

```


```bash
IMG="mcr.microsoft.com/devcontainers/python:3.13"
REPO="devcontainers/python"
REF="${IMG##*:}"   # "3.13.9"

# 1) Get the multi-arch index (manifest list) and pick linux/amd64
IDX_JSON=$(curl -fsSL \
  -H 'Accept: application/vnd.oci.image.index.v1+json, application/vnd.docker.distribution.manifest.list.v2+json' \
  "https://mcr.microsoft.com/v2/${REPO}/manifests/${REF}")

IMG_MANIFEST_DIGEST=$(echo "$IDX_JSON" \
  | jq -r '.manifests[] | select(.platform.os=="linux" and .platform.architecture=="amd64") | .digest')

# 2) Get that image manifest, then read its config digest
CFG_DIGEST=$(curl -fsSL \
  -H 'Accept: application/vnd.oci.image.manifest.v1+json, application/vnd.docker.distribution.manifest.v2+json' \
  "https://mcr.microsoft.com/v2/${REPO}/manifests/${IMG_MANIFEST_DIGEST}" \
  | jq -r '.config.digest')

# 3) Fetch the config blob and print labels (often includes the base OS tag)
curl -fsSL "https://mcr.microsoft.com/v2/${REPO}/blobs/${CFG_DIGEST}" \
  | jq '.config.Labels'

```
