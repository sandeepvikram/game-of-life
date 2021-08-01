pipeline {
    agent { label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'branch to build')
    }
    stages{
        stage('scm') {
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/sandeepvikram/game-of-life.git'
            }
        }
        stage('build') {
            steps {
                sh 'mvn package'
            }
        }
    }
    post {
        success {
            archive '**/*.war'
            junit '**/TEST-*.xml'
        }
        always {
            echo 'I will always say Hello again!'
        }
    }
}