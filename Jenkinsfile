pipeline {
    agent { label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'branch to build')
    }
    environment {
        CI_ENV ='DEV'
    }
    stages{
        stage('scm') {
            environment {
                DUMMY = 'FUN'
            }
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/sandeepvikram/game-of-life.git'
                echo env.CI_ENV
                echo env.DUMMY
            }
        }
        stage('build') {
            steps {
                echo env.GIT_URL
                timeout(time:10, unit: 'MINUTES') {
                sh 'mvn package'
                }
                
            }
        }
        stage('SONAR ANALYSIS') {
            steps {
               withSonarQubeEnv('SONAR-8.9LTS') {
                    // requires SonarQube Scanner for Maven 3.2+
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        }
    }
    post {
        success {
            archive '**/*.war'
            junit '**/TEST-*.xml'
        }
        always {
            echo 'The code analysis is good!'
        }
    }
}