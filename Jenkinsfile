#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        TOPLEVELENV = 'toplevelenv'
    }

    stages {
        stage('Initialize') {
          environment {
                INITIALIZE_VAR = 'initialize_var'
          }
          steps {
            sh 'printenv'
            echo "Running ${env.JOB_NAME} with id ${env.BUILD_ID} on ${env.JENKINS_URL}"

          }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
