#!/usr/bin/env groovy
pipeline {
    agent any

    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }

    environment {
        TOPLEVELENV = 'toplevelenv'

        // Using returnStdout CC will be equal to clang
        CC = """${sh(
                returnStdout: true,
                script: 'echo "clang"'
            )}"""
        // Using returnStatus EXIT_STATUS will be equal to 1
        EXIT_STATUS = """${sh(
                returnStatus: true,
                script: 'exit 1'
            )}"""

        // CredentialsTestId must exist in Jenkins Credentials
        TEST_CREDENTIALS=credentials('CredentialsTestId')
    }

    stages {
        stage('Initialize') {
          steps {
            sh 'printenv'
            echo "Running ${env.JOB_NAME} with id ${env.BUILD_ID} on ${env.JENKINS_URL}"

          }
        }
        stage('Build') {
          // Scope of INITIALIZE_VAR will only be this stage
          environment {
                INITIALIZE_VAR = 'initialize_var'
          }
            steps {
                echo 'Building..'
                sh 'printenv'
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
