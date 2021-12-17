pipeline{
    agent any
    tools {
     jdk 'JAVA'
     maven 'MAVEN-3.8.3'
    }
    stages{
        stage('Git checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/sivap083/hello-world.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh "mvn clean install package"
                # sh "mv target/*.war target/myapp.war"
            }
        }
        stage('Publish Artifact to S3') {
            steps {
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'myrepoartifact', excludedFile: 'webapp/target', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: 'webapp/target/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'artifacts_s3', userMetadata: []
            }
        }
    }
}
