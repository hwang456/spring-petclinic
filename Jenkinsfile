pipeline {
  agent any

  stages {
    // Github clone
    stage('Git clone') {
      steps {
        git url: 'https://github.com/hwang456/spring-petclinic.git/', branch: 'main'
      }
    }
  }
}
