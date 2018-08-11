pipeline {
    agent any
      tools {
             jdk "java10"
             maven  "maven3"
       }
    stages {
        stage('Maven Build') {
            steps { 
                sh 'mvn clean install'
            }
        }

        stage('Maven Package') {
            steps {
                sh 'mvn package'
            }
        }
      

        stage('Artifactory configuration') {
           steps {
             script {
               def server = Artifactory.server url: 'http://jfrog.baladigitalcloud.com/artifactory', username: 'admin', password: 'Kurtw@11'
                server.bypassProxy = true
                rtMaven.tool = "maven3"
                rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
                rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server
            def uploadSpec = """{
               "files": [
                  {
                    "pattern": "target/*.war",
                    "target": "libs-snapshot-local/"
                   }
                  ]
                }"""
                server.upload(uploadSpec)
    }




    }
}
