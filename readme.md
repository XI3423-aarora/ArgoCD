# ArgoCD

## What is ArgoCD ?
Argo CD is a Kubernetes-native continuous deployment (CD) tool. Unlike external CD tools that only enable push-based deployments, Argo CD can pull updated code from Git repositories and deploy it directly to Kubernetes resources. It enables developers to manage both infrastructure configuration and application updates in one system.

## challanges faced with CD workflow without ArgoCD
1. Install and setup tools, like kubectl
2. configure access to k8s
3. Configure access to cloud platform
4. No visibility of deployment status.

## CD workflow with ArgoCD
1. Deploy ArgoCD in k8s cluster
2. Configure ArgoCD to track Git repo
3. ArgoCD monitor for any changes and applies auomatically 

## Argo CD offers the following key features and capabilities:
1. Manual or automatic deployment of applications to a Kubernetes cluster.
2. Automatic synchronization of application state to the current version of declarative configuration.
3. Web user interface and command-line interface (CLI).
4. Ability to visualize deployment issues, detect and remediate configuration drift.
5. Role-based access control (RBAC) enabling multi-cluster management.
6. Single sign-on (SSO) with providers such as GitLab, GitHub, Microsoft, OAuth2, OIDC, LinkedIn, LDAP, and SAML 2.0
7. Support for webhooks triggering actions in GitLab, GitHub, and BitBucket.

## Installation
|Install ArgoCD Directly|
|-------------------|
|kubectl create namespace argocd
 kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml|

|Using Helm Chart|
|------------------|
|helm repo add argo https://argoproj.github.io/argo-helm
 kubectl create namespace argocd
 helm -n argocd install argo argo/argo-cd|

For More Information Visit : https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd

## CICD pipeline using any CI tool and ArgoCD
1. Prepare a microservice.
2. Run a CI pipeline using any CI tools like Jenkins and GitLabcli etc. 
3. Configure ArgoCD to track Git repo.
4. ArgoCD monitor for any changes and applies auomatically.

![](https://images.prismic.io/gspann/c547b13c-da8b-40c4-8cc4-2dc3dbfb69cb_Img+1+CI+CD+Flow+with+Argo+CD.jpg?auto=compress,format)

![](https://containerjournal.com/wp-content/uploads/2021/10/Screen-Shot-2021-10-07-at-7.25.38-PM.png)

### Configure ArgoCD to track Git repo
1. Go to ArgoCD UI(using port-forword command).
2. Click on new app and update form according to the field.

#### Alternative method
##### use Yaml file
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: guest
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/Kube.git  # Can point to either a Helm chart repo or a git repo.
    targetRevision: HEAD  # For Helm, this refers to the chart version.
    path: charts/kube-bench-adapter
  
  destination:
    server : https://kubernetes.default.svc
    namespace: my-appss

  syncPolicy:
    syncOptions:
    - CreateNamespace=true

    automated:
      selfHeal: true
      prune: true






## References
1. https://blog.risingstack.com/argo-cd-kubernetes-tutorial/
2. https://www.arthurkoziel.com/setting-up-argocd-with-helm/
3. https://codefresh.io/learn/argo-cd/
4. https://argo-cd.readthedocs.io/en/stable/getting_started/
5. https://github.com/argoproj/argo-cd
6. https://www.youtube.com/watch?v=MeU5_k9ssrs

