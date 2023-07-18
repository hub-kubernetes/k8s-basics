
A service can be created either using a YAML file or by using the kubectl utility 

## Cluster IP 

```
vi service.yaml 

apiVersion: v1
kind: Service
metadata:
  name: nginx-clusterip
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP

```

OR 

```
kubectl expose deploy nginx --port=80 --type=ClusterIP --name=nginx-clusterip
```

## NodePort 

```
vi service-nodeport.yaml

apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: NodePort

```

OR 

```
kubectl expose deploy nginx --port=80 --type=NodePort --name=nginx-nodeport

```

## LoadBalancer (Only on top of cloud providers)

```
vi service-lb.yaml

apiVersion: v1
kind: Service
metadata:
  name: nginx-lb
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: LoadBalancer
```

OR 

```
kubectl expose deploy nginx --port=80 --type=LoadBalancer --name=nginx-lb
```

To view the services use the `kubectl get service` command 

## --external-ip flag

```
kubectl run nginx --image=nginx
kubectl expose pod nginx --external-ip={Routable IP address of your VM} --port=80 --target-port=80
```
