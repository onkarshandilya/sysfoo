pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        sh 'mvn clean test'
      }
    }
    stage('package and publish'){
        when {
          branch 'master'
        }
        parallel {
        stage('package') {
            
                agent {
                    docker {
                    image 'maven:3.6.3-jdk-11-slim'
                    }

                }
                steps {
                    sh 'mvn package -DskipTests'
                    archiveArtifacts 'target/*.war'
                }
            }

        stage('Docker BnP') {

                agent any
                steps {
                    script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                        def dockerImage = docker.build("onkarshandilya/sysfoo:v${env.BUILD_ID}", "./")
                        dockerImage.push()
                        dockerImage.push("latest")
                        dockerImage.push("dev")
                    }
                    }

                }
        }
    }
    }

    stage('Deploy to dev') {
      when { branch 'master' }
      agent any
      steps {
        echo 'Deploying to Dev environment with Docker compose'
        sh 'docker-compose up -d'
      }
    }
    
  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}