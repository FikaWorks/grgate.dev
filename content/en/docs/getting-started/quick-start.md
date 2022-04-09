---
title: Quick Start
description: GRGate quick start guide
lead: Quick start guide to get started with GRGate.
draft: false
images: []
menu:
  docs:
    parent: getting-started
weight: 110
toc: true
---

There is multiple options to install GRGate in a git repository. The preferred
option being to self host GRGate yourself but you can also decide to install
GRGate from the GitHub marketplace.

## Using the GRGate GitHub App

1. Install the [GRGate GitHub App][github-market-place] to your repository or
organisation
2. Create a `.grgate.yaml` file at the root of your repository with the
following configuration:

    ```yaml
    # automerge releases if the following status succeeded
    statuses:
      - e2e happy flow
      - e2e feature A
    ```

3. Create a draft release
4. Start updating commits using the [GRGgate CLI][release-page], for example
(GitHub):

    ```bash
    grgate status set your-org/your-repository-name \
        --commit 93431f42d5a5abc2bb6703fc723b162a9d2f20c3 \
        --name "e2e happyflow" \
        --status completed \
        --state success
    ```

    ```bash
    grgate status set your-org/your-repository-name \
        --commit 93431f42d5a5abc2bb6703fc723b162a9d2f20c3 \
        --name "e2e happyflow" \
        --status completed \
        --state success
    ```

5. After GRGate process the repo, the draft release will be published!

## Self hosting GRGate using Helm chart

A Helm chart is available in the [FikaWorks Helm charts
repository][helm-charts].

Create a GitHub APP or GitLab token, then update the `values.yaml` file.

```bash
helm repo add fikaworks https://fikaworks.github.io/helm-charts
```

```bash
helm install --name grgate --values my-values.yaml fikaworks/grgate
```

## Running GRGate in Docker

```bash
docker run -ti -p 8080:8080 -p 8086:8086 -p 9101:9101 \
    -v $PWD/config.yaml:/etc/grgate/config.yaml \
    -v $PWD/github.private-key.pem:/etc/grgate/github.private-key.pem \
    fikaworks/grgate
```

## Exposed endpoints

By default GRGate expose the following endpoints:

| Address                       | Description                                 |
|-------------------------------|---------------------------------------------|
| `http://0.0.0.0:8080`         | Webserver which listen to webhooks          |
| `http://0.0.0.0:9101/metrics` | Prometheus metrics                          |
| `http://0.0.0.0:8086/ready`   | Readiness probe                             |
| `http://0.0.0.0:8086/live`    | Liveness probe                              |

<!-- page links -->
[helm-charts]: https://github.com/FikaWorks/helm-charts
[release-page]: https://github.com/fikaworks/grgate/releases
[github-market-place]: https://github.com/marketplace/grgate
