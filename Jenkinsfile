pipeline {
    agent {
        label "linux"
    }

    stages {
        stage('npm build') {
            steps {
                sh "echo 'npm build'"
            }
        }
        stage('gradle build') {
            steps {
                sh "echo 'gradle build'"
            }
        }
        stage('deploy') {
            steps {
                sh "echo 'scp -r build/libs/service.jar target-server.com:/opt/service_name/'"
            }
        }
        stage('scratch database') {
            when {
                expression {
                    env.ScratchDatabase == true
                }
            }
            steps {
                sh "echo 'ssh target-server.com ./dbteardown.sh'"
            }
        }
        stage('copy test database') {
            when {
                expression {
                    env.CopyTestData == true
                }
            }
            steps {
                sh "echo 'scp -r testdata.sql target-server.com:/target/path/'"
                sh "echo 'ssh target-server.com ./testdata.sh'"
            }
        }
        stage('restart apps') {
            steps {
                sh "echo 'ssh target-server.com /etc/init.d/application restart'"
            }
        }
    }
}
