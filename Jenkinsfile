pipeline {
    agent any

    parameters {
        string(name: 'STUDENT_NAME', defaultValue: 'Nitin', description: 'Enter your name')
        choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], description: 'Select environment')
        booleanParam(name: 'RUN_PYTHON', defaultValue: true, description: 'Run Python?')
    }

    stages {
        stage('Print Parameters') {
            steps {
                echo "Student Name: ${params.STUDENT_NAME}"
                echo "Environment: ${params.ENVIRONMENT}"
            }
        }

        stage('Run Python') {
            when {
                expression { params.RUN_PYTHON == true }
            }
            steps {
                sh 'python3 app.py'
            }
        }
    }

    post {
        success {
            mail to: 'ppnb973@gmail.com',
                 subject: "Pipeline Passed: ${JOB_NAME} #${BUILD_NUMBER}",
                 body: "Hello ${params.STUDENT_NAME}, your pipeline passed successfully!"
        }
        failure {
            mail to: 'ppnb973@gmail.com',
                 subject: "Pipeline Failed: ${JOB_NAME} #${BUILD_NUMBER}",
                 body: "Hello ${params.STUDENT_NAME}, your pipeline failed!"
        }
    }
}