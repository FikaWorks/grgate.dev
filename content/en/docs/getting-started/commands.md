---
title: "Commands"
description: "GRGate comes with commands for common tasks."
lead: "GRGate comes with commands for common tasks."
draft: false
images: []
menu:
  docs:
    parent: "getting-started"
weight: 130
toc: true
---

## run

The run command list all the draft/unpublished releases from a given repository
that match the provided tag. From this list, if all the status check are
completed and successful and match the list of provided status, then the
release is published.

```
Usage:
  grgate run [OWNER/REPOSITORY] [flags]
```

The example below run GRGate against the FikaWorks/my-repo repository, publish
draft release which with tag matching a stable semver tag (ie: v1.2.3) and both
statuses e2e-happyflow and e2e-useraccountflow succeeded:

```bash
grgate run FikaWorks/my-repo \
  --tag-regexp "^v[0-9]+\.[0-9]+\.[0-9]+$" \
  -s e2e-happyflow \
  -s e2e-useraccountflow
```

## serve

The serve command create 3 HTTP server with the following functionalities:
- 0.0.0.0:8080 listen for git webhook
- 0.0.0.0:9101 expose Prometheus metrics at `/metrics`
- 0.0.0.0:8086 expose health probe, liveness: `/live` and readiness: `/ready`

```
Usage:
  grgate serve [flags]
```

## status

Interact with commit status.

```
Usage:
  grgate status [command]

Available Commands:
  get         Get a status attached to a given commit by name
  list        List statuses attached to a given commit
  set         Set a status to a given commit
```

### status get

Get the status associated to a given commit sha.

```
Usage:
  grgate status get [OWNER/REPOSITORY] [flags]
```

The example below get the e2e-happy-flow status associated to the commit sha
36a2dabd4cc732ccab2657392d4a1f8db2f9e19e:

```bash
grgate status get my-org/my-repo \
  --commit 36a2dabd4cc732ccab2657392d4a1f8db2f9e19e \
  --name e2e-happy-flow
```

### status list

List status associated to a given commit sha.

```
Usage:
  grgate status list [OWNER/REPOSITORY] [flags]
```

The example below list all statuses associated to the commit
36a2dabd4cc732ccab2657392d4a1f8db2f9e19e:

```bash
grgate status list my-org/my-repo \
  --commit 36a2dabd4cc732ccab2657392d4a1f8db2f9e19e
```

### status set

Set status and state for a given commit sha.

```
Usage:
  grgate status set [OWNER/REPOSITORY] [flags]
```

{{< alert icon="💡" text="The --state flag is only required when interacting with Github repositories and can be omitted when interacting with GitLab repositories" />}}

The example below set the e2e-happy-flow status to completed:

```
grgate status set my-org/my-repo \
  --commit 36a2dabd4cc732ccab2657392d4a1f8db2f9e19e \
  --name e2e-happy-flow \
  --status completed \
  --state success
```
