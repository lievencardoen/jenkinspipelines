#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage('Initialize') {
          steps {
            sh 'printenv'
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
