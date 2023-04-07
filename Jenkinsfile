pipeline {
    agent { label 'JDK_17' }
    triggers { pollSCM ( '* * * * *')}
    parameters {
        choice (name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/comingapril/spring-petclinic.git',
                    branch: 'main'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_17_UBUNTU'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
                }
        }
            }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }