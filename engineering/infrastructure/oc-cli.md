# OC command line tools

You will need [oc-cli](https://docs.okd.io/latest/cli_reference/index.html) tools to login to and work with openshift clusters. 

### Table of contents

* [Install command line tools](#install-command-line-tools)
* [Login to Openshift cluster](#login-to-openshift-cluster)

## Install command line tools

If on macOS, then use `brew` to download and install:
```
brew install openshift-cli
```

Check the [documentation](https://docs.okd.io/latest/cli_reference/get_started_cli.html#installing-the-cli) for other operating systems.

## Login to Openshift cluster

**Note that this section requires you to have an account on the specific Openshift cluster you want to login to.**

Let's assume that openshift cluster is running on `https://openshift-test.mycompany.com`. To login to that cluster:

1. Try to login:

    ```
    $ oc login https://openshift-test.mycompany.com

    The server uses a certificate signed by an unknown authority.
    You can bypass the certificate check, but any data you send to the server could be intercepted by others.
    Use insecure connections? (y/n): y

    Login failed (401 Unauthorized)
    Verify you have provided correct credentials.
    You must obtain an API token by visiting https://openshift-test.mycompany.com/oauth/token/request
    ``` 

    Alright, so the login failed, because we need API token first. Additionally, we've had to accept self-signed certificate for the cluster domain, which is fine for test deployments.

2. Go to `https://openshift-test.mycompany.com/oauth/token/request` to obtain the token.
3. Now you should be able to login:

    ```
    $ oc login --token=<API_TOKEN> --server=https://openshift-test.mycompany.com

    Logged into "https://openshift-test.mycompany.com" as "myuser" using the token provided.

    You have access to the following projects and can switch between them with 'oc project <projectname>':
   
      * default
      openshift
      openshift-build
      ...

    Using project "default".
    Welcome! See 'oc help' to get started.
   ```
4. Use `oc project <project_name>` to switch to the desired project. Enjoy the cluster administration!

