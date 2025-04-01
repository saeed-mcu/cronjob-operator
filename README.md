# cronjob-operator

## Technical requirements
* go version 1.16+
* An `kubebuilder` binary installed locally
* Make sure your user is authorized with cluster-admin permissions.

## Step 1 : Setting up your project

initialize a boilerplate project structure with the following:

```bash
# we'll use a domain of tutorial.kubebuilder.io
# so all API groups will be <group>.tutorial.kubebuilder.io
kubebuilder init --domain tutorial.kubebuilder.io --repo github.com/saeed-mcu/cronjob-operator
```
