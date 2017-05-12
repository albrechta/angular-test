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
                sh "./gradlew build -xtest -PnodeInstall --no-daemon"
            }
        }
          
        stage('Test: Backend') {
            steps {
                try {
                    sh "./gradlew test -PnodeInstall --no-daemon"
                } catch(err) {
                    throw err
                } finally {
                    junit "**/build/**/TEST-*.xml"
                }
            }
        }

        stage('Test: Frontend') {
            steps {
                try {
                    sh "./gradlew yarn_test -PnodeInstall --no-daemon"
                } catch(err) {
                    throw err
                } finally {
                    junit "**/build/test-results/karma/TESTS-*.xml"
                }    
            }
        }
    }
}
