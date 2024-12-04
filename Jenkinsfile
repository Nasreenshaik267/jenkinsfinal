
pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'jdk17'
    }
    

    stages {
        stage('Git Checkout') {
            steps {
                 git branch: 'main' , url: 'https://github.com/Nasreenshaik267/jenkinsfinal.git'
            }
        }
        stage('Versioning') {
            steps {
                script {
                sh 'mvn versions:set -DnewVersion=1.0.${BUILD_NUMBER}'
                }
            }
        }
        stage('Maven Compile') {
            steps {
               echo 'Maven Compile Started'
               sh 'mvn compile'
            }
        } 
        stage('Maven Test') {
            steps {
               echo 'Maven Test Started'
               sh 'mvn test'
            } 
        } 
        stage('File System Scan by Trivy') {
            steps {
               echo 'Trivy Scan Started'
               sh 'trivy fs --format table --output trivy-fs-output.txt .'
            }
        } 
        stage('Build Docker Image and TAG') {
            steps {
                script {
                    // Build the Docker image using the renamed JAR file
                    script {
                            sh 'docker build -t nginx:latest .'
                   }
                }   
            }
        }
        
    }
}
