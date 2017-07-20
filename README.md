App Dev Cloud with JBoss Rewards Demo
=====================================
This demo is to install JBoss BPM Suite Rewards Demo in the Cloud based on leveraging the OpenShift Container Platform (OCP)
It delivers a fully functioning JBoss BPM Employee Rewards example containerized on OCP.

This is the HR employee rewards demo that provides examples of human task integration, form designer
and a custom email work item handler.


Install JBoss Rewards on OpenShift
----------------------------------
1. First ensure you have an OpenShift container based installation, such as one of the followling installed first:

  - [OCP Install Demo](https://github.com/redhatdemocentral/ocp-install-demo)

  - or your own OpenShift installation.

2. [Download and unzip this demo.](https://github.com/redhatdemocentral/rhcs-rewards-demo/archive/master.zip)

3. Download JBoss EAP & JBoss BPM Suite, add to installs directory (see installs/README).

4. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges:
```
   # The installation needs to be pointed to a running version
   # of OpenShift, so pass an IP address such as:
   #
   $ ./init.sh 192.168.99.100  # example for OCP.
```

Log in to JBoss Rewards to start exploring an online employee rewards application (the address will be generated by the init script):

  - OCP example:
    [http://rhcs-rewards-demo.192.168.99.100.xip.io/business-central](http://rhcs-rewards-demo.192.168.99.100.xip.io/business-central) ( u:erics / p:bpmsuite1! )

5. Want to build the Rewards demo from scratch? Try this hands-on <a href="https://bpmworkshop.github.io/lab11.html" target="_blank">online workshop</a>.


Note before running demo:
-------------------------
This project can be installed on any OpenShift platform, such as OpenShift Container Platform.
It's possible to install it on any available installation by pointing this installer to an OpenShift IP address:
```
  $ ./init.sh IP
```

If for any reason the installation breaks or you want a new installation, just remove the project entry in the OpenShift console and re-run the installation.

Should your local network DNS not handle the resolution of the above address, giving you page not found errors, you can apply the
following to your local hosts file:

```
$ sudo vi /etc/hosts

# add host for OCP demo resulution
192.168.99.100   rhcs-rewards-demo.192.168.99.100.xip.io 
```

This project is pre-loaded into the JBoss BPM Suite, after starting it you can login,
examine the rule, process, and data model from within the various product components.

After claiming the user task as a manager (to approve or deny the award), if task completion takes longer
than 1 minutes it will te reassigned back into the group so other managers can claim it. The short time frame
of 1 minutes is for demo purposes, should talk about days to complete instead as if a manager that claimed a
task got sick and failed to complete the claimed task.

Optional: A task notification has also been setup to alert the members of the group responsible if a task sits 
longer than 2 minutes without being started (claimed). 

To clone a repository in the running container, the following actions would need to occur from a developer's machine.

1. Execute port forwarding through the OpenShift CLI. This will open a tunnel between the developer's machine and the pod through
	 the OpenShift API pod proxy. The command window will block while the session is open:

   ```
   # Read-only access to repo on port 9418.
   #
   $ oc port-forward $(oc get pod -l=deploymentconfig=rhcs-rewards-demo --template='{{ range .items }} {{ .metadata.name }} {{ end }}') 9418:9418

   # Read-write access to repo on port 8001.
   #
   $ oc port-forward $(oc get pod -l=deploymentconfig=rhcs-rewards-demo --template='{{ range .items }} {{ .metadata.name }} {{ end }}') 8001:8001
   ```

2. Clone the repository. In another window, clone the remote repository after logging in to Business Central, creating a repository
	 and identifying the repository URL in the Admin Perspective (this example is a BackOffice repository):

   ```
   # Read-only access to repo on port 9418.
   #
   $ git clone git://localhost:9418/rewards

   # Read-write access to repo on port 8001.
   #
   $ git clone git://localhost:8001/rewards
   ```


Supporting Articles
-------------------
- [How to Optimize Existing IT by Modernizing HR Processes](http://www.schabell.org/2017/07/how-to-optimize-existing-it-modernizing-hr-processes.html)

- [App Dev in the Cloud - HR Employee Rewards Application on OpenShift](http://www.schabell.org/2017/01/appdev-in-cloud-hr-employee-rewards-app-openshift.html)

- [How to put the JBoss HR Employee Rewards project into the Cloud](http://www.schabell.org/2016/05/howto-put-jboss-hr-employee-rewards-into-cloud.html)

- [Build rewards demo project with online workshop.](http://bpmworkshop-onthe.rhcloud.com)


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.6 - JBoss BPM Suite 6.4.0 and JBoss EAP 7.0.0 with rewards demo installed on any given OpenShift installation and loading mulitple projects.

- v1.5 - JBoss BPM Suite 6.4.0 and JBoss EAP 7.0.0 with rewards demo installed on any given OpenShift installation and port forwarding for git repo access configured.

- v1.4 - JBoss BPM Suite 6.4.0 and JBoss EAP 7.0.0 with rewards demo installed on any given OpenShift installation.

- v1.3 - JBoss BPM Suite 6.3.0.GA and JBoss EAP 6.4.7 with rewards demo installed on Red Hat CDK.

- v1.2 - JBoss BPM Suite 6.2.0.GA-redhat-1-bz-1334704 on JBoss EAP 6.4.4 with rewards demo installed on Red Hat CDK.

- v1.1 - JBoss BPM Suite 6.2.0.GA-redhat-1-bz-1334704 on JBoss EAP 6.4.4 with rewards demo installed on Red Hat CDK using OpenShift Enterprise image.

- v1.0 - JBoss BPM Suite 6.2.0-BZ-1299002 on JBoss EAP 6.4.4 with rewards demo installed on Red Hat CDK using OpenShift Enterprise image.

![Cloud Pod](https://raw.githubusercontent.com/redhatdemocentral/rhcs-rewards-demo/master/docs/demo-images/rhcs-rewards-pod.png)

![Cloud Build](https://raw.githubusercontent.com/redhatdemocentral/rhcs-rewards-demo/master/docs/demo-images/rhcs-rewards-build.png)

![Process](https://raw.githubusercontent.com/redhatdemocentral/rhcs-rewards-demo/master/docs/demo-images/rewards-process.png)

![Process & Task Dashboard](https://raw.githubusercontent.com/redhatdemocentral/rhcs-rewards-demo/master/docs/demo-images/mock-bpm-data.png)

[![Video Rewards Run](https://raw.githubusercontent.com/eschabell/erics-images/master/brms_bpms_workshop/image309.png)](http://vimeo.com/ericschabell/bpms-hr-employee-rewards-demo-run)

![Cloud Suite](https://raw.githubusercontent.com/redhatdemocentral/rhcs-rewards-demo/master/docs/demo-images/rhcs-arch.png)

