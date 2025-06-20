# Workflows-CI

This repository contains an example Argo **app-of-apps** configuration that
deploys workflow templates and an event sensor for building Docker and Helm
artifacts. The build pulls source from `gogs.local` and pushes container images
and Helm charts to `harbor.local/library`.

## Files

- `argo/app-of-apps.yaml` – Root Argo CD application that loads child apps from
the `argo/applications` folder.
- `argo/applications/workflows-app.yaml` – Deploys the workflow templates
  located under `argo/workflows`.
- `argo/workflows/build-workflow-template.yaml` – Workflow template that lints,
  tests, builds and pushes Docker images and Helm charts.
- `argo/events/gogs-event-source.yaml` – EventSource for receiving Gogs
  webhooks.
- `argo/events/build-sensor.yaml` – Sensor that triggers the build workflow when
a webhook event is received.

Credentials for accessing Gogs and pushing to Harbor must be provided through
Kubernetes secrets named `gogs-credentials` and `harbor-credentials`. Additional
parameters can be set via workflow or sensor arguments.
