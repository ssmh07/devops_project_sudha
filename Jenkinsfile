@Library('my-shared-library') _

pipeline{
    agent any

    parameters{
        choice{name: 'action', choices: 'Create\nDelete', Description: 'Choose create/delete'}
    }

    stages{
        
        when{ expression { param.action == 'create' }}
        stage("Git Checkout"){
            steps{
                gitCheckout(
                    branch: 'main', 
                    url: 'https://github.com/ssmh07/devops_project_sudha.git'
                ) 
            }
        }

        stage("Unit Test maven"){
            when{ expression { param.action == 'create' }}
            steps{
                script{
                     mvnTest()
                }
                   
             } 
         }
         stage("Integration Test maven"){
            when{ expression { param.action == 'create' }}
            steps{
                script{
                     mvnIntegrationTest()
                }
                   
             } 
         }

         stage("Static code analysis : SonarQube"){
            when{ expression { param.action == 'create' }}
            steps{
                script{
                     staticCodeAnalysis()
                }
                   
             } 
         }
     }
}

staticCodeAnalysis