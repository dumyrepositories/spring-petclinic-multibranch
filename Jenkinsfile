pipeline {
    agent any
    triggers { pollSCM('* 21 * * 1-5')}
    stages {
        stage('VCS'){
            steps {
                git url: 'https://github.com/dumyrepositories/spring-petclinic-multibranch.git',
                    branch: 'dev'
            }
        }

        stage('Build'){
            steps {
                sh 'mvn package'
            }
        }

        stage('Post Build') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml',
                      allowEmptyResults: false
            }
        }
    }
}