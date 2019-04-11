# Respository to show Canary deployment strategy using k8s, istio, and helm

## The productpage app from istio docs is being used as the sample application to demonstrate this strategy

## Following [post](https://medium.com/microsoftazure/canary-release-strategy-using-kubernetes-istio-helm-fb49c0406f07) explains the strategy in more detail

## Strategy Stages

* STEADY STATE - 100 percent traffic to production deployment pods (which have current version of application)

* 10 % traffic to Canary deployment pods (Vnext of App) and 90% to production deployment (Current version of app)

* 90 % traffic to Canary deployment pods (Vnext of App) and 10% to production deployment (Current version of app)

* 100 % traffic to Canary deployment pods (Vnext of App) and 0% to production deployment (Current version of app)

* 100 % traffic to Canary deployment pods (Vnext of App) and do rolling updgrade of production deployment pods to move them to Vnext of App

* 100 percent traffic to production deployment pods (which now have Vnext of App) and 0% to canary deployment pods (Vnext of app)

* NEW STEADY STATE : 100 % to production deployment pods (Vnext of App) , 0% to canary deployment pods, and 0 replicas of canary deployment

## Repository structure:
* productpage folder contains
  * source code of the [python application](./productpage/productpage.py) (taken from istio docs)
  * [./productpage/Dockerfile](./productpage/Dockerfile) which is the dockerfile to dockerize the application
  * The [./productpage/chart/productpage](./productpage/chart/productpage) folder contains the helm chart which includes the kubernetes and istio resources
* [./helm-commands.sh](helm-commands.sh) : has the helm command for each stage, including rollback command and helm template command
* helm-template-output.yaml : contains the kubernetes resources generated using the sample helm command




