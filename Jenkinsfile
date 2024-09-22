@Library('my-shared-library') _

pipeline {
    agent any

    parameters {
        choice(name: 'action', choices: ['Create', 'Delete'], description: 'Choose create/delete')
    }

    stages {
        stage("Git Checkout") {
            when { expression { params.action == 'Create' } }
            steps {
                gitCheckout(
                    branch: 'main', 
                    url: 'https://github.com/ssmh07/devops_project_sudha.git'
                ) 
            }
        }

        stage("Unit Test Maven") {
            when { expression { params.action == 'Create' } }
            steps {
                script {
                    mvnTest()
                }
            } 
        }

        stage("Integration Test Maven") {
            when { expression { params.action == 'Create' } }
            steps {
                script {
                    mvnIntegrationTest()
                }
            } 
        }

        stage('Static Code Analysis: SonarQube') {
            when { expression { params.action == 'Create' } }
            steps {
                script {
                    def SonarQubecredentialsId = 'sonar-api'
                    staticCodeAnalysis(SonarQubecredentialsId)
                }
            }
        }

        stage('Quality Gate Status Check: SonarQube') {
            when { expression { params.action == 'Create' } }
            steps {
                script {
                    def SonarQubecredentialsId = 'sonar-api'
                    QualityGateStatus(SonarQubecredentialsId)
                }
            }
        }

        stage('Maven Build') {
            when { expression { params.action == 'Create' } }
            steps {
                script {
                    mvnBuild()
                }
            }
        }

        // Optionally, you can add a stage for deletion if needed
        stage("Delete Resources") {
            when { expression { params.action == 'Delete' } }
            steps {
                script {
                    // Add your deletion logic here
                }
            }
        }
    }
}
