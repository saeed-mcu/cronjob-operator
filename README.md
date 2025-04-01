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

## Step 2 : Defining an API
```bash
kubebuilder create api --group batch --version v1 --kind CronJob
```
Press y for “Create Resource” and “Create Controller”.

`CronJob` is our root type, and describes the `CronJob` kind.
Like all Kubernetes objects, it contains `TypeMeta` (which describes API version and Kind), and also contains `ObjectMeta`,
which holds things like name, namespace, and labels.
`CronJobList` is simply a container for multiple CronJobs.
It’s the Kind used in bulk operations, like LIST.

In general, we never modify either of these – all modifications go in either Spec or Status.
We define types for the `desired state (Spec)` and `observed state(Status)` of our Kind.

That little `+kubebuilder:object:root` comment is called a marker.
This particular one tells the object generator that this type represents a Kind.
Then, the object generator generates an implementation of the runtime.Object interface for us,
which is the standard interface that all types representing Kinds must implement.

Finally, we add the Go types to the API group. This allows us to add the types in this API group to any Scheme.
```go
func init() {
    SchemeBuilder.Register(&CronJob{}, &CronJobList{})
}
```
