# ArgoCD Application Deployment
This project follows Application of Applications ArgoCD pattern for deploying sample application `app1`.
ArgoCD Application `app1-deploy` deploys all ArgoCD resources from this repository including child Applications referring to separate Git or Helm repositories.

## Application onboarding
1. Create ArgoCD Project `app1`
Latest versions of ArgoCD allow declarative GitOps CD for ArgoCD itself and we are not limited only to submit Application resources.
We can manage multiple ArgoCD objects via GitOps, including ArgoCD configuration ConfigMaps, Projects or Repositores. Check [Operator manual](https://argo-cd.readthedocs.io/en/latest/operator-manual/declarative-setup/) for details and caveats.

2. Create ArgoCD Application following this repository's `main` branch.
In production, also this repository may contain DEV-STAGE-PROD branch management and `app1` can be deployed to non-prod ArgoCD instance.
`app1` Application Owner should however interact only with production ArgoCD cluster and consume it as a service.


## ArgoCD deployment
```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: app1-deploy
spec:
  destination:
    name: ''
    namespace: argocd
    server: 'https://kubernetes.default.svc'
  source:
    path: .
    repoURL: 'https://github.com/jkosik/app1-deploy.git'
    targetRevision: main
  project: default
```