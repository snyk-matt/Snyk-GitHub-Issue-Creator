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
            agent {
                docker {
                    image 'python:3-alpine' 
                }
            }
            steps {
                snykSecurity projectName: 'Jenkins Pipeline goof', snykInstallation: 'installSnyk', snykTokenId: 'snykAuth'
            }
        }
    }
}