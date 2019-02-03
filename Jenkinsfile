#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage('Initialize') {
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
