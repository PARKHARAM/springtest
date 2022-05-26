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
        
        /*************** Pulish Over SSH Plug in사용******************/
        stage('SSH transfer') {
            steps([$class: 'BapSshPromotionPublisherPlugin']) {
                sshPublisher(
                    continueOnError: false, failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "test_ssh",//Jenkins 시스템 정보에 사전 입력한 서버 ID
                            verbose: true,
                            transfers: [
                                sshTransfer(
                                    sourceFiles: "target/hello-0.0.1-SNAPSHOT.jar", //전송할 파일
                                    removePrefix: "target/", //파일에서 삭제할 경로가 있다면 작성
                                    remoteDirectory: "",//배포할 위치
                                    execCommand: "ls -al" //원격지에서 실행할 커맨드
                                )
                            ]
                        )
                    ]
                )
            }
        }
        
        
        
    }
    
}
