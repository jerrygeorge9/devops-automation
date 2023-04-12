pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jerrygeorge9/devops-automation']]])
                //sh 'mvn clean install'
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    //sh 'docker build -t jerrygeorge9/devops-integration .'
                    bat 'docker build -t jerrygeorge9/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   //sh 'docker login -u javatechie -p ${dockerhubpwd}'
                   bat 'docker login -u jerrygeorge9 -p Jinjer*99'
            		}
                   //sh 'docker push jerrygeorge9/devops-integration'
                   bat 'docker push jerrygeorge9/devops-integration'
                }
            }
        }


    }
}