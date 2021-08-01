pipeline {
    agent { label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    parameters {
        git branch: "${params.BRANCH}", url: 'https://github.com/sandeepvikram/game-of-life.git'
    }
    stages{
        stage('scm') {
            steps {
                git branch: 'master', url: 'https://github.com/asquarezone/game-of-life.git'
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