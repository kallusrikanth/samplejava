pipeline {
    agent any
      tools {
             jdk "java10"
             maven  "maven3"
       }
    stages {
        stage('Maven Build') {
            steps { 
                sh 'mvn --version'
            }
        }
    }
}
