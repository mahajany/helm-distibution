# Distribute Helm Chart

1. Create a repository
`$helm create my-app-helm-distribution`
Output `Creating my-app-helm-distribution`

2. Pacakge it (after testint it..) `$ helm package my-app-helm-distribution/`
Ouptut `Successfully packaged chart and saved it to: my-app-helm-distribution-0.1.0.tgz`

3. Create  a direcotry which you can push to git. First step is to move this `.tgz` file to that directory and create `index.yaml;`.
``` 
$mkdir helm-distibution
$mv my-app-helm-distribution-0.1.0.tgz helm-distibution
$helm repo index helm-distibution --url https://github.com/mahajany/helm-distibution.git
```
Now an index.yaml should be created int eh folder helm-distibution

4. Finally, publish it to git!
```
cd helm-distibution/
git init
git remote add origin https://github.com/mahajany/helm-distibution.git
git add .
git config user.name "Yogesh"
git config user.email "mahajany@gmail.com"
git commit -m "Create Helm Package, take-1"
git push origin master
```

Go to https://github.com/mahajany/helm-distibution.git
