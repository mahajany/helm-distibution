# Distribute Helm Chart

1. Create a repository
`helm create my-app-helm-distribution`
Output `Creating my-app-helm-distribution`

2. Pacakge it (after testing it..) `helm package my-app-helm-distribution/`
Ouptut `Successfully packaged chart and saved it to: my-app-helm-distribution-0.1.0.tgz`

3. Create  a direcotry which you can push to git. First step is to move this `.tgz` file to that directory and create `index.yaml;`.
``` 
mkdir helm-distibution
mv my-app-helm-distribution-0.1.0.tgz helm-distibution
 helm repo index helm-distibution --url  http://localhost:8000/helm-distibution
```
Now an index.yaml should be created int eh folder helm-distibution


Go to https://github.com/mahajany/helm-distibution.git

5.  Publish it. All it needs an htttp server where index.yaml can be distributed, we can use run it on localhost
```

python -m http.server
```
Check that index.yaml and your package is available as well:
`curl http://localhost:8000/helm-distibution/index.yaml`
`wget  http://localhost:8000/helm-distibution/my-app-helm-distribution-0.1.0.tgz`



6. Use it - add repo and install this wonderful app on your k8 distribution!
```
helm repo add helm-distribution-1 http://localhost:8000/helm-distibution
helm repo list
helm repo update
helm search repo  helm-distribution-1
helm install myapp1 helm-distribution-1/my-app-helm-distribution
```

See that your application is there:
`kubectl get all`

