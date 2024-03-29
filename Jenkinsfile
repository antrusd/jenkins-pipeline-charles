pipeline {
    agent {
        label "linux"
    }

    stages {
        stage('checkout repository') {
            steps {
                dir ('build') {
                    echo "git '${SERVICE}'"
                }
            }
        }
        stage('npm build') {
            steps {
                dir ('build') {
                    sh "echo 'npm build'"
                }
            }
        }
        stage('gradle build') {
            steps {
                dir ('build') {
                    sh "echo 'gradle build'"
                }
            }
        }
        stage('deploy') {
            steps {
                sh "echo 'scp -r build/build/libs/service.jar target-server.com:/opt/service_name/'"
            }
        }
        stage('scratch database') {
            when {
                expression {
                    env.SCRATCH_DATABASE == 'true'
                }
            }
            steps {
                sh "echo 'ssh target-server.com ./dbteardown.sh'"
            }
        }
        stage('copy test database') {
            when {
                expression {
                    env.COPY_TEST_DATA == 'true'
                }
            }
            steps {
                sh "echo 'scp -r testdata.sql target-server.com:/target/path/'"
                sh "echo 'ssh target-server.com ./testdata.sh'"
            }
        }
        stage('restart apps') {
            steps {
                sh "echo 'ssh target-server.com service application restart'"
            }
        }
    }
}
