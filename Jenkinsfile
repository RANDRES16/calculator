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
                sh "./mvnw jacoco:report"
                sh "./mvnw verify"
            }
        }
    }
}
