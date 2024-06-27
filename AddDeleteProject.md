<pre>
<b>Create and delete projects</b>


[mahsan@oc14 ex280-prep2024]$ oc new-project my-website
Now using project "my-website" on server "https://api.crc.testing:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.43 -- /agnhost serve-hostname

[mahsan@oc14 ex280-prep2024]$

[mahsan@oc14 ex280-prep2024]$ oc get projects
NAME                                               DISPLAY NAME   STATUS
default                                                           Active
hostpath-provisioner                                              Active
kube-node-lease                                                   Active
kube-public                                                       Active
kube-system                                                       Active
<b>my-website                                                        Active</b>
openshift                                                         Active
openshift-apiserver                                               Active

<b> create Apps </b>

[mahsan@oc14 ex280-prep2024]$ oc new-app --docker-image=bitnami/nginx --name=bnginx
Flag --docker-image has been deprecated, Deprecated flag use --image
--> Found container image b606d1d (8 days old) from Docker Hub for "bitnami/nginx"

    * An image stream tag will be created as "bnginx:latest" that will track this image

--> Creating resources ...
    imagestream.image.openshift.io "bnginx" created
    deployment.apps "bnginx" created
    service "bnginx" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/bnginx'
    Run 'oc status' to view your app.
[mahsan@oc14 ex280-prep2024]$


[mahsan@oc14 ex280-prep2024]$ oc get pods
NAME                     READY   STATUS    RESTARTS   AGE
bnginx-cbd8b8696-7xwcq   1/1     Running   0          78s
[mahsan@oc14 ex280-prep2024]$ oc get all
Warning: apps.openshift.io/v1 DeploymentConfig is deprecated in v4.14+, unavailable in v4.10000+
NAME                         READY   STATUS    RESTARTS   AGE
pod/bnginx-cbd8b8696-7xwcq   1/1     Running   0          83s

NAME             TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)             AGE
service/bnginx   ClusterIP   10.217.5.54   <none>        8080/TCP,8443/TCP   84s

NAME                     READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/bnginx   1/1     1            1           84s

NAME                                DESIRED   CURRENT   READY   AGE
replicaset.apps/bnginx-6884b8f655   0         0         0       84s
replicaset.apps/bnginx-cbd8b8696    1         1         1       83s

NAME                                    IMAGE REPOSITORY                                                            TAGS     UPDATED
imagestream.image.openshift.io/bnginx   default-route-openshift-image-registry.apps-crc.testing/my-website/bnginx   latest   About a minute ago
[mahsan@oc14 ex280-prep2024]$

<b> delete project </b>

[mahsan@oc14 ex280-prep2024]$ oc delete project my-website
project.project.openshift.io "my-website" deleted













</pre>

