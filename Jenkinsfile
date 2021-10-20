pipeline {
  agent any

  tools{
      maven 'Maven 3.6.3'
  }
  stages{
      stage("build"){
          steps{
              sh 'mavan compile'
          }
      }
      stage("test"){
          steps{
              sh 'mavan clean test'
          }
      }
      stage("package"){
          steps{
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
