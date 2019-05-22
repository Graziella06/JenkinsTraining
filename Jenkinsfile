pipeline{
    agent none
    environment {
        EXAMPLE = 20190521
    }
    //options {
    //    skipStageAfterUnstable() // prevent other stages to be executed in case 
        // unstable stage
    
    //}
    stages {
        stage('build mvn'){
            agent {
                docker{
                    //image 'maven:3.3.3'
                    image 'maven'
                }
            }
            steps{
                echo 'Hello world'
                sh 'mvn --version'
            }
            post {
            always{
                echo "TRALALA LA"
            }
        }
        }
        
        stage('build python'){
            agent {
                docker{
                    image 'python'
                }
            }
            steps{
                retry(3){
                    sh 'python --version'
                }
                timeout(time:3,unit:'MINUTES'){
                   sh 'echo "Hello world"; return 1;'
                   sh 'python --version'
                }
            }
        }
        stage('buid dev'){
            agent {
                docker{
                    image 'python'
                }
            }
            steps{
                retry(3){
                    sh 'python --version'
                }
                timeout(time:3,unit:'MINUTES'){
                   echo 'Hello world'
                   sh 'python --version'
                }
            }
        }
        
    }
    post {
        always{
            echo "$EXAMPLE"
            //junit 'build/reports/**/*.xml' //work only if Jenkins executes Junit scripts
            //To Try : xunit which may work with python
            //archiveArtifacts artifacts: "dossier",fingerprint: true //fingerprint 
            //hipchatSend message:"Message @here ${env.JOB_NAME"
            //deleteDir() //
            //
        }
        success {
            echo '1 stage SUCCESSED'
        }
        failure {
            echo '1 stage FAILS'
        }
        changed {
            echo 'Status CHANGED'
        }
    }    
}
