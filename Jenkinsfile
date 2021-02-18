def image
pipeline
{
    agent any
    
    environment
    {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-key-id')
       
    } 

    stages 
    {
        stage('Checkout')
        {
         steps
         {
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/DineshYazali/express.git']]]) 
         }
         
        }
        
       stage('Build')
        {
            steps
             {
                sh 'npm install'
            }
        } 
        
        stage('Build image and publish')
        {
            steps
            {
                script {
                withDockerRegistry(credentialsId: 'dockerhub', url: 'https://index.docker.io/v1/')
                {
                  image = docker.build("omega206/node-repo")
                  image.push()    
                }
                }
            }
            
        } 
         stage('Deploy')
         {
            steps
            {
                script {
                        export AWS_REGION=us-east-2
                        /usr/bin/docker login -u omega206 -p $DOCKER
                        $PATH/aws eks update-kubeconfig  --region us-east-2  --name jenkins-eks-cluster
                        $PATH/kubectl create -f lerni-svc.yaml
                        $PATH/kubectl get all
  
                }
            }
        } 
        
       
          
    }
}
