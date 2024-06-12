<pre>
<h1> Configuring MySQL </h1>

The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: GuJ9g-z7nWc-WQWy6-R2jxY

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443
<h2>[mahsan@oc14 ~]$ eval $(crc oc-env)
[mahsan@oc14 ~]$ oc login -u developer https://api.crc.testing:6443 </h2>
Logged into "https://api.crc.testing:6443" as "developer" using existing credentials.

You don't have any projects. You can try to create a new project, by running

    oc new-project <projectname>

<h2> [mahsan@oc14 ~]$ oc new-project microservice </h2>
Now using project "microservice" on server "https://api.crc.testing:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.43 -- /agnhost serve-hostname

<h2> [mahsan@oc14 ~]$ oc get projects </h2>
NAME           DISPLAY NAME   STATUS
microservice                  Active
<h2> [mahsan@oc14 ~]$ oc create secret generic mysql --from-literal=password=mypassword </h2>
secret/mysql created
<h2> [mahsan@oc14 ~]$ oc get secret </h2>
NAME                       TYPE                                  DATA   AGE
builder-dockercfg-f924w    kubernetes.io/dockercfg               1      91s
builder-token-8c97d        kubernetes.io/service-account-token   4      91s
default-dockercfg-92kb6    kubernetes.io/dockercfg               1      91s
default-token-f9cms        kubernetes.io/service-account-token   4      91s
deployer-dockercfg-cvnzh   kubernetes.io/dockercfg               1      91s
deployer-token-x6vxq       kubernetes.io/service-account-token   4      91s
mysql                      Opaque                                1      15s
[mahsan@oc14 ~]$ oc whoami
developer
<h2> [mahsan@oc14 ~]$ oc new-app --name mysql --docker-image mysql </h2>
Flag --docker-image has been deprecated, Deprecated flag use --image
--> Found container image fcd86ff (6 weeks old) from Docker Hub for "mysql"

    * An image stream tag will be created as "mysql:latest" that will track this image

--> Creating resources ...
    imagestream.image.openshift.io "mysql" created
    deployment.apps "mysql" created
    service "mysql" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/mysql'
    Run 'oc status' to view your app.
<h2> [mahsan@oc14 ~]$ oc get pods </h2> 


NAME                     READY   STATUS             RESTARTS      AGE
mysql-6df5845f9c-j4v2f   0/1     CrashLoopBackOff   1 (43s ago)   72s
[mahsan@oc14 ~]$
[mahsan@oc14 ~]$
[mahsan@oc14 ~]$
<h2> [mahsan@oc14 ~]$ oc logs mysql-6df5845f9c-j4v2f </h2>
 2024-06-12 23:04:11+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.0-1.el9 started.
2024-06-12 23:04:12+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
    You need to specify one of the following as an environment variable:
    - MYSQL_ROOT_PASSWORD
    - MYSQL_ALLOW_EMPTY_PASSWORD
    - MYSQL_RANDOM_ROOT_PASSWORD
[mahsan@oc14 ~]$

[mahsan@oc14 ~]$
<h2> [mahsan@oc14 ~]$ oc set env deployment mysql --prefix MYSQL_ROOT_ --from secret/mysql </h2>
deployment.apps/mysql updated
[mahsan@oc14 ~]$ oc get pods
NAME                     READY   STATUS    RESTARTS   AGE
mysql-5b7f466448-ng79d   1/1     Running   0          6s
[mahsan@oc14 ~]$


<h2> [mahsan@oc14 ~]$ oc set volumes deployment/mysql --name mysql-pvc --add --type pvc --claim-size 1Gi --claim-mode rwo --mount-path /mnt </h2>
deployment.apps/mysql volume updated
[mahsan@oc14 ~]$


The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: GuJ9g-z7nWc-WQWy6-R2jxY

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  $ eval $(crc oc-env)
  $ oc login -u developer https://api.crc.testing:6443
[mahsan@oc14 ~]$

<h2> [mahsan@oc14 ~]$ oc login -u kubeadmin -p GuJ9g-z7nWc-WQWy6-R2jxY </h2>
Login successful.

You have access to 68 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "microservice".
[mahsan@oc14 ~]$

[<h2> mahsan@oc14 ~]$ oc get node </h2> 
NAME   STATUS   ROLES                         AGE   VERSION
crc    Ready    control-plane,master,worker   17d   v1.28.9+416ecaf
[mahsan@oc14 ~]$

<h2> [mahsan@oc14 ~]$ oc label nodes crc role=master </h2> 
node/crc labeled
[mahsan@oc14 ~]$

<h2> [mahsan@oc14 ~]$ oc describe node crc </h2>
Name:               crc
Roles:              control-plane,master,worker
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=crc
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node-role.kubernetes.io/master=
                    node-role.kubernetes.io/worker=
                    node.openshift.io/os_id=rhcos
                   <b> role=master </b>
                    topology.hostpath.csi/node=crc
Annotations:        csi.volume.kubernetes.io/nodeid: {"kubevirt.io.hostpath-provisioner":"crc"}
                    k8s.ovn.org/host-cidrs: ["192.168.126.11/24","192.168.130.11/24"]
                    k8s.ovn.org/l3-gateway-config:
					
<h2> [mahsan@oc14 ~]$ oc login -u developer https://api.crc.testing:6443 </h2> 
Logged into "https://api.crc.testing:6443" as "developer" using existing credentials.

You have one project on this server: "microservice"

Using project "microservice".
[mahsan@oc14 ~]$

<h2>[mahsan@oc14 ~]$ oc get deployment </h2>
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
mysql   1/1     1            1           28m
<h2> [ hsan@oc14 ~]$ oc edit deployment mysql </h2>


- containerPort: 3306
          protocol: TCP
        - containerPort: 33060
          protocol: TCP
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /var/lib/mysql
          name: mysql-volume-1
        - mountPath: /mnt
          name: mysql-pvc
      dnsPolicy: ClusterFirst
     <h2> nodeSelector:
        role: master </h2>
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - emptyDir: {}
        name: mysql-volume-1
      - name: mysql-pvc
        persistentVolumeClaim:
          claimName: pvc-nj67c
status:
  availableReplicas: 1
  conditions:
  - lastTransitionTime: "2024-06-12T23:11:05Z"
-- INSERT --

<h2> [mahsan@oc14 ~]$ oc get pods </h2>
NAME                    READY   STATUS    RESTARTS   AGE
mysql-b466c8678-mghzr   1/1     Running   0          11s
[mahsan@oc14 ~]$


</pre>
