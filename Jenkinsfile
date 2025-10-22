pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Building project...'
        // example build command: sh './gradlew build'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        // example: sh './gradlew test'
      }
    }
  }

post {
    always {
        script {
            // Capture last 1000 lines from the Jenkins console log
            def log = currentBuild.rawBuild.getLog(1000).join("\n")

            // Create JSON payload for Flask webhook
            def payload = [log: log]

            // Send POST request to your Flask server
            httpRequest(
                httpMode: 'POST',
                url: 'http://127.0.0.1:5001/analyze',  // Flask webhook
                contentType: 'APPLICATION_JSON',
                requestBody: groovy.json.JsonOutput.toJson(payload)
            )
        }
    }
}
