
![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Warning.svg/156px-Warning.svg.png)

## Status of this repo is Proof of Concept. Please don't use!

## DBaaS Catalog
Welcome! This repository is OLM Catalog for DBaaS

### build log

```
mkdir catalog/percona-xtradb-cluster-operator ; cd catalog/percona-xtradb-cluster-operator
cat << EOF >> veneer.yaml
Schema: olm.semver
GenerateMajorChannels: true
GenerateMinorChannels: false
Stable:
  Bundles:
  - Image: quay.io/operatorhubio/percona-xtradb-cluster-operator:v1.10.0
EOF

opm alpha render-veneer semver -o yaml < veneer.yaml > catalog.yaml
opm validate .

cd ../..

podman build . -f dbaas-catalog.Dockerfile -t ghcr.io/percona-lab/dbaas-catalog:latest
podman push ghcr.io/percona-lab/dbaas-catalog:latest
```
