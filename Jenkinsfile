// Define variable
def app_tag = "app.1.$BUILD_NUMBER"
pipeline {
    agent any
            stages {
                stage('Build') {
                    steps {
                        sh 'npm install'
                    }
                }
                stage('SonarQube Analysis'){
                  // environment {     
                    // SCANNER_HOME = tool 'SonarQubeScanner'
                  // }
                    steps {
                        withSonarQubeEnv('sonarqube') {
                        sh "/opt/sonar-scanner/bin/sonar-scanner \
                            -Dsonar.projectKey=node_js_project_test \
                            -Dsonar.projectName=demo-dhl-nodejs \
                            -Dsonar.login=admin \
                            -Dsonar.password=1Cloud@hub20#22"
                    }
                    }
                    }
                stage('Building image') {
                    steps {
//                          sh "sudo docker build -t myubuntuimage:version1 ."
                          sh "sudo az acr build --image aksdemo/restapi:${app_tag}   --registry dhltestcluster   --file Dockerfile ."
                          sh "echo docker"
                    }
                }



           }
//            post {
//              always {
//                  cleanWs()
//              }
//          }
}
