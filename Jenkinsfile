pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
                // Example: sh './gradlew build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Example: sh './gradlew test'
            }
        }
    }

    post {
        always {
            script {
                // Safe sandbox-friendly way to get Jenkins logs
                def logContent = manager.build.logFile.text

                // Prepare payload
                def payload = [log: logContent]

                // Send logs to your local Flask webhook
                httpRequest(
                    httpMode: 'POST',
                    url: 'http://127.0.0.1:5001/analyze',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload)
                )
            }
        }
    }
}

