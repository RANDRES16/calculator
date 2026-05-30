pipeline {
    agent any

    stages {

        stage("Compile") {
            steps {
                sh "./mvnw compile"
            }
        }

        stage("Unit test") {
            steps {
                sh "./mvnw test"
            }
        }

        stage("Code coverage") {
            steps {
                sh "./mvnw clean verify"

                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Report'
                ])
            }
        }
    }
}
