pipeline {
    agent any
    tools {
        maven 'Maven'
        jdk 'jdk'
    }
    stages {
        stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/Nouman72884/jenkins-s3-artifacts.git"
            }
        }
        stage ('build stage') {
            steps {
                sh 'mvn clean install package'
            }
        }
        // stage ('publish artifacts') {
        //     steps {
        //         sh 'cd ../..'
        //         sh 'ls'
        //         s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'nouman-work', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: true, noUploadOnFailure: true, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '~/. m2/repository/', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'artifacts', userMetadata: []
        //     }
        // }
        stage ('upload artifacts') {
            steps {
                script {
                    withAWS(region: 'us-east-1',credentials:'aws-credentials') {
                        s3Upload(file:'/var/jenkins_home/.m2/repository/', bucket:'nouman-work', path:'artifacts/')    
                            }
                }
            }
        }
    }
}