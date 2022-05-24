pipeline {
    options {
        // set a timeout of 30 minutes for this pipeline
        timeout(time: 30, unit: 'MINUTES')
    }
    agent {
      node {
        label 'master'
      }
    }

    stages {

        stage('stage 1') {
            steps {
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                                oc create deployment jenkinsdeployment1 --image quay.io/mayank123modi/mayanknginximage}"
                        }
                    }
                }
            }
        }

        stage('stage 2') {
            steps {
                sh 'oc expose deplyment jenkinsdeployment1  --port 80'
            }
        }

        stage('manual approval') {
            steps {
                timeout(time: 4, unit: 'MINUTES') {
                    input message: "Move to stage 3?"
                }
            }
        }

        stage('stage 3') {
            steps {
                sh 'oc expose service jenkinsdeployment1'
            }
        }

    }
}
