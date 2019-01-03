# Local OpenShift setup

We deploy the applications to OpenShift cluster. OpenShift comes in two versions: [open source](https://www.okd.io/) and [enterprise](https://www.openshift.com/). We use the open source version and it's relatively complex to setup properly. To make this process easier, we use the [Minishift](https://github.com/minishift/minishift) tool. Minishift will take care of setting up the VM with CentOS and deploying OpenShift cluster, as well as `oc` command line tool.

### Table of contents

* [Setup OpenShift cluster](#setup-openshift-cluster)
    * [Example app](#example-app)
    * [Shut down the cluster](#shut-down-the-cluster)

## Setup OpenShift cluster

Following are the steps to set up your local OpenShift cluster:

* Setup the virtualization environment. This is OS dependent, so check the [Minishift docs](https://docs.okd.io/latest/minishift/getting-started/setting-up-virtualization-environment.html) what needs to be done for a particular OS. For macOS:

```
$ brew install docker-machine-driver-xhyve
$ sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
$ sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve    
```
* Install Minishift. This is also OS dependent, see the [relevant documentation](https://docs.okd.io/latest/minishift/getting-started/installing.html). For macOS:

```
$ brew cask install minishift
```
* Start minishift. The process may take awhile the first time as it needs to download CentOS, OpenShift, ... So, grab a coffee.

```
$ minishift start
```

* As part of installation process, the `oc` command line tool is also installed. Add it to your `$PATH` environment variable. To check the path, use `minishift oc-env` command:

```
$ minishift oc-env
export PATH="/Users/jang/.minishift/cache/oc/v3.11.0/darwin:$PATH"
# Run this command to configure your shell:
# eval $(minishift oc-env)
```

* Run `oc status` to verify that the cluster is running.

**Congratulations!** You have now a running OpenShift cluster on your laptop.

#### Example app
Let's deploy rabbitMQ as an example of using OpenShift cluster:

* Tell the cluster to download and run rabbitMQ docker image (with rabbit's admin console):

```
$ oc new-app rabbitmq:management-alpine
```

* Check the logs:

```
$ oc logs -f svc/rabbitmq
```

* Expose the admin console to be accessible from outside of cluster:
```
$ oc expose service rabbitmq --name=rabbitmq-admin --port 15672
```

* Use `oc status` to verify that the new route is available. See example output:

```
$ oc status
In project My Project (myproject) on server https://192.168.64.2:8443

http://rabbitmq-admin-myproject.192.168.64.2.nip.io to pod port 15672
  dc/rabbitmq deploys istag/rabbitmq:management-alpine
    deployment #1 deployed 37 minutes ago - 1 pod
```

* Use a browser to open rabbitMQ console using the http address from `oc status` command. If everything worked correctly, then you should see the login form and you can use `guest/quest` to login and inspect your rabbitMQ instance.

#### Shut down the cluster
Let's delete the rabbitMQ example application and then stop the cluster:

```
$ oc delete svc rabbitmq
$ oc delete dc rabbitmq
$ minishift stop
```