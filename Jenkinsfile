pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main',
                    url: 'https://github.com/exantusw1-art/springboot-nexus-hw6.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot project...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Push to Nexus') {
            steps {
                echo 'Uploading artifact to Nexus...'
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '192.168.2.129:8081',
                    groupId: 'com.example',
                    version: '0.0.1-SNAPSHOT',
                    repository: 'maven-releases',
                    credentialsId: 'nexus-credentials',
                    artifacts: [
                        [
                            artifactId: 'demo',
                            classifier: '',
                            file: 'target/demo-0.0.1-SNAPSHOT.jar',
                            type: 'jar'
                        ],
                        [
                            artifactId: 'demo',
                            classifier: '',
                            file: 'pom.xml',
                            type: 'pom'
                        ]
                    ]
                )
            }
        }
    }

    post {
        success {
            echo '✅ JAR successfully uploaded to Nexus!'
        }
        failure {
            echo '❌ Build failed!'
        }
    }
}
