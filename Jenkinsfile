post {
    always {
        script {
            // Capture build log safely using manager.build.logFile
            def log = readFile(manager.build.logFile)
            def payload = [log: log]

            httpRequest(
                httpMode: 'POST',
                url: 'http://host.docker.internal:5001/analyze',  // Flask webhook
                contentType: 'APPLICATION_JSON',
                requestBody: groovy.json.JsonOutput.toJson(payload)
            )
        }
    }
}
