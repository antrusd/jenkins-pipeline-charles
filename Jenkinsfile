pipeline {
    agent {
        label "master && linux"
    }

    stages {
        stage('npm build') {
            steps {
                sh "echo 'npm build'"
            }
        }
    }
}
