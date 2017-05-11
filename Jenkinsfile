pipeline {
    agent any
    stages {
        stage('Build') {
            agent { docker 'openjdk:8-jre' } 
            steps {
                sh ./gradlew build
            }
        }
    }
}


