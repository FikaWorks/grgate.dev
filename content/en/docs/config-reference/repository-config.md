---
title: Repository config
description: GRGate repository config reference
lead: GRGate repository config reference
draft: false
images: []
menu:
  docs:
    parent: config-reference
weight: 630
toc: true
---

If you create a file named `.grgate.yaml` at the root of the repository, GRGate
will read it before processing the repository.

The `globals:` section of the GRGate global configuration can be overriden from
the repository itself.

```yaml
# toggle processing of the repository
enabled: true

# only process releases with tag matching a regular expression pattern
tagRegexp: "v1.0.0-beta-\d*"

# list of statuses required to get releases merged
statuses:
  - E2e happy flow
  - E2e feature A
  - E2e feature B
```
