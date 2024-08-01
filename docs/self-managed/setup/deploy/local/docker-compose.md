---
id: docker-compose
title: "Docker Compose"
keywords: ["camunda docker"]
---

* Docker Compose configuration -- to run -- Zeebe, Operate, Tasklist, Optimize, Identity, and Connectors Bundle
  * [Check camunda-platform repository](https://github.com/camunda/camunda-platform/blob/main/docker-compose.yaml)
  * [Follow README](https://github.com/camunda/camunda-platform#using-docker-compose)
  * vs [Docker images](/self-managed/setup/deploy/other/docker.md)
    * Docker images
      * 👁️-- are supported for -- production usage 👁️
    * Docker Compose files
      * uses
        * by developers / run a local environment
        * document way / components -- are -- wired together
        * ❌NOT for production ❌
  * recommendation 
    * 👁️ [Kubernetes | production ](/self-managed/setup/install.md) 👁️
    * [Helm + KIND | local environments ](/self-managed/setup/deploy/local/local-kubernetes-cluster.md)
      * 👁️ better than Docker Compose 👁️
        * Reason: 🧠 much closer -- to -- production systems 🧠

## Web Modeler

* Docker Compose configuration -- to run -- Web Modeler
  * [Check camunda-platform](https://github.com/camunda/camunda-platform/blob/main/docker-compose-web-modeler.yaml)
  * [Follow README](https://github.com/camunda/camunda-platform#web-modeler-self-managed)
