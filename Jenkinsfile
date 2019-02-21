pipeline {
    agent none
    options {
        checkoutToSubdirectory('source')
    }
    tools {
        maven 'Machai_home'
    }
    options {
        checkoutToSubdirectory('source')
    stages {
        stage ('Build') {
            agent {
              label 'build'
            }
            steps {
                dir ('source') {
                    sh '''mvn -Dmaven.test.failure.ignore=true clean install
                          cp -R target/*.war ansible/hello-world.war'''
                }
                dir ('source/terraform/dev') {
                    sh 'terraform init && terraform apply -auto-approve'
                }
            }
        }
    }
}
