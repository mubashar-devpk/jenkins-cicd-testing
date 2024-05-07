pipeline{
    agent any

    stages{

        stage("build"){

            steps {
                sh 'make'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                
            }
        }

        stage("Test"){

            steps {
                sh 'make check || true'
                junit '**/target/* .xml'
                
            }
        }
        stage("deploy"){
            when {
                epression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }

            steps {
                sh 'make publish'
                
            }
        }
    }
}