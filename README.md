# OpenTofu Shared AWS Provider Installation

This directory contains a shared AWS provider installation for OpenTofu, allowing multiple projects to use the same provider binaries without re-downloading them.

## Overview

The shared provider installation is configured through two main files:
- `~/.tofurc` - Main configuration that points to this shared installation
-  [tofu.tfrc](tofu.tfrc) - Update configuration for installing new provider versions

## Current Configuration

### Global Configuration (`~/.tofurc`)
```hcl
provider_installation {
  filesystem_mirror {
    path    = "[this_dir]/.terraform/providers"
    include = ["registry.opentofu.org/hashicorp/aws"]
  }
  direct {
    exclude = ["registry.opentofu.org/hashicorp/aws"]
  }
}
```

This makes AWS provider downloads to use the local mirror.

## Provider Update Process

1. Specify the desired version still missing from the mirror in the `~/opentofu/providers.tf`
2. Run init with the override `TF_CLI_CONFIG_FILE=tofu.tfrc tofu init`. This will download the latest AWS provider to this dir.
