pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo '🛠️ Building project...'
                // Example: sh './gradlew build'

            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                // Example: sh './gradlew test'
            }
        }
    }

    post {
        always {
            script {
                // ✅ Safe sandbox-friendly way to get Jenkins logs
                def logContent = manager.build.logFile.text

                // Prepare payload
                def payload = [log: logContent]

                // ✅ Send logs to your local Flask webhook
                httpRequest(
                    httpMode: 'POST',
                    url: 'http://127.0.0.1:5001/analyze', // Local Flask endpoint
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload)
                )
            }
        }
    }
}    


        
            
                
             
>>>>>>> f02dd8f (Fix sandbox restriction and connect to Flask webhook)
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                // Example: sh './gradlew test'
            }
        }
    }

    post {
        always {
            script {
                // Capture last 1000 lines from Jenkins console log safely
                def logContent = manager.build.logFile.text

                // Create JSON payload for Flask webhook
                def payload = [log: logContent]

                // Send POST request to local Flask server
                httpRequest(
                    httpMode: 'POST',
                    url: 'http://127.0.0.1:5001/analyze', // 👈 Correct local connection
                    contentType: 'APPLICATION_JSON',
                    requestBody: groovy.json.JsonOutput.toJson(payload)
                )
            }
        }
    }
}
