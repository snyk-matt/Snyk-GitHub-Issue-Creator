/*
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Python app built'
            }
        }
    }
}
*/

pipeline {
    agent none 
    stages {
        stage('Build') { 
            agent any
            steps {
                snykSecurity snykInstallation: 'installSnyk', snykTokenId: 'snykAuth'
            }
        }
    }
}