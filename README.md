# Bootstrap with ArgoCD Autopilot
This scenario shows the steps to install ArgoCD with ArgoCD Autopilot

Check if kubernetes is up and running(It can take some time):
```kubectl cluster-info```

Run below commands to setup argocd autopilot:

```VERSION=$(curl --silent "https://api.github.com/repos/argoproj-labs/argocd-autopilot/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/')```

```curl -L --output - https://github.com/argoproj-labs/argocd-autopilot/releases/download/$VERSION/argocd-autopilot-linux-amd64.tar.gz | tar zx```

```mv ./argocd-autopilot-* /usr/local/bin/argocd-autopilot```

```argocd-autopilot version```

Copy and edit XXX with your PAT then execute:

```PAT=XXX```

Copy and edit XXX with your Github Account Name then execute:

```GITHUB_ACCOUNT=XXX```

Copy and edit XXX with Github Repository Name then execute:

```REPOSITORY=XXX```

Run command:

```export GIT_TOKEN=$PAT```

Run command:

```git config --global user.email "test"```

Run command:

```git config --global user.name "test"```

Run Command:

```export GIT_REPO=https://github.com/$GITHUB_ACCOUNT/$REPOSITORY```

Run command to create repository and bootstrap ArgoCD:

```argocd-autopilot repo bootstrap```

Check if ArgoCD setup completed:

```kubectl get pods -n argocd -w```

Check if applications synchronized:

```kubectl get application -n argocd -owide -w```


You can also check your Github Repository.

Don't forget to delete PAT you have created to prevent exploits.
