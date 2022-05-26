#!groovy

pipeline{
    agent{
        kubernetes{
            inheritFrom 'jenkins-slave'
            defaultContainer 'test'
        }
    }
    
    stages{
        stage('parameter check')
        {
            steps{
                echo "Current workspace : ${workspace}"
                sh 'mvn -version'
            }
        }
        
        stage('git check')
        {
            steps{
                checkout scm
            }
        }
        
        stage('build')
        {
            steps{
                sh 'pwd' 
                sh 'mvn clean package -Dmaven.test.skip=true'
                sh 'ls -al'
                dir('target'){
                   sh 'pwd'
                   sh 'ls -al'
                }
            }
            
        }   
        
        
        
    }
    
}
