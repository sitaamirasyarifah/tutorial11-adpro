## Tutorial 11 - Deployment on Kubernetes
Nama: Sita Amira Syarifah

NPM: 2206023023

Kelas: C


### Reflection on Hello Minikube

1. **Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?**

Yes, there is a difference before and after the service is exposed. After being exposed, the service can accept requests so that logs will record the requests made, for example as shown in the image where the service sends multiple /GET requests if the hello-node service is refreshed multiple times.


2. **Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?**

The difference between the two syntaxes is that using `-n`, we indicate that the desired service comes from the namespace. This is necessary, for example, if there are many different services with the same name spread across multiple namespaces. By using `-n`, we focus the GET on the namespace provided after the `-n` flag.


### Reflection on Rolling Update & Kubernetes Manifest File
1. **What is the difference between Rolling Update and Recreate deployment strategy?**

   The main difference between the rolling update and recreate deployment strategies is that in recreate deployment, there will be downtime during the application update because this strategy requires removing the previous application and then redeploying the new application. Therefore, downtime occurs after removal and completion of deployment. In contrast, rolling update gradually changes the application to its latest version. In other words, rolling update can update the application gradually without significant downtime.


2. **Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt. Reference: https://dev.to/cloudskills/kubernetes-deployment-strategy-recreate-3kgn**

First, I will recreate the springboot-petclinic-rest that has been upgraded to version 3.0.2.

After that, I will leverage the replica set's nature, which will replace the deleted pod with its template, thus updating the template version in the following settings. Ensure that the changes are successfully applied by running the following query, which will produce output as shown in the image. Deleting the pod. It appears that a new pod is being created to replace it.


3. **Prepare different manifest files for executing Recreate deployment strategy.**
A file can be created, as pushed to GitHub, with the name deployment2.yaml. The contents of the file are the same as the exported file in the tutorial, but there are differences in the strategy and selector sections.


    ```yaml
            selector:
                matchLabels:
                app: spring-petclinic-rest
            strategy:
                type: Recreate
    ```

The file can be imported into Kubernetes like any other manifest file. After that, to demonstrate the usefulness of this manifest file, we can change the image in the file to the version we want, for example, `a3.3.0`. This will delete pods in our old replica set and then deploy new pods in the new replica set.


4. **What do you think are the benefits of using Kubernetes manifest files?**

   The benefits of using Kubernetes manifest files lie in efficiency. We no longer need to remember the procedures and syntax required when updating or initially implementing. It's similar to importing a file into a document. We don't need to know how the document was created; the important thing is that we now have a ready-to-use document. Using manifest files also reduces the likelihood of human errors because with a manifest file, the services created are exactly as specified in the file, thus avoiding typos when typing out each syntax one by one.
