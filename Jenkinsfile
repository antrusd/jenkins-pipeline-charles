pipeline {
    agent {
        label "linux"
    }

    stages {
        stage('npm build') {
            steps {
                sh "echo 'npm build'"
                sh "echo ${env.SDB}"
            }
        }
    }
}
