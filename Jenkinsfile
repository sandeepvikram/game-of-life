pipeline {
    agent { label 'SPC'}
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
            artifacts '**/*.war'
            junit '**/TEST-*.xml'
        }
    }
}