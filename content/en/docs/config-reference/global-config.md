---
title: Global config
description: GRGate global config reference
draft: false
images: []
menu:
  docs:
    parent: config-reference
weight: 630
toc: true
---

The main configuration file can be passed to the CLI via the `--config`
argument, by default it will try to read from `/etc/grgate/config.yaml`.

```yaml
# global configuration, this is the default
globals:
  # enable GRGate, if set to false release are not published
  enabled: true

  # filter release by tag, the tag associated to the draft/unpublished releases
  # must match the regular expression defined by tagRegexp, default: .*
  tagRegexp: ".*"

  # list of statuses, default: []
  statuses:
    - e2e happy flow

  # display issue dashboard, GRGate create an issue in the repository and
  # provide feedback when mis-configuration or other issues are detected
  dashboard:
    enabled: true
    author: GRGate[bot]
    title: GRGate dashboard
    template: |-
      GRGate is {{ if .Enabled }}enabled
      {{- else }}disabled{{ end }} for this repository.
      {{- if .Errors }}

      Incorrect configuration detected with the following error(s):
      {{- range .Errors }}
      - {{ . }}
      {{- end }}
      {{- end }}

  # append statuses to release note
  releaseNote:
    enabled: true
    template: |-
      {{- .ReleaseNote -}}
      <!-- GRGate start -->
      <details><summary>Status check</summary>
      {{ range .Statuses }}
      - [{{ if or (eq .Status "completed" ) (eq .Status "success") }}x{{ else }} {{ end }}] {{ .Name }}
      {{- end }}

      </details>
      <!-- GRGate end -->

# server configuration (webhook)
# webhook should be sent to /<provider>/webhook, where provider is either
# github or gitlab
server:
  listenAddress: 0.0.0.0:8080
  metricsAddress: 0.0.0.0:9101
  probeAddress: 0.0.0.0:8086
  webhookSecret: a-random-string

# number of workers to run, default: 1
workers: 1

# platform to use
platform: github # github|gitlab, default: github

# GitHub configuration
# when creating the GitHub App, make sure to set the following permissions:
# A. for self-hosting, the following permissions are required to process
#    repositories through webhook events:
#      - Checks read-only
#      - Contents read/write
#      - Issues read/write
#      - Metadata read-only
#      - Commit statuses read-only
#    and subscribe to the following webhook events:
#      - Check runs
#      - Check suites
#      - Releases
#      - Statuses
# B. when using the cli, additional permissions are required to interact with
#    checks and commit statuses:
#      - Checks read/write
#      - Contents read/write
#      - Metadata read-only
#      - Commit statuses read/write
github:
  appID: 000000
  installationID: 00000000
  privateKeyPath: path-to-key.pem

# GitLab configuration
# when creating the Gitlab token, make sure to set the following permissions:
#   - read_repository
# subscribe to the following webhook events:
#   - Release events
#   - Pipeline events
gitlab:
  token: gitlab-token

# configuration can be overriden in the repository itself, you can define the
# default path below, default: .grgate.yaml
repoConfigPath: .grgate.yaml

logLevel: info  # trace|debug|info|warn|error|fatal|panic, default: info
logFormat: json # json|pretty, default: pretty
```
