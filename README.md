# Tekton CLI Wrapper
An opinionated wrapper to deploy OCP clusters by using OpenShift Pipelines throught [tkn cli](https://github.com/tektoncd/cli).

---
### How to use it
The steps are simple:
1. First make sure that you are **authenticated** throught command line (by using `oc login` or getting the proper `kubeconfig` file) to the *bootstrap cluster*<sup>1</sup> to have access to the pipelines
2. Set the needed **variables** by exporting them or by placing them in front of the make command. Then, **run** your desired target.
For instance:
```
export OCP_VER=4.8
export NAME="my-ocp-cluster"
make deploy-ocp-regular-aws
```
...or...
```
OCP_VER=4.8 NAME="my-ocp-cluster" make deploy-ocp-regular-aws
```

<span style="font-size: .7rem"><sup>1</sup>(The *bootstrap cluster* is a OpenShift/Kubernetes cluster with the [plumbing-gitops](https://gitlab.cee.redhat.com/gitops/plumbing-gitops) manifests for pipelines already applied).</span>

---
### Targets
This table shows the different targets within the Makefile that you can call:
| **Target**                     | **Description**                                                          | **Requires** |
|--------------------------------|--------------------------------------------------------------------------|--------------|
| `make help`                    | Prints help.                                                             | OCP_VER      |
| `make deploy-ocp-regular-psi`  | Deploys a regular cluster in PSI (OpenStack infrastructure).             | OCP_VER      |
| `make deploy-ocp-regular-aws`  | Deploys a regular cluster in AWS (EC2 infrastructure).                   | OCP_VER      |
| `make deploy-ocp-proxy`        | Deploys a proxy cluster in AWS (EC2 infrastructure).                     | OCP_VER      |
| `make deploy-ocp-disconnected` | Deploys a disconnected (air-gapped) cluster in AWS (EC2 infrastructure). | OCP_VER      |
| `make destroy-cluster`         | Destroys an existent cluster.                                            | NAME         |

### Variables:
Below you will find the variables reference
| **Variable**      | **Description**                                                                                                                          |
|-------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| OCP_VER           | OpenShift Version. It accepts major and minor in format *X.Y* (i.e. `4.9`).                                                              |
| NAME              | Name for the OpenShift cluster. If not needed for the target, it will be auto-generated.                                                 |
| BOOTSTRAP_CLUSTER | Specifies the OCP cluster name where the plumbing-gitops tekton pipelines are installed. <br/> Default: *api-ocp-c1-prod-psi-redhat-com* |