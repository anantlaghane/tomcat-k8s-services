pipeline {
  agent any

  stages {
    stage('Clone Repo') {
      steps {
        git branch: 'main', url: 'https://github.com/anantlaghane/tomcat-k8s-services.git'
      }
    }
    // stage('Build WAR') {
    //   steps {
    //      dir('mywebapp/mywebapp') {
    //       sh 'mvn clean package'
    //     }
    //   }
    // }
    stage('Deploy WAR to Tomcat') {
      steps {
         script {
          def pod = sh(script: "kubectl get pod -l app=tomcat -o jsonpath='{.items[0].metadata.name}'", returnStdout: true).trim()
          sh "kubectl cp  mywebapp/mywebapp/target/mywebapp.war ${pod}:/usr/local/tomcat/webapps/"
        }
      }
    }
  }
}
