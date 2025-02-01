pipeline{

agent any

stages{
    stage('CodeCheckOut'){
        steps{
            git branch: 'main', credentialsId: '618d965c-04bb-4e9a-964f-f8eae6852d39', url: 'https://github.com/Eliyaz203/NodeJS-Devops-Project.git'
        }
    }
    stage('DockerBuild'){
        steps{
            sh "docker build -t mohammedeliyaz/node-js-app:${BUILD_NUMBER} ."
        }
    }
    stage('DockerPush'){
        steps{
            sh "docker push mohammedeliyaz/node-js-app:${BUILD_NUMBER}"
            sh "pwd"
        }
    }
    stage('K8s Deploy'){
        steps{
            sh "sed -i 's|mohammedeliyaz/node-js-app:.*|mohammedeliyaz/node-js-app:${BUILD_NUMBER}|' deployment.yaml"
            sh "kubectl apply -f deployment.yaml"
            sh "kubectl apply -f service.yaml"
        }
    }
        
    

}//End-stages

}//End-pipeline
