pipeline {
agent any
tools {nodejs "nodenv"}
stages {
 stage("Code Checkout from GitLab") {
  steps {
   git branch: 'master',
    credentialsId: 'gitlab_user_pass',
    url: 'http://64.227.109.36:10080/root/nodejs-demoapp.git'
  }
 }
   stage('Code Quality Check via SonarQube') {
   steps {
       script {
       def scannerHome = tool 'sonarqube';
           withSonarQubeEnv("sonarqube-container") {
           sh "${tool("sonarqube")}/bin/sonar-scanner \
           -Dsonar.projectKey=gitlab_node-js-demoapp \
           -Dsonar.sources=. \
           -Dsonar.css.node=. \
           -Dsonar.host.url=http://64.227.109.36:9000 \
           -Dsonar.login=68d0c3f18b3109c2ba69395b2f5f76648879fac8"
               }
           }
       }
   }
   stage("Install Project Dependencies") {
   steps {
       nodejs(nodeJSInstallationName: 'nodenv'){
           sh "npm install"
           }
       }
   }
}
}
