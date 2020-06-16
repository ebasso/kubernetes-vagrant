
To deploy Dashboard, execute following command:

```sh
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.1/aio/deploy/recommended.yaml
```

To access Dashboard from your local workstation you must create a secure channel to your Kubernetes cluster. Run the following command:

```sh
$ kubectl proxy
```
Now access Dashboard at:

[`http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/`](
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/).


Apply the changes:

```sh
$ kubectl apply -f yamls/kubernetes-dashboard-service-np.yaml
```

Get the authentication token to use on the Kubernetes Dashboard authentication realm:

```sh
$ kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```

Access the Kubernetes Dashboard using the URL https://172.42.42.100:30002/#/login using the previous token:




