# Deploy Redis to k8s use statefulset

## Create a namespace
```
kubectl create ns redis
```

## Define a storage class
- This article uses persistent volume for the purposes of the demo with local storage (a file system folder). You can skip this section if you have some other storage provisioner.

```
kubectl apply -f sc.yaml
```

## Create a persistent volume
```
kubectl apply -f pv.yaml
```

## Create the ConfigMap
```
kubectl apply -n redis -f redis-config.yaml
```

## Deploy Redis using StatefulSet
```
kubectl apply -n redis -f redis-statefulset.yaml
```

## Create headless service
```
kubectl apply -n redis -f redis-service.yaml
```

## Check

### get log
```
kubectl -n redis logs redis-0
```

```
kubectl -n redis describe pod redis-0
```

### access to redis
```
kubectl -n redis exec -it redis-0 -- sh
redis-cli 
auth a-very-complex-password-here
```

### add a key-value
```
SET emp1 raja
SET emp2 mano
SET emp3 ram
```

```
KEYS *
```