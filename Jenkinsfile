pipeline {
    agent any
    stages {
        stage('Clean') {
            steps {
                sh "chmod +x gradlew"
                sh "./gradlew clean --no-daemon"
            }
        }
        
        stage('Build') {
            agent { docker 'openjdk:8-jdk' }
            steps {
                sh "./gradlew build -xtest --no-daemon"
            }
        }
          
        stage('Test: Backend') {
            steps {
                sh "./gradlew test --no-daemon"
                junit "**/build/**/TEST-*.xml"
            }
        }

        stage('Test: Frontend') {
            steps {
                sh "./gradlew yarn_install -PnodeInstall --no-daemon"
                sh "./gradlew yarn_test -PnodeInstall --no-daemon"
                junit "**/build/test-results/karma/TESTS-*.xml"   
            }
        }
    }
}
