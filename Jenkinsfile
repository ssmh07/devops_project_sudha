@Library(my-shared-library) -

pipeline{
    agent any

    stages{
        stage("Git Checkout"){
            steps{
                gitCheckout{
                    branch: 'main', 
                    url: 'https://github.com/ssmh07/devops_project_sudha.git'
                }
            }

        }
    }
}