@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
        choice(name: 'action', choices: ['Create', 'Delete'], description: 'Choose create/delete')
    }

    stages {
        stage("Git Checkout") {
            when { expression { params.action == 'Create' } } // Changed 'param' to 'params'
            steps {
                gitCheckout(
                    branch: 'main', 
                    url: 'https://github.com/ssmh07/devops_project_sudha.git'
                ) 
            }
        }

        stage("Unit Test Maven") {
            when { expression { params.action == 'Create' } } // Changed 'param' to 'params'
            steps {
                script {
                    mvnTest()
                }
            } 
        }

        stage("Integration Test Maven") {
            when { expression { params.action == 'Create' } } // Changed 'param' to 'params'
            steps {
                script {
                    mvnIntegrationTest()
                }
            } 
        }

        stage("Static Code Analysis: SonarQube") {
            when { expression { params.action == 'Create' } } // Changed 'param' to 'params'
            steps {
                script {
                    def SonarQubecredentialsId = 'sonar-api'
                    staticCodeAnalysis(SonarQubecredentialsId)
                }
            } 
        }
    }
}
