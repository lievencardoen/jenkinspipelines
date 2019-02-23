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
        TEST_CREDENTIALS = credentials('CredentialsTestId')

        FOO_CREDENTIALS = credentials('FOOcredentials')

        FOO_CREDENTIALS_SYSTEM_SCOPED = credentials('FOOcredentialsSystemScope')
    }

    options {
      // This displays colors using the 'xterm' ansi color map.
      ansiColor('xterm')
      timeout(time: 1, unit: 'HOURS')
    }

    stages {
        stage('Input Example') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }
        stage('Try Catch Example') {
            try {
                sh 'exit 1'
            }
            catch (exc) {
                echo 'Something failed, I should sound the klaxons!'
                throw
            }
        }
        stage('foo credentials') {
            steps {
                // all credential values are available for use but will be masked in console log
                sh 'echo "FOO is $FOO_CREDENTIALS"'
                sh 'echo "FOO_USR is $FOO_CREDENTIALS"'
                sh 'echo "FOO_PSW is $FOO_CREDENTIALS"'

                //Write to file
                dir("combined") {
                    sh 'echo $FOO_CREDENTIALS > foo.txt'
                }
                sh 'echo $FOO_CREDENTIALS > foo_psw.txt'
                sh 'echo $FOO_CREDENTIALS > foo_usr.txt'
                archive "**/*.txt"
            }
        }
        stage('Checkout scm') {
          steps {
             checkout scm
          }
        }
        stage('Initialize') {
          steps {
            sh 'printenv'
            echo "Running ${env.JOB_NAME} with id ${env.BUILD_ID} on ${env.JENKINS_URL}"
            echo "Hello ${params.PERSON}"
            echo "Biography: ${params.BIOGRAPHY}"
            echo "Toggle: ${params.TOGGLE}"
            echo "Choice: ${params.CHOICE}"
            echo "Password: ${params.PASSWORD}"
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
