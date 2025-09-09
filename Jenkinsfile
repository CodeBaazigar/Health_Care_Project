pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'Master', credentialsId: 'Github_Credentials', url: 'https://github.com/CodeBaazigar/Health_Care_Project.git'
            }
        }
     stage('Build Stage') {
            steps {
                sh 'mvn clean package'
            }
        }
    stage('Docker Build Image') {
            steps {
                sh 'docker build -t codebaazigar/healthcare:5.0 .'
            }
        }
    stage('Pushing to Dockerhub') {
            steps {
                withDockerRegistry(credentialsId: 'Dockerhub_Credentials') {
                    sh 'docker push codebaazigar/healthcare:5.0'
                }
            }
        }
     stage('Deploying to K8s Cluster') {
            steps {
                kubernetesDeploy (configs: 'Kubernetesfile.yml', kubeconfigId: 'Kubernetes_Config')
            }
        }
    }
}

