Create the objects defined in a configuration file:
```
kubectl create -f nginx.yaml
```

Delete the objects defined in two configuration files:
```
kubectl delete -f nginx.yaml -f redis.yaml
```

Update the objects defined in a configuration file by overwriting the live configuration:
```
kubectl replace -f nginx.yaml
```