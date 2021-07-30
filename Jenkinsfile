node('SPC') {
    stage('scm') {
        git "https://github.com/sandeepvikram/game-of-life.git"
    }
    stage('build') {
        sh 'mvn package'
    }
    stage('postbuild') {
        junit '**/TEST-*.xml'
        archive '**/*.war'
    }
}