# Creating a POD using YAML

## YAML?

Kubernetes uses YAML as inputs for the creation of objects such as:

- PODs
- Replicas
- Deployments
- Services
- Etc.

All of these follow a similar structure, the Kubernetes definition file always contains 4 top level fields:

```yaml
apiVersion:
kind:
metadata:
spec:
```

Let's take a look at each one:

**apiVersion**

The version of the Kubernetes API you are using to create the objects, depending on what we are trying to create we must use the right API version, for now, since we are working on PODs we will set the `apiVersion` as `v1`.  
Here are some of the values it has:

| Kind       | Version |
| ---------- | ------- |
| Pod        | v1      |
| Service    | v1      |
| ReplicaSet | apps/v1 |
| Deployment | apps/v1 |

**kind**

The kind refers to the type of object we are triying to create, we could use the values in the column Kind of the table above, in this case, we'll use `Pod`.

**metadata**

This is data about the objects like its name (string), labels (dictionary), etc.

**spec**

This is the specification of the object we are creating, this is the place where we provide additional information to Kubernetes pertaining to this object, this is different for different objects so it's very important to refer to the documentation to get the right format for each.

So after I explained all that, this would be the final result for creating our POD:

File `pod-definition.yml`
```yaml
apiVersion: v1

kind: Pod

metadata:
  name: myapp-pod
  labels:
    app: myapp
    type: front-end

spec:
  containers:
    - name: nginx-container
      image: nginx
```

Once that you have your configuration YAML file ready, run the following command:

```
kubectl create -f pod-definition.yml
```

To see your POD run these commands:

```
kubectl get pods
kubectl describe pod myapp-pod
```

