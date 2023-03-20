pipeline {
    agent {
        label 'jenkins'
    }
    triggers {
        pollSCM ('* * * * *')
    }
    parameters {
        choice (
            name: 'MAVEN_MAIN',
            choices: ['install', 'package', 'clen']
            description: 'maven-main'
        )
    }
    stages {
        stage('version control system') {
            steps {
                git url: 'https://github.com/qtrajkumarmarch23/spring-petclinic.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps {
                sh 'mvn ${params.MAVEN_MAIN}'
            }
        }
        stage('package') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                   onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'                   
            }
        }
    }
}