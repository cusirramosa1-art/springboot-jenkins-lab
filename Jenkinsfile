pipeline {
    agent any

    environment {
        // Java and Gradle versions can be set in Jenkins globally or here
        JAVA_HOME = tool name: 'JDK 17', type: 'jdk'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main', url: 'https://github.com/cusirramosa1-art/springboot-jenkins-lab.git'
            }
        }

        stage('Build') {
            steps {
                // Build fat jar using Gradle
                sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh './gradlew test'
            }
        }

        stage('Archive Artifact') {
            steps {
                // Archive the built jar
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
