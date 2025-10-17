pipeline {
  agent any

  tools {
  maven 'M3'
    jdk 'JDK21'
  }
  environment {
    DOCKERHUB_CREDENTILAS = credentials('dockerCredential')
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

    // Docker Image 생성
    stage('Docker Image Build') {
      steps{
        dir("$(env.WORKSPACE}") {
          sh """
          docker build -t spring-petclinic:$BUILD_NUMBER .
          docker tag spring-petclinic:$BUILD_NUMBER hwang567/spring-petclinic:latest
          """
        }
      }
    }
    
// Docker Login and Push
    stage ('Docker Login') {
      steps{
        sh """
        echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_URR --password-stdin
        docker push hwang456/spring-petclinic:latest
        """
      }
    }
    
    //Docker Image Remove
    stage ('Docker Image Remove') {
      steps{
        sh """
        docker rmi spring-petclinic:$BUILD_NUMBER
        docker rmi hwang567/spring-petclinic:latest
        """
  }
}
