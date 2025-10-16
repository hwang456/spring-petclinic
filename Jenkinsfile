pipeline {
  agent any

  tools {
  maven 'M3'
    jdk 'JDK21'
  }
  
  stages {
    // Github clone
    stage('Git clone') {
      steps {
        git url: 'https://github.com/hwang456/spring-petclinic.git/', branch: 'main'
      }
    }

    //Maven Build
    stage('Maven Build') {
      steps {
        sh 'mvn -Dmaven.test.failure.ignore=true clean package'
  }
}
  }
}
