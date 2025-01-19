pipeline{

agent any

stages{
    stage('CodeCheckOut'){
        steps{
            checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Eliyaz203/NodeJS-Devops-Project.git']])
        }
    }
    stage('DockerBuild'){
        steps{
            sh "docker build -t mohammedeliyaz/nodejs-app:${BUILD_NUMBER} ."
        }
    }
    stage('DockerPush'){
        steps{
            sh "docker push mohammedeliyaz/nodejs-app:${BUILD_NUMBER}"
        }
    }
    stage('K8s Deploy'){
        steps{
            sh "sed -i 's|mohammedeliyaz/nodejs-app:.*|mohammedeliyaz/nodejs-app:${BUILD_NUMBER}|' deployment.yaml"
            sh "kubectl apply -f deployment.yaml"
            sh "kubectl apply -f services.yaml"
        }
    }
        
    

}//End-stages

}//End-pipeline
