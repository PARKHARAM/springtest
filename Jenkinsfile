#!groovy

pipeline{
    agent{
        kubernetes{
            inheritFrom 'jenkins-slave'
            //defaultContainer 'test'
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
    }
    
}
