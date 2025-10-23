# Exercise 2 - Use External Scalers. Keda

- Have your Function with the replicas value set to 1 to prevent the internal Serverless HPA creation.

## Exercise 2.1 HPA


- step1:
Initially deployed serveless python 3.12 function with a single replica....  
As shwon below, no HPA in place yet:  

```
kubectl get hpa faas-srv  -n xp264-050 --kubeconfig ~/.kube/kubeconfig-b84edf3.yaml
Error from server (NotFound): horizontalpodautoscalers.autoscaling "faas-srv" not found
```

- step2:
Scale-out to 5 replicas 
```
kubectl autoscale function faas-srv  -n xp264-050 --cpu-percent=50 --min=5 --max=10 --kubeconfig ~/.kube/kubeconfig-b84edf3.yaml
horizontalpodautoscaler.autoscaling/faas-srv autoscaled
```


- step3:  

After a littlr while the HPA will be up and running:  
s
```
kubectl get hpa faas-srv  -n xp264-050 --kubeconfig ~/.kube/kubeconfig-b84edf3.yaml                                             
NAME       REFERENCE           TARGETS              MINPODS   MAXPODS   REPLICAS   AGE
faas-srv   Function/faas-srv   cpu: <unknown>/50%   5         10        0          11s

kubectl get hpa faas-srv  -n xp264-050 --kubeconfig ~/.kube/kubeconfig-b84edf3.yaml
NAME       REFERENCE           TARGETS       MINPODS   MAXPODS   REPLICAS   AGE
faas-srv   Function/faas-srv   cpu: 3%/50%   5         10        5          93s
```

- step4:
scale down from 5 to 2 replicas by editiong the `horizontalpodautoscaler.autoscaling/faas-srv` resource

```
kubectl edit hpa faas-srv  -n xp264-050 --kubeconfig ~/.kube/kubeconfig-b84edf3.yaml
horizontalpodautoscaler.autoscaling/faas-srv edited
```

- step5:
scale back to a single replica. how this is to be done ?

In order to scale down from 2 or 5 replicas to 1 replica just remove the HPA resource?

- 
What about scaling down to zero ?



## Exercise 2.2 KEDA

After completing these steps you will have...


## Summary

You've now ...

Continue to - [Exercise 3 - Exploring Kyma Telemetry with SAP Cloud Logging](../ex3/README.md)
