# Install chartmuseum Component with Kubebb

## Prerequisites

1. Install [kubebb-core](https://github.com/kubebb/components/tree/main/charts/kubebb-core) v0.1.0+

2. Create a repo [kubebb](https://github.com/kubebb/components/blob/main/repos/repository_kubebb.yaml)

```shell
    kubectl apply -n kubebbs-sytem -f repos/repository_kubebb.yaml
```

## Install chartmuseum Component 


1. Apply `componentplan.yaml` or `componentplan_auth.yaml` support basic_auth

```shell
    kubectl apply -f  examples/chartmuseum/componentplan.yaml  or  kubectl apply -f  examples/chartmuseum/componentplan_auth.yaml
```

2. Get service for CLUSTER-IP

```shell
    kubectl get svc -n kubebb-system
    NAME          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
    chartmuseum   ClusterIP   10.96.116.173   <none>        8080/TCP   17h 
```

3. According to clusterIP, change below spec.url and save into `repository_chartmuseum.yaml`

```yaml
apiVersion: core.kubebb.k8s.com.cn/v1alpha1
kind: Repository
metadata:
  name: chartmuseum
  namespace: kubebb-system
spec:
  url: http://10.96.116.173:8080
  pullStategy:
    intervalSeconds: 120
    retry: 5
```

4. Apply `repository_chartmuseum.yaml`

```shell
    kubectl apply -f repository_chartmuseum.yaml
```



