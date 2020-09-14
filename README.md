# jenkins-k8s

This project shows an example on how to configure Jenkins to run in Kubernetes using the [Jenkins Operator for Kubernetes](https://github.com/jenkinsci/kubernetes-operator).

## Prerequisites

* access to a Kubernetes cluster version `1.11+`
* kubectl version `1.11+`

## Installation

1. Install Jenkins Custom Resource Definition:
    ```bash
    kubectl apply -f https://raw.githubusercontent.com/jenkinsci/kubernetes-operator/master/deploy/crds/jenkins_v1alpha2_jenkins_crd.yaml
    ```

2. Apply Service Account and RBAC roles:
    ```bash
    kubectl apply -f https://raw.githubusercontent.com/jenkinsci/kubernetes-operator/master/deploy/all-in-one-v1alpha2.yaml
    ```

3. Watch Jenkins Operator instance being created:
    ```bash
    kubectl get pods -w
    ```

**NOTE:** Please see [Kubernetes Operator Installation](https://jenkinsci.github.io/kubernetes-operator/docs/installation/) for more information.

## Deploy Jenkins

1. Deploy a Jenkins to Kubernetes:
    ```bash
    kubectl create -f jenkins_instance.yaml
    ```

2. Watch the Jenkins instance being created:
    ```bash
    kubectl get pods -w
    ```

3. Get the Jenkins credentials:
   ### Unix
    ```bash
    kubectl get secret jenkins-operator-credentials-example -o 'jsonpath={.data.user}' | base64 -d
    kubectl get secret jenkins-operator-credentials-example -o 'jsonpath={.data.password}' | base64 -d
    ```
    ### Windows
    ```bash
    kubectl get secret jenkins-operator-credentials-example -o 'jsonpath={.data.user}' | certutil -decode
    kubectl get secret jenkins-operator-credentials-example -o 'jsonpath={.data.password}' | certutil -decode
    ```

4. Connect to the Jenkins instance (actual Kubernetes cluster):
    ```bash
    kubectl port-forward jenkins-example 8080:8080
    ```

5. Then open browser with address http://localhost:8080.

NOTE: Please see the [Kuberntes Operator Deploy Jenkins](https://jenkinsci.github.io/kubernetes-operator/docs/getting-started/latest/deploy-jenkins/) for more information.
