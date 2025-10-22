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
    failure {
        script {
            def log = readFile('build.log')
            def payload = [log: log]
            httpRequest(
                httpMode: 'POST',
                url: 'http://127.0.0.1:5001/analyze',
                contentType: 'APPLICATION_JSON',
                requestBody: groovy.json.JsonOutput.toJson(payload)
            )
        }
    }
}
