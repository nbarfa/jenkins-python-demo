pipeline {
    agent any

    parameters {
        string(
            name: 'STUDENT_NAME',
            defaultValue: 'Nitin',
            description: 'Enter your name'
        )
        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'staging', 'prod'],
            description: 'Select environment'
        )
        booleanParam(
            name: 'RUN_PYTHON',
            defaultValue: true,
            description: 'Do you want to run Python?'
        )
    }

    stages {
        stage('Print Parameters') {
            steps {
                echo "Student Name: ${params.STUDENT_NAME}"
                echo "Environment: ${params.ENVIRONMENT}"
                echo "Run Python: ${params.RUN_PYTHON}"
            }
        }

        stage('Run Python') {
            when {
                expression { params.RUN_PYTHON == true }
            }
            steps {
                echo "Running Python for ${params.STUDENT_NAME}..."
                sh 'python3 app.py'
            }
        }

        stage('Deploy') {
            when {
                expression { params.ENVIRONMENT == 'prod' }
            }
            steps {
                echo "Deploying to PRODUCTION for ${params.STUDENT_NAME}!"
            }
        }
    }

    post {
        success {
            echo "Pipeline completed for ${params.STUDENT_NAME}!"
        }
    }
}