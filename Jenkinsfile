pipeline{
    agent any
    environment{
        DOCKER_IMAGE = "tummetikrishna/spring-petclinic"
    }
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/krishnatummeti/springboot-docker-kubernetes-cicd.git']])
                sh 'mvn clean install'
                echo  "Build Maven install Completed"
            }
        }
        stage('Build a Docker Image'){
            steps{
                script{
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                    echo "docker image build completed ${DOCKER_IMAGE}"
                }
            }
        }
        stage('Push to docker hub'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                sh 'docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}' 
}
                sh 'docker push ${DOCKER_IMAGE}'
            }
        }
        stage('Deploy to Kubernetes'){
            steps{
                script{
                    withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s-config', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://192.168.71.129:6443') {
                    sh 'kubectl apply -f deploymentservice.yaml'
                    sh 'kubectl get all'
}
                    
                }

            }
        }
    }

}
