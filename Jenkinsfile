pipeline {
    agent any
    tools {
        jdk 'JDK11'
        gradle 'Gradle6'  // Make sure you configure Gradle in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/cusirramosa1-art/cusirramosa1-art.git'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew clean build'
            }
        }
        stage('Publish to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'localhost:8081',
                    groupId: 'com.example.demo',          // Replace with your group
                    version: '0.0.1-SNAPSHOT',           // Replace with your version
                    repository: 'maven-releases',        // Your Nexus repo
                    credentialsId: 'nexus-credentials',  // Jenkins Nexus credentials
                    artifacts: [
                        [artifactId: 'cusirramosa1-art', classifier: '', file: 'build/libs/*.jar', type: 'jar']
                    ]
                )
            }
        }
    }
}
