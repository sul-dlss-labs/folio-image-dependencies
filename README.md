# folio-image-dependencies

To update the versions of the folio dependencies, edit the copy_images.yml file with the updated image versions for elasticsearch and kafka. Make a PR and merge into the `main` branch. The new folio images will be in the github package container registry for the organization.

To use the saved image use the created GHCR image tag in the helm values for the chart e.g.:

## Elasticsearch
```
image:
  repository: "ghcr.io/sul-dlss-labs/folio-elasticsearch"
  tag: "8.6.2-debian-11-r10"
```
```
sysctlImage:
  repository: "ghcr.io/sul-dlss-labs/folio-os-shell"
```
```
metrics:
  enabled: true
  image:
    repository: ghcr.io/sul-dlss-labs/folio-elasticsearch-exporter
    tag: 1.5.0-debian-11-r80
```

## Kafka
```
image:
  repository: "ghcr.io/sul-dlss-labs/folio-kafka"
  tag: "3.9.0-debian-12-r1"
```
```
metrics:
  jmx:
    image:
      repository: ghcr.io/sul-dlss-labs/folio-jmx-exporter
      tag: 1.0.1-debian-12-r9
```

## Postfix/Mail
`helm pull bokysan/mail` will copy the updated mail package to this repo. To install the mail package use:

```
helm install -n ${namespace} -f helm-postfix.yaml mail mail-[chart-version].tgz
```
