pipeline {
    agent { label 'JDK_17_UBUNTU' }
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
        stage('mvn package') {
            tools {
                jdk 'JDK_17_UBUNTU'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
                }
        }
    }
}
