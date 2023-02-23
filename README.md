# Kustomize v5 YAML Anchor bug

Works with v4:
```
$ go install sigs.k8s.io/kustomize/kustomize/v4@latest 
go: downloading sigs.k8s.io/kustomize/kustomize v0.0.0-20191024000301-ce7ebe3299dd

$ $(go env GOPATH)/bin/kustomize build
apiVersion: v1
data:
  key1: value1
  key2: value2
  key3: value3
kind: ConfigMap
metadata:
  name: cm1
---
apiVersion: v1
data:
  keya: value1
  keyb: value2
  keyc: value2
kind: ConfigMap
metadata:
  name: cm2

```

Fails with v5:
```
$ go install sigs.k8s.io/kustomize/kustomize/v5@latest
go: downloading sigs.k8s.io/kustomize/kustomize/v5 v5.0.0
go: downloading sigs.k8s.io/kustomize/kyaml v0.14.0
go: downloading sigs.k8s.io/kustomize/api v0.13.1
go: downloading sigs.k8s.io/kustomize/cmd/config v0.11.0

$ $(go env GOPATH)/bin/kustomize build
Error: invalid Kustomization: error converting YAML to JSON: yaml: unmarshal errors:
  line 25: key "fieldPath" already set in map
  line 34: key "fieldPath" already set in map

```