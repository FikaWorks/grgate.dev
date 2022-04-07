---
title: "Repository config"
description: "GRGate repository config reference"
lead: ""
draft: false
images: []
menu:
  docs:
    parent: "config-reference"
weight: 630
toc: true
---

The `globals:` section of the GRGate configuration can be overriden from the
repository itself. If you create a file named `.grgate.yaml` at the root of the
repository, GRGate will read it before processing the repository.

```yaml
# only process releases with tag matching a regular expression pattern
tagRegexp: v1.0.0-beta-\d*

# automerge release if the following status succeeded
statuses:
  - e2e-with-feature-A-on
  - e2e-with-feature-B-on
```
