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
                echo "Deploying to PRODUCTION!"
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
            mail(
                to: 'ppnb973@gmail.com',
                subject: "✅ Pipeline Passed: ${JOB_NAME} #${BUILD_NUMBER}",
                body: """
Hello ${params.STUDENT_NAME}!

Your Jenkins pipeline passed successfully!

Job: ${JOB_NAME}
Build: #${BUILD_NUMBER}
Environment: ${params.ENVIRONMENT}
Status: SUCCESS ✅
                """