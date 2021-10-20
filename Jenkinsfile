pipeline {
  agent any

  tools{
      maven 'Maven 3.6.3'
  }
  stages{
      stage("build"){
          steps{
              echo 'compile maven app'
              sh 'mavan compile'
          }
      }
      stage("test"){
          steps{
              echo 'test maven app'
              sh 'mavan clean test'
          }
      }
      stage("package"){
          steps{
              echo 'package maven app'
              sh 'mvn package -DskipTests'
          }
      }
  }

  post{
    always{
        echo 'This pipeline is completed..'
    }
  }
}
