pipeline {
  agent any

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/anantlaghane/tomcat-k8s-services.git'
      }
    }

    stage('Deploy WAR to Tomcat') {
      steps {
        script {
          def pod = sh(script: "kubectl get pod -l app=tomcat -o jsonpath='{.items[0].metadata.name}'", returnStdout: true).trim()
          sh "kubectl cp target/yourapp.war ${pod}:/usr/local/tomcat/webapps/"
        }
      }
    }
  }
}
