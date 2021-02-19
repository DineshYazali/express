This is an angular application which is being deployed to AWS EKS

Create an EKS cluster either from console or from command line using eksctl.
Install aws cli, kubectl on your machine build server.
Refer: https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html.
Refer: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html.
Configure aws cli, kubectl paths,dockerhub pwd in jenkins environment variable.
Add aws access key and secret access key as secret texts in jenkins.
Refer to the jenkinsfile for build commands.
In case of deployment using Helm , Install Helm on your build server.
Refer: https://docs.aws.amazon.com/eks/latest/userguide/helm.html
A helm chart called demochart is present in the repo .
Using this chart deployment is done on eks.
Required HELM commands:


   1.To create a helm chart use: helm create name-of-chart



   2.Edit the values.yaml,deployment.yaml,service.yaml as per the requirements.



   3.To test the chart: helm lint demochart



   4.To install/deploy a chart:  helm install release-name chart-name
