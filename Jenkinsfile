#!groovy
stage('I3GIS_SCAN') {
    steps {
        script {
            echo "Scanning project testing-jenkinsfile with i3gis..."
            final String url = """--location -g --request POST 'http://192.168.1.33:8083/scan' --header 'Content-Type: application/json' --header 'Authorization: Bearer dXC+OroteZQ/uGDFAzAS+ihnsy5TVHnn2VyrArzug43u9IH/6QxTPbHfuTlcIth5lF52dDpteJ2UlAH+fdRaPZSr/UV3HO6bTn9Gn6PRj6gNUsHOpbk3bheHy3mcZ1xdm0FCCap6cxNwDN9VowZJ2g==' -d '{"project_id":93}'"""
            final def (String response, int code) = sh(script: "set +x; curl -s -w '\n%{response_code}' $url", returnStdout: true).trim().tokenize("\n")
            echo "HTTP response status code: $code"
            if (code != 200) {
                echo "Response: " + response
                error("Build failed because scan not success...")
            } else {
                echo "Scan project testing-jenkinsfile with i3gis..."
            }
            echo "Scan project testing-jenkinsfile with i3gis is starting..."
        }
    }
}
stage('I3GIS_SCAN_STATUS') {
    steps {
        script {
            echo "Get scan status..."
            final Boolean status_running = true
            while(status_running) {
                sleep(time: 5, unit: "SECONDS")
                echo "Scan still running..."
                final String url1 = """--location -g --request GET 'http://192.168.1.33:8083/scan/93' --header 'Content-Type: application/json' --header 'Authorization: Bearer dXC+OroteZQ/uGDFAzAS+ihnsy5TVHnn2VyrArzug43u9IH/6QxTPbHfuTlcIth5lF52dDpteJ2UlAH+fdRaPZSr/UV3HO6bTn9Gn6PRj6gNUsHOpbk3bheHy3mcZ1xdm0FCCap6cxNwDN9VowZJ2g=='"""
                final def (String response1, int code1) = sh(script: "set +x; curl -s -w '\n%{response_code}' $url1", returnStdout: true).trim().tokenize("\n")
                echo "HTTP response status code: $code1"
                if (code1 != 200 && code1 != 404) {
                    echo "Response: " + response1
                    error("Scan failed...")
                }
                if(code1 == 404) break
            }
            echo "Scan finished..."
        }
    }
}