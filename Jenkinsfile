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
                // ✅ Get Jenkins log file path (sandbox-safe)
                def logFile = currentBuild.rawBuild.getLogFile()

                // Read the last 1000 lines safely
                def logText = logFile.readLines().takeRight(1000).join('\n')

                // Prepare JSON payload
                def payload = [log: logText]

                // ✅ Send log to your Flask server
                httpRequest(
                    httpMode: 'POST',
                    url: 'url: 'http://10.0.0.112:5001/analyze',
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload)
                )
            }
        }
    }
}

