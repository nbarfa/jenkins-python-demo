pipeline{
    agent any

    stages{
        stage('Checkout Code'){
            steps{
                echo 'Pulling code from github'
                checkout scm

            }

        }
        stage('Run Python'){
            steps{
                echo 'Running Python Program'
                sh 'python3 app.py'
            }
        }
    }

    post{
        success{
            echo 'Pipeline Completed Successfully'

        }
        failure{
            echo 'Pipeline Failed'
        }
    }
}
