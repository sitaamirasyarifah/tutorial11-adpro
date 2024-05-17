## Tutorial 11 - Deployment on Kubernetes
Nama: Sita Amira Syarifah

NPM: 2206023023

Kelas: C


### Reflection on Hello Minikube

1. **Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?**

Yes, there is a difference before and after the service is exposed. After being exposed, the service can accept requests so that logs will record the requests made, for example as shown in the image where the service sends multiple /GET requests if the hello-node service is refreshed multiple times.


2. **Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?**

The difference between the two syntaxes is that using `-n`, we indicate that the desired service comes from the namespace. This is necessary, for example, if there are many different services with the same name spread across multiple namespaces. By using `-n`, we focus the GET on the namespace provided after the `-n` flag.
