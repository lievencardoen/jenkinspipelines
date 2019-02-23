#!/usr/bin/env groovy
pipeline {
    agent any

    parameters {
      string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

      text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

      booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

      // The value on the first line will be the default.
      choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

      password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

      file(name: "FILE", description: "Choose a file to upload")

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

    // This displays colors using the 'xterm' ansi color map.
    ansiColor('xterm') {
        // Just some echoes to show the ANSI color.
        stage "\u001B[31mI'm Red\u001B[0m Now not"
    }

    stages {
        stage('Checkout scm') {
          steps {
             checkout scm
          }
        }
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
    post {
        always {
            echo 'Always show this message'
        }
        failure {
            echo 'Show this message in case of failure'
        }
    }
}
