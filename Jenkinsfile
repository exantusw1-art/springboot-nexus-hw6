stage('Push to Nexus') {
    steps {
        echo 'Uploading artifact to Nexus...'
        nexusArtifactUploader(
            nexusVersion: 'nexus3',
            protocol: 'http',
            nexusUrl: '192.168.2.129:8081',
            groupId: 'com.example',
            version: '1.0.0',
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
